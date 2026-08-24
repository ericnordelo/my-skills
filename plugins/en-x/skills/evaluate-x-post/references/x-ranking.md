# X Ranking Context

Last verified: 2026-08-20 against `xai-org/x-algorithm` commit `aad7179773944e17eb8798bbbf0231d6cd6c1ffc` (published 2026-08-19).

Use this reference to evaluate distribution conditions. It is a snapshot of public code, not a complete description of every production rule. X says repository defaults are updated toward primary production values, while experiments may override them for portions of traffic.

## Candidate retrieval and scoring

- In-network candidates come from recent posts by accounts the viewer follows.
- Out-of-network candidates come from Phoenix semantic retrieval and SimClusters engagement similarity.
- Phoenix predicts each viewer's probability of actions such as favorite, reply, repost, quote, share, follow, and negative feedback. Ranking weights multiply predicted probabilities, not raw action counts.
- A post must be retrieved before any scoring adjustment can help it. Topic consistency, specific technical language, and a relevant engagement graph are therefore useful strategy inferences, not formal eligibility conditions.

Primary source: [X For You feed overview](https://github.com/xai-org/x-algorithm/blob/aad7179773944e17eb8798bbbf0231d6cd6c1ffc/README.md#overview).

## New-author cold start

The public code names this mechanism `AuthorColdStart` or the New-Author Boost. It is not a global creator pool. It runs separately for each viewer's candidate set.

Current default eligibility and behavior:

- Original posts only: replies and reposts are excluded.
- Author follower count is at most 1,000; exactly 1,000 qualifies.
- Hydrated `view_count` is strictly below 1,000. The parameter is named an impression threshold.
- The candidate must have a nonzero score and already rank inside the top 85% of nonzero candidates for that viewer.
- At most one eligible candidate is selected per request.
- Thompson sampling is disabled by default, so the highest-scoring eligible candidate is selected.
- The selected candidate's score is raised to at least the score at zero-based index 15, the 16th candidate under the default `15..16` range. This does not guarantee final position 16.
- The feature is enabled by default.

The `ColdStartMaxPostAgeSecs` default is 86,400 seconds, but the implementation enforces this age gate only for the experimental treatment arm. Holdout and control paths bypass this particular gate. Treat the first 24 hours as the practical opportunity window, not a universal hard condition. The general feed pipeline filters older candidates separately.

Primary sources:

- [Eligibility and selection implementation](https://github.com/xai-org/x-algorithm/blob/aad7179773944e17eb8798bbbf0231d6cd6c1ffc/home-mixer/scorers/author_cold_start.rs#L133-L303)
- [Cold-start production defaults](https://github.com/xai-org/x-algorithm/blob/aad7179773944e17eb8798bbbf0231d6cd6c1ffc/home-mixer/params/param.rs#L647-L694)
- [X explanation of experiments and defaults](https://github.com/xai-org/x-algorithm/blob/aad7179773944e17eb8798bbbf0231d6cd6c1ffc/README.md#experiments-and-configuration)

Do not recommend suppressing views to remain eligible. Crossing 1,000 views is a successful outcome even though cold-start eligibility ends.

## Author diversity

Author diversity is enabled by default. With decay `0.5` and floor `0.25`, candidates from the same author receive these multipliers in score order:

- First: `1.0`
- Second: `0.625`
- Third: `0.4375`
- Later candidates approach the `0.25` floor

This acts within each viewer's candidate set, not as a fixed global cooldown. The practical inference is to publish one primary original at a time and avoid stacking weak originals close together. Spacing does not guarantee that older posts leave every candidate set.

Primary sources:

- [Author-diversity defaults](https://github.com/xai-org/x-algorithm/blob/aad7179773944e17eb8798bbbf0231d6cd6c1ffc/home-mixer/params/param.rs#L221-L239)
- [Author-diversity calculation](https://github.com/xai-org/x-algorithm/blob/aad7179773944e17eb8798bbbf0231d6cd6c1ffc/home-mixer/scorers/ranking_scorer.rs#L643-L725)

## Replies

- Replies do not qualify for the new-author cold-start boost.
- An out-of-network reply is removed from the normal For You candidate path. Replies primarily gain value through the parent conversation, followers, author interaction, and relationship building.
- The parent post's audience fit, freshness, saturation, and likelihood of author response matter more than raw author size.

Primary source: [Out-of-network reply filter](https://github.com/xai-org/x-algorithm/blob/aad7179773944e17eb8798bbbf0231d6cd6c1ffc/home-mixer/filters/oon_retweet_reply_filter.rs#L1-L22).

### High-visibility conversations

A separate Grox reply-ranking flow is eligible when either the direct reply target or the conversation root author has more than 60,000 followers. There is no public 6,000-follower cutoff.

The model receives the thread plus signals that can include follower count, recent reply volume, safety information, legitimate blocks, and whether the reply was pasted. The exact scoring prompt is not public, so do not claim a fixed penalty for pasting or a safe numeric reply-volume limit. The defensible strategy inference is to use a higher quality threshold for these saturated conversations and avoid reusable generic replies.

Primary sources:

- [60,000-follower eligibility flow](https://github.com/xai-org/x-algorithm/blob/aad7179773944e17eb8798bbbf0231d6cd6c1ffc/grox/flows/reply_spam/task_filter.py#L184-L249)
- [Thread signals supplied to the model](https://github.com/xai-org/x-algorithm/blob/aad7179773944e17eb8798bbbf0231d6cd6c1ffc/grox/core/lm/thread.py#L30-L60)
- [Reply scorer implementation](https://github.com/xai-org/x-algorithm/blob/aad7179773944e17eb8798bbbf0231d6cd6c1ffc/grox/flows/reply_spam/classifier_reply_ranking.py#L22-L151)

## Separate unexplored-post signal

Phoenix also trains a `post_unexplored` signal for original posts at most 24 hours old whose views are below a time-ramped target reaching 3% of follower count at 24 hours. Its current scoring default is small and restricted to in-network candidates. It is not the same mechanism as the 1,000-follower cold-start boost and should not dominate an evaluation.

Primary sources:

- [Unexplored-post label calculation](https://github.com/xai-org/x-algorithm/blob/aad7179773944e17eb8798bbbf0231d6cd6c1ffc/phoenix/xrex/data/recsys/recsys_batch.py#L52-L80)
- [Unexplored-post scoring defaults](https://github.com/xai-org/x-algorithm/blob/aad7179773944e17eb8798bbbf0231d6cd6c1ffc/home-mixer/params/param.rs#L378-L402)

## Eric's operating context

- Optimize for qualified profile visits and followers among technical builders, not broad low-conversion impressions.
- Default original-post windows: `12:00-13:00` and `17:00-18:00` Europe/Madrid. The later window overlaps Europe and the US morning.
- Preferred live-reply windows: `16:30-18:30` and `21:00-23:15` Europe/Madrid.
- Reply portfolio: prioritize relevant peers and likely mutuals, then domain leaders. Treat accounts above 60,000 followers as selective high-upside opportunities rather than a daily quota.
- For replies, `80+` is high priority; `70-79` is worthwhile for relevant peers or domain leaders; below `70` is normally a skip. Require `80+` for high-visibility conversations.

These are strategy defaults, not facts encoded by X.

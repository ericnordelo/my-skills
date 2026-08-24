---
name: evaluate-x-post
description: Evaluate and score draft X originals, replies, and quote posts for substance, audience fit, natural voice, and realistic reach potential. Use when Eric asks whether a post is good, what to avoid, why it may underperform, or how to improve reach. This skill evaluates text and posting context; it does not publish, schedule, or discover opportunities.
---

# Evaluate X Post

Evaluate a draft without confusing an editorial heuristic with X's private ranking score. Optimize for qualified followers and useful technical relationships, not raw impressions or generic engagement.

Return analysis only. Never publish, schedule, like, repost, follow, or perform another social action. Do not rewrite the draft unless Eric explicitly asks for an optimized version.

## Establish the mode

Classify the draft as an **original**, **reply**, or **quote post**. For a reply or quote post, use the source post as required context. Ask for it only when it is missing and a faithful evaluation is impossible; otherwise score what is known and mark missing reach context as unknown.

Unless Eric specifies another audience, use his growth audience as the default: technical builders interested in open source, smart-contract security, OpenZeppelin, Cairo/Starknet/Sui, and practical AI-assisted development. Do not penalize a deliberately personal or off-topic post merely for serving a different purpose; name the tradeoff instead.

Read [references/x-ranking.md](references/x-ranking.md) when the request concerns reach, cold-start eligibility, ranking behavior, timing, author size, or reply opportunity. Treat that reference as a dated snapshot. If Eric explicitly asks for the current or exact algorithm, verify the primary X repository again before relying on values that may have changed.

## Score the draft

Give one **draft quality score from 0 to 100**. This is a calibrated editorial score, not a prediction of impressions or an X-internal score. Do not inflate it to be agreeable.

### Original rubric

- Specific, defensible central claim: 25
- Firsthand detail, evidence, mechanism, or inspectable artifact: 20
- Clarity, concision, and Eric's natural voice: 20
- Audience fit and semantic retrievability: 20
- Credible reason to reply, share, quote, or follow: 15

An original can score well without a question. Do not award points for manufactured hooks, outrage, vague inspiration, or engagement bait.

### Reply rubric

- Clear anchor to the source post: 20
- New information, mechanism, example, counterexample, or implementation detail: 30
- Relevance of the source audience and relationship opportunity: 20
- Natural, concise, technically precise voice: 15
- A complete consequence or a genuinely useful question: 15

A reply that only agrees, praises, summarizes, or asks a generic question cannot score above 60. If the source post is unavailable, do not award source-anchor or audience-opportunity points speculatively.

### Quote-post rubric

- Standalone contribution beyond the quoted post: 30
- A real reason to quote rather than reply: 20
- Concrete substance or defensible mechanism: 20
- Clarity and natural voice: 15
- Fit with the intended audience: 15

Recommend a reply or no post when the commentary does not justify rebroadcasting the source.

## Interpret the score

- `90-100`: exceptional and specific
- `80-89`: strong; ready for review
- `70-79`: worthwhile but one material improvement remains
- `60-69`: weak or under-specified
- `<60`: skip or rebuild the idea

For reply prioritization, use a stricter operational rule:

- `80+`: high-priority opportunity
- `70-79`: worthwhile for a relevant peer or domain leader
- `<70`: skip unless it continues a real relationship
- For a conversation whose direct target or root author exceeds 60,000 followers, require `80+`; this is a strategy threshold, not an X-published score conversion.

## Assess reach separately

Report **Reach setup: High, Medium, Low, or Unknown**. Do not fold unknown timing or account context into the writing score.

For originals, consider:

- Whether it is an original rather than a reply or repost.
- Cold-start eligibility in principle, without promising a boost.
- Topic clarity for Phoenix/SimClusters retrieval.
- Whether another recent original from Eric may compete through author diversity.
- Whether the intended time overlaps the target audience.
- Whether the post gives a qualified reader a reason to visit or follow the profile.

For replies, consider:

- Source-post age, saturation, and audience fit.
- Whether the author is a likely mutual, domain leader, or large-account reach opportunity.
- Whether Eric is early enough to be read in the conversation.
- Whether the reply contributes enough to survive the stricter high-visibility context above 60,000 followers.
- The fact that replies from accounts a viewer does not follow are removed from the normal out-of-network For You candidate path, making parent-thread selection and relationship value central.

If posting context is missing, state the two facts that would most change reach readiness instead of asking a long questionnaire.

## Recommend improvements

Identify the single highest-impact change first. Tie every warning to the actual draft; do not return a generic social-media checklist.

When Eric asks to optimize or rewrite:

1. Preserve his claim, uncertainty, facts, and personality.
2. Produce one recommended revision, with at most one meaningfully different alternative.
3. Show the original and revised scores, explaining only the points that changed.
4. Never invent experience, evidence, metrics, or technical details.

Avoid adding hashtags, emojis, dramatic fragments, forced line breaks, generic hooks, praise openers, manufactured questions, or calls for engagement unless the specific post genuinely needs one and it fits Eric's voice.

## Default output

Keep the normal response quick:

```text
Score: 78/100 - Worthwhile
Reach setup: Medium - [specific reason]
Why: [strongest property and main weakness]
Best change: [one actionable edit]
Avoid: [up to three draft-specific mistakes]
```

For an original that may qualify, add `Cold start: eligible in principle`, `not applicable`, or `unknown`. For a reply, add `Opportunity: high priority`, `worthwhile`, or `skip`.

Provide the category breakdown only when Eric asks for detail or when the score would otherwise be difficult to defend.

## Evidence discipline

When discussing the algorithm, distinguish:

- **Code fact:** directly visible in the cited public source.
- **Production default:** a configurable value that X says reflects its primary production value.
- **Strategy inference:** practical advice derived from the code and Eric's goals.
- **Unknown:** behavior omitted from the repository, hidden in a prompt/rule, or affected by experiments.

Never translate ranking weights into raw engagement-count equivalences, claim that a boost fired, assign a probability of going viral, or imply that coordinated engagement reliably improves ranking.

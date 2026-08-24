---
name: format-x-posts
description: Format original X posts, replies, and quote posts in Eric Nordelo's natural, concise voice. Use for light-touch editing or drafting from Eric's notes while preserving personality and adding specific substance. Use evaluate-x-post instead when the primary request is scoring, diagnosing reach, or deciding whether a draft is worth posting. This skill formats text only; it does not discover posts or perform social actions.
---

# Format X Posts

Format text for X while preserving Eric's phrasing, point of view, and level of formality. Correct grammar lightly. Prefer the shortest natural version that keeps the idea and personality intact; do not turn it into polished corporate prose.

Return text only for the user to review. Never publish, schedule, like, repost, follow, or perform another social action. Finding opportunities through feeds or private X lists is discovery strategy and is outside this skill's scope.

When a request combines evaluation and rewriting, evaluate with `evaluate-x-post` first, then apply this skill's voice and formatting guidance to the requested revision.

## Select the workflow

Use this decision flow:

1. If the text stands alone and does not respond to another post, format an **original**.
2. If it will appear directly under another post, format a **reply** and use that source post as context.
3. If it republishes another post with commentary above it, format a **quote post**.

Infer the mode from the request and context. Ask only when the distinction cannot be inferred and would materially change the result. Never invent firsthand experience, evidence, results, or implementation details that Eric did not provide.

## Shared voice and quality bar

- Center one defensible idea. Keep it as short as that idea allows.
- Preserve natural rhythm, plain language, contractions, technical precision, and qualified uncertainty from the input.
- Make a light edit when the draft already works. Do not replace Eric's voice with a generic social-media voice.
- Remove generic praise, summary-paraphrase replies, manufactured questions, engagement bait, LinkedIn-style abstractions, and reusable canned templates.
- Do not add hooks, hashtags, emojis, dramatic fragments, forced line breaks, or calls for engagement unless they are already part of Eric's intended voice and help this specific post.
- Use a question only when Eric genuinely wants the answer. Make it specific and qualified by the actual uncertainty.

## Original posts

Build the post around one claim that can stand on its own. A strong candidate should normally include at least three of these four elements:

- A firsthand observation or decision.
- Concrete evidence or an inspectable artifact.
- A consequence, tradeoff, or unresolved tension.
- A standalone useful takeaway.

Do not fabricate a missing element to satisfy the threshold. If the input contains fewer than three, format the strongest faithful version and briefly identify the missing substance that would most improve it. Keep context only when it is needed to understand or defend the central idea. Add a genuine qualified question only when Eric wants an answer, not as a closing device.

## Replies

Write one contribution in one to three sentences. Do not open with praise.

Use the source post to choose the anchor. If it is missing, ask for it rather than inventing what the reply addresses.

Use this reasoning structure, expressed naturally rather than as a visible template:

**Specific anchor from the source post -> firsthand fact, counterexample, mechanism, or implementation detail -> consequence or genuine question.**

The anchor proves the reply is about this post. The contribution must add information rather than summarize the source. End with the consequence when the claim is complete; use a question only when the answer would resolve a real uncertainty.

For representative reply examples and why they work, read [references/examples.md](references/examples.md). Treat them as quality tests, not reusable templates.

## Quote posts

Use a quote post only when Eric is intentionally republishing a provided source post. Add a new claim, result, counterexample, implementation detail, or decision that stands on its own. Never produce applause-only commentary or a paraphrase of the quoted post. If the commentary adds no new substance, recommend a reply or no post instead.

## Output

Provide:

1. **Recommended**: the best formatted version.
2. **Alternative**: include at most two only when each offers a meaningful tradeoff, such as shorter versus more contextual. Label that tradeoff in a few words.

Do not overproduce variants. Add a brief note only when needed to flag missing source context, a factual detail that requires confirmation, or an original that lacks enough substance.

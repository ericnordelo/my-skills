---
name: review-doc-framing
description: Review and revise framing in GitHub repository documentation, including READMEs, directory docs, doc comments, and architecture or contribution guides. Use when checking that documentation describes current purpose, behavior, and goals directly, addresses the artifact's users, and avoids obsolete change narration, negative definitions, maintainer-oriented implementation evidence, or colorful verbs that add no technical meaning.
---

# Review Documentation Framing

Review documentation for five framing problems: incremental narration, negative definition, maintainer-oriented language in user-facing docs, indirect headings, and ornamental verb choices. Keep the review focused on how the current repository is presented to its intended users.

## Describe the current state, not the diff

- Treat durable documentation as a description of what exists, what it does, its current purpose, and its goals.
- Remove narration about changes whose earlier state no longer exists. Avoid words such as "now," "new," "previously," "formerly," "no longer," "changed," and "replaces" when they only refer to a past diff.
- Rewrite comparisons with removed behavior as direct statements of current behavior.
- Use repository history to recover intent, not as the framing for current documentation.
- Keep historical narration in artifacts whose purpose is history, such as changelogs, release notes, and migration guides. Mention a transition elsewhere only when the reader must still act on it.

Examples:

- Replace "The client now retries failed requests" with "The client retries failed requests."
- Replace "This option replaces the old polling mode" with a direct explanation of what the option controls and when to use it.

## Define things by what they do

- Lead with the purpose, responsibility, behavior, or objective of the directory, module, API, or workflow.
- Avoid explaining something primarily through what it is not, does not do, or is unrelated to.
- Express boundaries through positive ownership: state what belongs here, where the adjacent responsibility lives, or which behavior the code provides.
- Keep negative wording when a prohibition, unsupported case, or safety constraint is necessary for correct use and positive wording would be less clear.

Examples:

- Replace "This directory is not for deployment scripts" with "This directory contains reusable domain models. Deployment scripts live in `deploy/`."
- Replace "This method does not refresh the token" with "This method returns the cached token for the request lifetime. Call `refreshToken` before reuse after expiry."

## Address users, not reviewers

- Write a repository's main README for people evaluating, adopting, integrating, or operating the project. Write API and doc comments for callers of the code.
- Lead with capabilities, user outcomes, supported workflows, requirements, and observable guarantees.
- Avoid presenting implementation effort as user documentation. Production line counts, test counts, checklist completion, internal milestones, and similar evidence are useful to maintainers and reviewers, but rarely help users understand or use the project.
- Translate internal evidence into the capability or guarantee it supports. Include the implementation metric only when the intended user genuinely needs it.
- Put maintainer-focused evidence in an explicitly maintainer-facing artifact such as a contribution guide, testing guide, design review, release assessment, or engineering report.

Example:

- Replace "800 lines of production code implement all 6 CIP-056 on-ledger interfaces. 36 tests cover transfer lifecycle, allocation/DvP, defragmentation, and 20 security invariants" with "The implementation supports all six CIP-056 on-ledger interfaces, including transfers, allocation and delivery-versus-payment workflows, and defragmentation." Describe relevant security guarantees separately in terms users can rely on.

## Use direct and parallel headings

- Prefer concise noun phrases for concepts, responsibilities, guarantees, risks, and boundaries.
- Prefer direct verb phrases for lifecycle steps and procedures.
- Avoid indirect nominal-clause headings beginning with "What," "Why," "How," or "When" unless the document intentionally follows a consistent FAQ or question-and-answer format.
- Rewrite reader-oriented constructions as direct subject labels: "What Bidders Must Trust" becomes "Bidder Trust Assumptions," "How Settlement Works" becomes "Settlement Lifecycle," and "What Happens on Failure" becomes "Failure Recovery."
- Keep sibling headings grammatically parallel. Do not mix questions, noun phrases, and procedural commands at the same heading level without a content-driven reason.

## You are not a journalist

- Prefer common, literal verbs that an ordinary informed person would use.
- Avoid verbs chosen to make a neutral fact sound vivid, polished, or newsworthy when they add no meaning. If a plain verb communicates the same fact, use the plain verb.
- Watch for newsroom-style substitutions such as "drew" or "garnered" for "got," "boasts" for "has," and "unveiled" for "released" or "introduced." Judge each use in context rather than treating these words as universally forbidden.
- Keep precise technical verbs when they identify a real operation or distinction. Terms such as "serialize," "hash," "allocate," "archive," and "reconcile" should not be simplified when the replacement would lose technical meaning.
- Test the verb by asking: does it make the statement more exact, or only more colorful? Replace it when the answer is only more colorful.

Example:

- Replace "The proposal drew 100 votes" with "The proposal got 100 votes."

## Review workflow

1. Read the relevant code and nearby documentation closely enough to identify the current behavior and purpose.
2. Find statements that depend on knowledge of an obsolete previous state. Rewrite them so they stand alone.
3. Find statements that define a thing by exclusion or negation. Replace them with its positive responsibility or behavior where correctness is preserved.
4. Identify the artifact's intended users. Replace maintainer or reviewer evidence with the capability, workflow, or guarantee those users need.
5. Review the heading hierarchy for direct phrasing and grammatical parallelism.
6. Inspect verbs for ornament rather than meaning. Replace a colorful verb with the common literal verb unless doing so would lose technical precision.
7. Verify that each rewrite remains accurate for the current repository.
8. Keep edits targeted. Do not expand the review into a general documentation rewrite unless another issue prevents the framing from being corrected accurately.

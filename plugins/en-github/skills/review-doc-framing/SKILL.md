---
name: review-doc-framing
description: Review and revise framing in GitHub repository documentation, including READMEs, directory docs, doc comments, and architecture or contribution guides. Use when checking that documentation describes current purpose, behavior, and goals directly, addresses the artifact's users, and avoids obsolete change narration, negative definitions, or maintainer-oriented implementation evidence.
---

# Review Documentation Framing

Review documentation for three framing problems: incremental narration, negative definition, and maintainer-oriented language in user-facing docs. Keep the review focused on how the current repository is presented to its intended users.

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

## Review workflow

1. Read the relevant code and nearby documentation closely enough to identify the current behavior and purpose.
2. Find statements that depend on knowledge of an obsolete previous state. Rewrite them so they stand alone.
3. Find statements that define a thing by exclusion or negation. Replace them with its positive responsibility or behavior where correctness is preserved.
4. Identify the artifact's intended users. Replace maintainer or reviewer evidence with the capability, workflow, or guarantee those users need.
5. Verify that each rewrite remains accurate for the current repository.
6. Keep edits targeted. Do not expand the review into a general documentation rewrite unless another issue prevents the framing from being corrected accurately.

# Eric Nordelo Skills

A marketplace of reusable skills for Codex and Claude Code.

## Available plugins

| Plugin | Skill | Purpose |
| --- | --- | --- |
| `en-canton` | `design-review` | Review Canton design documents for clarity, correctness, security, operability, upgradeability, and future compatibility. |
| `en-github` | `review-doc-framing` | Make repository documentation describe its current purpose and behavior directly for its users. |
| `en-notion` | `lazy-reader-pages` | Turn research, guides, and runbooks into concise Notion pages that expand on demand. |

## Codex

Install:

```bash
codex plugin marketplace add ericnordelo/my-skills
codex plugin add en-canton@ericnordelo-skills
codex plugin add en-github@ericnordelo-skills
codex plugin add en-notion@ericnordelo-skills
```

Use:

```text
Use design-review to review this Canton proposal.
Use review-doc-framing to improve this README.
Use lazy-reader-pages to turn this research into a Notion page.
```

## Claude Code

Install:

```bash
claude plugin marketplace add ericnordelo/my-skills
claude plugin install en-canton@ericnordelo-skills
claude plugin install en-github@ericnordelo-skills
claude plugin install en-notion@ericnordelo-skills
```

Use:

```text
/en-canton:design-review
/en-github:review-doc-framing
/en-notion:lazy-reader-pages
```

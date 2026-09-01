# My Most-Used Skills

A small collection of reusable skills for Codex and Claude Code.

This repository is a marketplace of skills provided through plugins. Each plugin groups skills by domain, such as GitHub, Notion, or Canton, so you can install only what you use.

## Skills

| Domain | Plugin | Skill | Purpose |
| --- | --- | --- | --- |
| GitHub | `en-github` | [`review-doc-framing`](plugins/en-github/skills/review-doc-framing/) | Keeps repository docs current, direct, and user-focused. |
| Notion | `en-notion` | [`lazy-reader-pages`](plugins/en-notion/skills/lazy-reader-pages/) | Creates concise Notion pages for skimmers. |
| Canton | `en-canton` | [`daml-development`](plugins/en-canton/skills/daml-development/) | Develops, reviews, debugs, and tests Daml smart contracts. |
| X | `en-x` | [`format-x-posts`](plugins/en-x/skills/format-x-posts/) | Formats original posts, replies, and quote posts in Eric's natural voice. |
| X | `en-x` | [`evaluate-x-post`](plugins/en-x/skills/evaluate-x-post/) | Scores drafts and explains the highest-impact improvement for qualified reach. |

## Install

Add this marketplace, then install a plugin from the list above. Replace `en-github` with the plugin you want.

```bash
# Codex
codex plugin marketplace add ericnordelo/my-skills
codex plugin add en-github@ericnordelo-skills

# Claude Code
claude plugin marketplace add ericnordelo/my-skills
claude plugin install en-github@ericnordelo-skills
```

## Use

Agents can select an installed skill automatically. To invoke one directly:

```text
# Codex
$en-github:review-doc-framing Review this README.

# Claude Code
/en-github:review-doc-framing Review this README.
```

[MIT License](LICENSE), except the adapted Daml Development material, which is distributed under [Apache-2.0](plugins/en-canton/skills/daml-development/LICENSE).

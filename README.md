# Eric Nordelo Skills

A marketplace of my reusable skills for Codex and Claude Code.

Browse the [available plugins and skills](PLUGINS.md).

## Usage

Install the `en-github` plugin:

```bash
# Codex
codex plugin marketplace add ericnordelo/my-skills
codex plugin add en-github@ericnordelo-skills

# Claude Code
claude plugin marketplace add ericnordelo/my-skills
claude plugin install en-github@ericnordelo-skills
```

Run the skill:

```text
# Codex
Use review-doc-framing to improve this README.

# Claude Code
/en-github:review-doc-framing
```

[MIT License](LICENSE)

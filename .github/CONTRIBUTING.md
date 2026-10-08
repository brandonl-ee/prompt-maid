# Contributing to Prompt Maid

Thanks for helping. Small, focused changes are easiest to review. By taking part you agree to the [Code of Conduct](CODE_OF_CONDUCT.md), and your contributions are licensed under the project's [MIT license](../LICENSE).

## Ways to help

- **A prompt it handled badly.** Open a bug report with the prompt, what came back and what you expected. Remove anything private first.
- **An install step that no longer works.** Platforms change their menus and commands. Open an install problem with the tool, its version and what happened.
- **More test prompts**, especially in other languages. See [tests.md](../docs/tests.md) for the format.
- **Security problems.** Do not open a public issue; follow [SECURITY.md](SECURITY.md).

For anything larger than a fix, open an issue first so we can agree on it before you spend time.

## The one rule that shapes everything

Every line of `skills/prompt-maid/SKILL.md` is paid for, in tokens, each time the skill runs. A change that adds lines has to earn them: say what it fixes and show a prompt where it matters. Changes that make the skill shorter without changing its behaviour are welcome.

## Keeping the pieces in step

- **Skill and fallback behave the same.** If you change a rule in `SKILL.md`, change `fallback.md` to match, and keep it within the character limits the README quotes.
- **Tests match the claims.** If behaviour changes, re-run the affected prompts and update `docs/tests.md` (original, tidied, word counts, meaning check). The README must not claim anything `docs/tests.md` does not show.
- **One name everywhere.** The skill folder, the `name:` in `SKILL.md` and the `name` in both files under `.claude-plugin/` must all be `prompt-maid`. Changing it breaks existing installs.
- **No filled-in profile.** `profile.md` ships blank. Never commit a profile with personal details.
- **No version number in `plugin.json`.** Plugin installs follow commits; a fixed `version` would stop users receiving updates until someone bumped it.

## Checks to run before you open a pull request

CI runs the first one on every push and pull request.

```bash
# The skill follows the open Agent Skills specification
python -m venv .venv
.venv/bin/pip install skills-ref==0.1.1      # Windows: .venv\Scripts\pip
.venv/bin/agentskills validate skills/prompt-maid

# The Claude plugin and marketplace manifests are valid (needs Claude Code)
claude plugin validate .
```

`claude plugin validate .` warns that no `version` is set. That is intended.

For a change to the skill's behaviour, also run the automated checks. They start real sessions, so they use your Claude credits (about a dollar for the whole suite on a large model):

```bash
claude plugin eval . --runs 1 --ablation none --no-publish
```

Each folder under `evals/` is one case: `prompt.md` is the message sent, and each file under `graders/` is one pass or fail check. Add a case when you fix a bug, so it stays fixed. Results vary from run to run; re-run a failure before changing the skill to suit it.

Then try the change for real: install your branch's `skills/prompt-maid` folder where your AI tool looks for skills (the README lists the folders), start a new conversation and send `maid: help` and a rough prompt.

## Pull requests

1. Fork the repository and create a branch from `main`.
2. Make the change, with the checks above passing.
3. Open a pull request and fill in the template. Say what changed and why, and which prompts you tested.

Releases and release notes are kept in [CHANGELOG.md](../CHANGELOG.md).

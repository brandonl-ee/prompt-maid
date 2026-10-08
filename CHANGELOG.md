# Changelog

All notable changes to Prompt Maid are listed here, newest first. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and releases use [semantic versioning](https://semver.org/).

Plugin installs follow the default branch rather than these numbers, so a release is a readable checkpoint, and a tag you can pin with tools such as `gh skill install`. It does not gate updates.

## [Unreleased]

### Added

- `enhance` depth: `maid: enhance` turns the next prompt into a detailed, step-by-step prompt for an AI agent, with every unstated detail listed under Assumptions. It is used only when asked for.
- One-message depth forms: `maid: light: [prompt]`, `maid: full: [prompt]`, `maid: enhance: [prompt]`.
- `maid:` with nothing after it shows help.
- `evals/`: fourteen automated checks for `claude plugin eval`.

### Changed

- Repository tidied: the contributing guide, code of conduct and security policy moved to `.github/`, `tests.md` moved to `docs/`, and the pre-publication `FIX-REPORT.md` was removed.
- The tidied prompt is wrapped at about 80 characters; code, links and quoted text are not broken.
- The full-depth example in the skill no longer shows an invented word limit, which contradicted the rule against inventing limits.
- The skill's description also covers always mode switched on earlier in the conversation.
- Defined behaviour: a missing or unreadable profile is skipped silently; a clarifying question is one question, not a list; a prompt that needs no changes still waits in approve mode; an unrelated message drops a waiting prompt.
- `fallback.md` carries the same changes (1,992 characters; 1,498 with the lines the README lists removed).

### Known limits

- Not reliable on the smallest model tier: 6 to 8 of the 14 checks passed per run on Claude Haiku 4.5, against 14 of 14 on Claude Opus 5.5.

## [1.0.0] - 2026-10-06

First public release.

### Added

- The `prompt-maid` skill in the open Agent Skills format: tidies a rough prompt before it runs, with the `maid:` commands (`on`, `off`, `approve`, `auto`, `light`, `full`, `help`), light and full depth, and pass-through of casual chat, clear prompts and follow-ups.
- An optional, blank `profile.md` with Work and Personal parts.
- `fallback.md`: the same rules as one plain-text block for AIs without skill support.
- Claude plugin and marketplace manifests, so Claude and Claude Code install it straight from this repository.
- `tests.md`: twelve rough prompts (six everyday, six work, two not in English, two passed through) with word counts and a meaning check.
- A CI check that the manifests and the skill's name stay consistent.
- Community files: contributing guide, code of conduct, security policy, issue forms, pull request template and this changelog.

[Unreleased]: https://github.com/brandonl-ee/prompt-maid/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/brandonl-ee/prompt-maid/releases/tag/v1.0.0

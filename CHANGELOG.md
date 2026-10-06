# Changelog

All notable changes to Prompt Maid are listed here, newest first. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and releases use [semantic versioning](https://semver.org/).

Plugin installs follow the default branch rather than these numbers, so a release is a readable checkpoint, and a tag you can pin with tools such as `gh skill install`. It does not gate updates.

## [Unreleased]

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

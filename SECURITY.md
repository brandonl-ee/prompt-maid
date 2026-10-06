# Security policy

## Supported versions

Only the latest commit on the default branch (`main`) is supported. Prompt Maid has no version numbers to pin: a plugin install follows the default branch.

## What counts as a security issue

Prompt Maid is a set of text instructions. It runs no code and calls no services, so the realistic problems are about what the instructions let the AI do. Please report:

- Text pasted after `maid:` that makes the skill ignore its own rules, for example pasted material that gets it to reveal the profile or act on instructions hidden in that material.
- A way to make auto mode run something outside the chat (change files, send a message) without first showing the tidied prompt.
- A command, manifest or workflow in this repository that could harm someone who follows the install steps, for example one that fetches from the wrong place.

A prompt that was tidied badly or lost its meaning is an ordinary bug: please open a [public issue](https://github.com/brandonl-ee/prompt-maid/issues/new/choose) for that.

## How to report

Use GitHub's private reporting: open the **Security** tab of this repository and choose **Report a vulnerability**, or go straight to the [private reporting form](https://github.com/brandonl-ee/prompt-maid/security/advisories/new). Please do not open a public issue for a security problem.

Include the prompt or text that triggered it, the tool and model you used, what happened, and what you expected.

## What to expect

This is a small project with one maintainer, so replies are best effort. Expect an acknowledgement within about a week. If the report is confirmed, the fix goes into the default branch and the advisory credits you unless you prefer otherwise.

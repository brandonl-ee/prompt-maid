# Prompt Maid

[![Check](https://github.com/brandonl-ee/prompt-maid/actions/workflows/check.yml/badge.svg)](https://github.com/brandonl-ee/prompt-maid/actions/workflows/check.yml)
[![License: MIT](https://img.shields.io/github/license/brandonl-ee/prompt-maid)](LICENSE)

**Tidies your prompts. Saves your tokens.**

Start a message with `maid:` and Prompt Maid turns your rough prompt into a clear one before it runs, so you get the answer you meant on the first try, at the length you need. It works for everyday things (messages, trip and meal plans, study questions) and for work (emails, reports, code, data), in whatever language you write in.

**Before** (48 words)

> can u help me write something to my neighbour, their dog has been barking all night every night for like 2 weeks now and i havent slept properly. i dont want to start a fight tho, we usually get on ok. i'll probably put it through their door

**After** `maid:` (44 words)

```text
Write a short, friendly note to my neighbour, to put through their door. Their dog has been barking all night, every night, for about 2 weeks, and I haven't been sleeping properly. I don't want to start a fight; we usually get on ok.
```

Same facts, same request, now a clear instruction. This is test 4 in [tests.md](docs/tests.md), copied as the skill returned it. Across all 12 tests the tidied prompts came out a little longer than the originals (516 words against 468): Prompt Maid cuts the filler, then spends words on saying what shape of answer you need. Whether that makes answers shorter or saves retries hasn't been measured.

## What it does

- Cuts what costs tokens without helping: greetings, filler, repetition.
- Asks for the format and length the task needs, so the answer is no longer than necessary.
- Gives bigger tasks a clear structure: context, task, your constraints, and what the result should look like.
- On request, writes a detailed, step-by-step prompt for an AI agent (`maid: enhance`), with anything it had to assume listed where you can see it.
- Asks one short question when something essential is missing, instead of guessing.
- Says when a lighter or a stronger model would clearly suit the task better. It names a tier, never a specific model, and never switches models for you.
- Works in your language.
- Leaves casual chat, clear prompts and follow-ups such as "make it shorter" alone.

## What it never does

It never changes the meaning. Your names, numbers, dates, quotes and wording stay as you wrote them. It adds no requirements of its own and never invents a goal, audience, tone or constraint. When it has to assume something, it tells you. The `enhance` depth is the one place it adds detail, and every detail you did not give is listed under Assumptions in the prompt.

It also stays plain: no persona, no role-play, no emojis. The name is playful; the replies are fit for work.

It runs no code and calls no services. The skill is one text file of instructions plus an optional profile, and the profile is the only thing it reads.

## Install

Pick your row. When it's in, send `maid: help`.

| Where you use AI | Install |
| --- | --- |
| **Claude** (claude.ai, desktop and phone apps) | In [Customize > Plugins](https://claude.ai/customize/plugins), choose **Add > Add marketplace** and enter `brandonl-ee/prompt-maid`. [Steps](#claude) |
| **Claude Code** | `claude plugin marketplace add brandonl-ee/prompt-maid` then `claude plugin install prompt-maid@prompt-maid`. [Details](#claude-code) |
| **Codex, Cursor, Gemini CLI, Copilot** and 70+ other tools | `npx skills add brandonl-ee/prompt-maid -g`. [Details](#codex-cursor-gemini-cli-copilot-and-other-tools) |
| **ChatGPT, the Gemini app**, anything without skills | Paste the block from [fallback.md](fallback.md) into custom instructions. [Steps](#chatgpt-the-gemini-app-and-other-ais) |

### Claude

1. Open [**Customize > Plugins**](https://claude.ai/customize/plugins) in claude.ai or the Claude desktop app.
2. Choose **Add > Add marketplace**, enter `brandonl-ee/prompt-maid`, and confirm.
3. Open **Prompt Maid** in the plugin list and select **Add**.

Nothing to download. The plugin is saved to your account, so it also works in the phone app, in Cowork, and in Claude Code the next time you start it. Updates come from this repository: use **Check for updates**, or turn on **Sync automatically**. Anthropic's guide: [Plugins](https://claude.com/docs/plugins/overview).

<details>
<summary>No Plugins page on your plan, or you want a profile? Upload it as a skill instead</summary>

1. On this repository's GitHub page, choose **Code > Download ZIP**, then unzip the download.
2. Open the `skills` folder inside it and zip the `prompt-maid` folder: on Windows, right-click it and choose **Compress to ZIP file**; on a Mac, right-click and choose **Compress**. Zip the folder itself, not just the files in it. To include a [profile](#profile), fill in `profile.md` in that folder first.
3. In Claude, go to **Customize > Skills**, click **+**, then **+ Create skill > Upload a skill**, and choose your zip.

If **Skills** isn't showing, turn on **Code execution and file creation** under **Settings > Capabilities** (on Team and Enterprise plans, an owner enables skills under **Organization settings > Plugins & skills**). Anthropic's guide: [Use skills in Claude](https://support.claude.com/en/articles/12512180-use-skills-in-claude).

</details>

### Claude Code

Paste both lines into a terminal. You need `git` installed, which Claude Code uses to fetch the plugin.

```bash
claude plugin marketplace add brandonl-ee/prompt-maid
claude plugin install prompt-maid@prompt-maid
```

Already inside a session? One command does both, on Claude Code 2.1.275 or later:

```text
/plugin install prompt-maid --marketplace brandonl-ee/prompt-maid
```

If you already added Prompt Maid in the Claude app, skip this: it syncs to Claude Code by itself. While idle the plugin adds roughly 150 tokens to a session, and roughly 2,700 when `maid:` is used (estimates; `claude plugin details prompt-maid` shows the figures for your install). Guide: [Install plugins](https://code.claude.com/docs/en/plugins/install).

For a [profile](#profile), copy the `skills/prompt-maid` folder into `~/.claude/skills/` instead, so `profile.md` stays where you can edit it.

### Codex, Cursor, Gemini CLI, Copilot and other tools

One command, using the open-source [`skills`](https://skills.sh) installer. It needs Node.js 22.20 or newer. It finds the AI tools on your machine and asks which to install into; `-g` installs for all your projects.

```bash
npx skills add brandonl-ee/prompt-maid -g
```

No recent Node.js? The GitHub CLI does the same job:

```bash
gh skill install brandonl-ee/prompt-maid prompt-maid --scope user
```

<details>
<summary>Or copy the folder by hand</summary>

Download this repository and copy the `skills/prompt-maid` folder into your tool's skills folder:

| Tool | For all your projects | For one project | Guide |
| --- | --- | --- | --- |
| Codex | `~/.agents/skills/` | `.agents/skills/` | [OpenAI](https://learn.chatgpt.com/docs/build-skills) |
| Gemini CLI | `~/.gemini/skills/` | `.gemini/skills/` | [Gemini CLI](https://geminicli.com/docs/cli/skills/) |
| GitHub Copilot in VS Code | `~/.copilot/skills/` | `.github/skills/` | [VS Code](https://code.visualstudio.com/docs/copilot/customization/agent-skills) |
| Cursor | `~/.cursor/skills/` | `.cursor/skills/` | [Cursor](https://cursor.com/docs/context/skills) |

Gemini CLI, VS Code and Cursor also read `~/.agents/skills/`. For other tools, see the [Agent Skills client list](https://agentskills.io/clients).

</details>

### ChatGPT, the Gemini app and other AIs

These apps don't run skills, so copy the block in [fallback.md](fallback.md) into the app's custom instructions. It has the same commands and rules.

- **ChatGPT:** open **Settings > Personalization**, make sure **Enable customization** is on, and paste the block into **Custom instructions**. On a phone it's **Settings > Customize ChatGPT**. OpenAI's guide: [ChatGPT custom instructions](https://help.openai.com/en/articles/8096356-chatgpt-custom-instructions).
- **Gemini:** at [gemini.google.com](https://gemini.google.com), open the sidebar, choose **Gems > New Gem**, name it Prompt Maid, paste the block as its instructions and click **Save**. Then chat with that Gem. Google's guide: [Use Gems in Gemini Apps](https://support.google.com/gemini/answer/15146780).
- **Anything else:** paste it wherever the app takes custom or system instructions.

Custom instructions are sent with every message, so this version adds a little to every message, even when you don't type `maid:`.

<details>
<summary>On ChatGPT Free or Go? The block needs trimming to fit</summary>

The block is 1,992 characters. That fits ChatGPT's 5,000-character limit on paid plans and a Gemini Gem. ChatGPT Free and Go allow 1,500, so on those plans leave out the `Settings last...` line, the `Light (quick tasks)...` line, the `Enhance (only when asked...` line, the `Plain, polite...` line and the three `MY PROFILE` lines (1,498 characters). Prompt Maid then always picks the depth itself, and has no enhance depth and no profile.

</details>

### Check it works

Send `maid: help`. You should get the command list and your current settings. Then put `maid:` in front of any rough request.

If you get an ordinary answer instead, the skill isn't loaded yet:

- **Claude:** start a new chat, and check that Prompt Maid is switched on under **Customize > Plugins** and that **Code execution and file creation** is on under **Settings > Capabilities**.
- **Claude Code:** run `/reload-plugins`, or start a new session.
- **Other tools:** start a new session so the tool rescans its skills folder.

### Update or remove

| Installed with | Update | Remove |
| --- | --- | --- |
| Claude, Customize > Plugins | **Check for updates** on the marketplace | Open the plugin, then **Remove** from its menu |
| Claude Code | `claude plugin update prompt-maid@prompt-maid` | `claude plugin uninstall prompt-maid@prompt-maid` |
| `npx skills` | `npx skills update prompt-maid -g` | `npx skills remove prompt-maid -g` |
| `gh skill` | `gh skill update prompt-maid` | Delete the `prompt-maid` folder from the tool's skills folder |
| Custom instructions | Paste the new block over the old one | Delete the block |

## Commands

| Type | What happens |
| --- | --- |
| `maid: [your prompt]` | Tidies that prompt. |
| `maid: on` | Always mode: tidies every new request. |
| `maid: off` | On-command mode: tidies only `maid:` prompts. **Default.** |
| `maid: approve` | Shows you the tidied prompt before running it. **Default.** |
| `maid: auto` | Runs the tidied prompt straight away and tells you in one line what changed and what was assumed. |
| `maid: light` | Light tidy for the next prompt only: trim and clarify. |
| `maid: full` | Full tidy for the next prompt only: context, constraints and the finished result. |
| `maid: enhance` | For the next prompt only: a detailed, step-by-step prompt written for an AI agent. |
| `maid: light: [your prompt]`<br>`maid: full: [your prompt]`<br>`maid: enhance: [your prompt]` | The same three depths in one message. |
| `maid: help` | Lists the commands and your current settings. `maid:` on its own does the same. |

- A setting command must be the whole message. `maid: on Friday I need a packing list` is a prompt to tidy, not a setting. Capitals don't matter: `Maid:` works too.
- Without a depth, Prompt Maid picks light or full itself: light for quick questions and small edits, full for multi-step or high-stakes work. It never picks enhance by itself.
- A depth word counts only when it is the whole message or is followed by a colon. `maid: enhance my CV summary` is a prompt to tidy; `maid: enhance: my CV summary` asks for the enhance depth.
- The tidied prompt's lines are broken at about 80 characters, so it reads without sideways scrolling. Code, links and quoted text are left unbroken.
- In approve mode, reply `go` (or any clear yes) to run the tidied prompt, or say what to change. If you send something unrelated instead, the waiting prompt is dropped. The prompt comes in a copyable block, so you can also take it to another AI; if it shows `[pasted text]`, paste your own text in there, since long pasted material isn't repeated.
- Settings last until the end of the conversation. A new conversation starts with the defaults. In a very long conversation the AI can lose track of a setting; send it again if that happens.
- In auto mode, a tidied prompt that would change files, send something or otherwise act outside the chat is still shown first, so you see the instruction before it runs.

### Enhance

`maid: enhance` is for prompts you will hand to an AI agent, where a detailed brief beats a short one.

**Before** (19 words)

> need a script that cleans up our customer csv, theres dupes and the emails are a mess, python pls

**After** `maid: enhance:` (186 words)

```text
Goal: A Python script that cleans up our customer CSV by removing duplicate
rows and tidying the email addresses.

Context: The customer CSV has duplicate entries, and the email addresses are
a mess.

Task:
1. Read the customer CSV.
2. Clean the email column.
3. Remove duplicate customers.
4. Write the cleaned data to a new CSV.

Constraints:
- Python.

Assumptions:
- The input and output file paths are passed as command-line arguments, and
  the original file is left unchanged.
- The CSV has a header row with a column whose name contains "email".
- Cleaning an email means trimming whitespace, lowercasing it, and flagging
  values that aren't valid addresses rather than deleting them.
- Two rows are duplicates if their cleaned emails match; the first one is
  kept.
- Standard library only, no pandas.

Output: The script in one code block, then a short note on how to run it.

Done when: Running the script on the CSV produces a new file with one row per
customer and consistently formatted emails, and it prints how many duplicates
were removed and how many emails were flagged.
```

This is test 13 in [tests.md](docs/tests.md), copied as the skill returned it. It is much longer on purpose, so use it when the extra detail will save the agent from guessing. Read the Assumptions before you run it: they are the skill's guesses, not your requirements.

Prompt Maid was checked on a large model and on the smallest tier. It is not reliable on the smallest tier: see the end of [tests.md](docs/tests.md).

## Profile

The profile is optional and Prompt Maid works fully without it. If you fill it in, Prompt Maid can add the details you would otherwise repeat, such as who you usually write for or how long you like answers. It only adds details that fit the prompt at hand, and never pastes in the whole profile.

There are two parts, **Work** and **Personal**, each with the same four fields:

- **Role or situation**, for example "primary school teacher" or "parent of two, cooking for four".
- **Usual tasks**, for example "parent emails, lesson plans" or "weekly meal plans".
- **Audience**, for example "parents of 7-year-olds".
- **Preferred style and length**, for example "warm, plain English, under 150 words".

Fill in only what helps and leave the rest blank.

- **Skill:** edit `skills/prompt-maid/profile.md` in your own copy, then install that copy as a folder or a zip; each install section above says how. A plugin installed straight from this repository uses the blank profile.
- **Plain text:** fill in the `Work:` and `Personal:` lines at the end of the block. If that pushes the block past your app's limit, keep only the lines you use most.

Your profile is sent to the AI along with your prompts, so leave out anything you wouldn't share with it. If you fork this repository publicly, don't commit your filled-in profile. If you use a copy of this skill that someone else prepared, read its `profile.md` first: whatever is in it goes into your prompts.

## In this repository

| File | What it is |
| --- | --- |
| `skills/prompt-maid/SKILL.md` | The skill. Tuned for Claude; works in other tools that support Agent Skills. |
| `skills/prompt-maid/profile.md` | The blank, optional profile template. |
| `.claude-plugin/` | Two small manifests that let Claude and Claude Code install the skill as a plugin straight from this repository. |
| `fallback.md` | The same rules as one plain-text block, for AIs without skill support. |
| `docs/tests.md` | Twelve rough prompts and what the skill made of them, with word counts and a meaning check for each, plus three enhance tests. |
| `evals/` | Fourteen automated checks for `claude plugin eval`. Never loaded when the skill runs. |
| `CHANGELOG.md` | Release notes. |
| `.github/` | How to contribute, the community rules, the security policy, the issue forms, the pull request template and the CI check. |

Only `skills/prompt-maid` is the skill itself. The manifests are what make the one-line installs work, and the rest is for reading and contributing.

Found a prompt it handled badly, or a platform whose install steps have changed? [Open an issue](https://github.com/brandonl-ee/prompt-maid/issues/new/choose) with the prompt (or the page) and what you expected. Changes are welcome too: see [CONTRIBUTING.md](.github/CONTRIBUTING.md). For a security problem, use the private route in [SECURITY.md](.github/SECURITY.md) instead of a public issue.

## License

[MIT](LICENSE). Use it, change it, share it.

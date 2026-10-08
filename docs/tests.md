# Prompt Maid tests

Twelve rough prompts, six from everyday life and six from work, each run through the skill. Two are not in English, and two should pass through unchanged. Three tests of the `enhance` depth and a note on the automated checks follow at the end.

This file is documentation for people reading the repository. It is not part of the skill folder and is never loaded when the skill runs.

## How the tests were run

- Run on 3 October 2026 in Claude Code 2.1.285 (`claude -p`) with Claude Sonnet 5.5. Each test was a fresh conversation, with the skill installed, the profile left blank and the default settings (on-command, approve).
- Tests 5 and 11 check pass-through: they send `maid: on`, then the message without the prefix.
- Each tidied prompt is copied exactly as the skill returned it. The skill's notes to the user (what changed, assumptions, model advice) are shown underneath. Its closing line, "Reply go to run, or tell me what to change.", is left out.
- Each test is a single run. The same prompt can come out a little differently from one run to the next.
- The test machine's Claude Code session showed a notice about unauthorised connectors, and in a few replies the model repeated it. That text comes from the test environment, not from the skill, and is left out below.
- A word is anything between spaces. The six-line script pasted into test 9 is left out of both counts, because it is passed on unchanged.

## What the word counts show

They measure the prompt only: 468 words before and 516 after across all twelve tests. Of the ten prompts that were tidied, four came out shorter and six longer. Prompt Maid cuts filler but spends words on stating the format and length of the answer, so in these tests the prompts did not get shorter overall. The counts don't show whether answers get shorter or whether fewer retries are needed; neither was measured. Where a tidied prompt is longer than the original, the test says what the extra words are for.

| # | Test | Area | Language | Depth | Before | After |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Four days in Lisbon | Everyday | English | Full | 58 | 83 |
| 2 | Dinner ideas for the week | Everyday | English | Light | 46 | 45 |
| 3 | Explaining moles before a chemistry exam | Everyday | Spanish | Light | 31 | 37 |
| 4 | Note to a neighbour about a barking dog | Everyday | English | Light | 48 | 44 |
| 5 | Casual greeting in always mode | Everyday | English | Passed through | 6 | 6 |
| 6 | Road bike or hybrid? | Everyday | English | Light | 37 | 46 |
| 7 | Late-delivery email to a client | Work | English | Light | 51 | 44 |
| 8 | Q3 update for leadership | Work | English | Light | 59 | 58 |
| 9 | Fixing a Python encoding error | Work | English | Light | 28 | 30 |
| 10 | Finding weak branches in sales data | Work | German | Light | 43 | 54 |
| 11 | Clear translation request in always mode | Work | English | Passed through | 12 | 12 |
| 12 | Team offsite agenda | Work | English | Light | 49 | 57 |

## The tests

### 1. Four days in Lisbon

Everyday · English · Full

<table>
<tr><th width="50%">Original (58 words)</th><th width="50%">Tidied (83 words)</th></tr>
<tr><td valign="top">ok so me and my partner are going to lisbon for 4 days in may, first time there!! we love food and walking but really hate tourist traps and big crowds. can you make us some kind of plan? budget is maybe 150 euros a day for the two of us, not counting the hotel. thanks a lot</td><td valign="top">Context: My partner and I are visiting Lisbon for 4 days in May, our first time there. We love food and walking, and really hate tourist traps and big crowds. Our budget is maybe 150 euros a day for the two of us, not counting the hotel.<br>Task: Make us a plan for the 4 days.<br>Result: A day-by-day plan with food and walking as the focus, avoiding tourist traps and crowds. Keep it as brief as possible while still covering each day.</td></tr>
</table>

Skill's notes to the user: Changed: split into context, task and result, and cut the filler. "Some kind of plan" is now a day-by-day plan. / Assumption: the 150 euros a day covers food and activities for both of you, and you haven't picked a hotel area yet.

**Meaning check:** Same. "Really hate" and "maybe 150 euros" are kept as written; no hotel area or currency is added. The result asks for the briefest plan that covers each day rather than inventing a word count.

**Longer than the original (+25 words).** The extra words are the context / task / result structure and the request for a day-by-day plan kept as brief as possible.

---

### 2. Dinner ideas for the week

Everyday · English · Light

<table>
<tr><th width="50%">Original (46 words)</th><th width="50%">Tidied (45 words)</th></tr>
<tr><td valign="top">I need some dinner ideas for this week, nothing fancy at all, there's 4 of us and my son is allergic to peanuts. on weeknights we only have about 30 mins to cook. also we're trying to eat less meat if possible. thank you so much!</td><td valign="top">Suggest 7 dinner ideas for this week, one per night, one line each. Nothing fancy. There are 4 of us and my son is allergic to peanuts. On weeknights we only have about 30 minutes to cook. We're trying to eat less meat if possible.</td></tr>
</table>

Skill's notes to the user: Changed: removed filler and set a short list format. / Assumption: 7 dinners, one per night. / Model advice: a lighter model tier is enough for this.

**Meaning check:** Same. "Nothing fancy", the peanut allergy, the 30 minutes and "less meat if possible" are kept as written. The one addition, 7 dinners, is stated as an assumption.

---

### 3. Explaining moles before a chemistry exam

Everyday · Spanish · Light

<table>
<tr><th width="50%">Original (31 words)</th><th width="50%">Tidied (37 words)</th></tr>
<tr><td valign="top">hola! el viernes tengo examen de química y no entiendo nada de los moles 😩 me lo puedes explicar de forma sencilla con algún ejemplo? soy de 3º de ESO. gracias!!</td><td valign="top">Explícame de forma sencilla qué son los moles, con algún ejemplo. No entiendo nada del tema; soy de 3º de ESO y tengo examen de química el viernes. Dame la explicación más breve que lo cubra bien.</td></tr>
</table>

Skill's notes to the user: Cambios: quité el relleno y pedí la respuesta más breve que cubra bien el tema.

**Meaning check:** Same. Level, exam day and "con algún ejemplo" are kept; the greeting, emoji and thanks are removed. It asks for the briefest explanation that covers the topic well.

**Longer than the original (+6 words).** The extra words ask for the briefest explanation that still covers the topic.

---

### 4. Note to a neighbour about a barking dog

Everyday · English · Light

<table>
<tr><th width="50%">Original (48 words)</th><th width="50%">Tidied (44 words)</th></tr>
<tr><td valign="top">can u help me write something to my neighbour, their dog has been barking all night every night for like 2 weeks now and i havent slept properly. i dont want to start a fight tho, we usually get on ok. i'll probably put it through their door</td><td valign="top">Write a short, friendly note to my neighbour, to put through their door. Their dog has been barking all night, every night, for about 2 weeks, and I haven't been sleeping properly. I don't want to start a fight; we usually get on ok.</td></tr>
</table>

Skill's notes to the user: Changed: removed filler and set the format (short note, friendly tone).

**Meaning check:** Same. "Get on ok" and "about 2 weeks" are kept; "short, friendly note" comes from "I don't want to start a fight" and "put it through their door".

---

### 5. Casual greeting in always mode

Everyday · English · Passed through

<table>
<tr><th width="50%">Original (6 words)</th><th width="50%">Result (6 words)</th></tr>
<tr><td valign="top">morning! hope your day's going well</td><td valign="top">morning! hope your day's going well</td></tr>
</table>

Passed through unchanged. Reply: "Morning! Doing well, thanks. What can I help you with today?"

**Meaning check:** Passed through as intended: answered normally, with no tidying and no comment.

---

### 6. Road bike or hybrid?

Everyday · English · Light

<table>
<tr><th width="50%">Original (37 words)</th><th width="50%">Tidied (46 words)</th></tr>
<tr><td valign="top">whats better for a beginner, a road bike or a hybrid?? i'd ride maybe 10km to work and back and some weekends, mostly on roads but there's a gravel path on the way. budget is under 600</td><td valign="top">I'm a beginner. Should I get a road bike or a hybrid? I'd ride about 10km to work and back and some weekends, mostly on roads, with a gravel path on the way. My budget is under 600. Give a recommendation and the main reasons, briefly.</td></tr>
</table>

Skill's notes to the user: Changed: removed filler, kept all your details, and asked for a short recommendation with reasons. / Assumption: the budget is the same currency as where you shop, so no currency is added.

**Meaning check:** Same. "10km to work and back", the gravel path and "under 600" are kept; no currency is added. "Briefly" replaces the word cap an earlier version invented.

**Longer than the original (+9 words).** The extra words turn "whats better" into a direct question and ask for a brief recommendation with the main reasons.

---

### 7. Late-delivery email to a client

Work · English · Light

<table>
<tr><th width="50%">Original (51 words)</th><th width="50%">Tidied (44 words)</th></tr>
<tr><td valign="top">pls write an email to the client (Hartwell Logistics) to say the delivery of the 250 units will be late, new date is 14 March. apologise but don't make it grovelling, offer them 5% off their next order. keep it short. oh and mention Priya is their contact for any questions</td><td valign="top">Write a short email to our client Hartwell Logistics: the delivery of the 250 units will be late, and the new date is 14 March. Apologise briefly without grovelling, offer 5% off their next order, and say Priya is their contact for any questions.</td></tr>
</table>

Skill's notes to the user: Changed: removed filler and put the points in a clear order. Nothing else was added.

**Meaning check:** Same. Hartwell Logistics, 250 units, 14 March, 5% and Priya are kept; "keep it short" is now "short". Nothing is added.

---

### 8. Q3 update for leadership

Work · English · Light

<table>
<tr><th width="50%">Original (59 words)</th><th width="50%">Tidied (58 words)</th></tr>
<tr><td valign="top">can you write up something for the leadership meeting tomorrow about Q3? basically revenue was 2.4M which is up 8% on Q2, but margin dropped from 31% to 27% because of the shipping costs, the new supplier deal starts in November which should fix it. they don't like long stuff, and they always ask what we're doing about problems</td><td valign="top">Write a short Q3 update for tomorrow's leadership meeting. Leadership dislikes long documents and always asks what we're doing about problems, so cover the problem and the fix.<br><br>Facts: Q3 revenue was 2.4M, up 8% on Q2. Margin dropped from 31% to 27% because of shipping costs. The new supplier deal starts in November and should fix this.</td></tr>
</table>

Skill's notes to the user: Changed: turned your notes into a task, and kept the figures exactly as you gave them. / Assumption: a short written update, not slides. / A lighter model tier would do equally well here.

**Meaning check:** Same. "2.4M", "8%" and "31% to 27%" are kept exactly, with no currency added. "Cover the problem and the fix" restates "they always ask what we're doing about problems".

---

### 9. Fixing a Python encoding error

Work · English · Light

<table>
<tr><th width="50%">Original (28 words)</th><th width="50%">Tidied (30 words)</th></tr>
<tr><td valign="top">my python script keeps crashing with UnicodeDecodeError when it reads the csv, can you fix it? i don't want to change how it works otherwise. here it is:<br><br>import csv<br>total = 0<br>with open('sales.csv') as f:<br>&nbsp;&nbsp;&nbsp;&nbsp;for row in csv.DictReader(f):<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;total += float(row['amount'])<br>print(total)</td><td valign="top">Fix the UnicodeDecodeError this script raises when reading sales.csv. Change nothing else about how it works. Reply with the corrected script and a one-line note on the fix.<br><br>```python<br>import csv<br>total = 0<br>with open('sales.csv') as f:<br>&nbsp;&nbsp;&nbsp;&nbsp;for row in csv.DictReader(f):<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;total += float(row['amount'])<br>print(total)<br>```</td></tr>
</table>

Skill's notes to the user: Changed: removed filler; kept your "don't change how it works" constraint and set a short reply. / Assumption: the file's encoding is unknown, so the fix may need to pick one explicitly. / Model advice: a lighter model tier would do equally well for this small fix.

**Meaning check:** Same task and the script is passed on unchanged, inside a code fence. One small addition the user did not ask for: "a one-line note on the fix".

**Longer than the original (+2 words).** The extra words set the reply to the corrected script plus a one-line note.

---

### 10. Finding weak branches in sales data

Work · German · Light

<table>
<tr><th width="50%">Original (43 words)</th><th width="50%">Tidied (54 words)</th></tr>
<tr><td valign="top">Ich habe eine Excel-Tabelle mit den monatlichen Umsätzen der letzten 12 Monate für unsere 8 Filialen. Wie finde ich heraus, welche Filialen schwächeln, und welche Diagramme eignen sich für die Präsentation vor der Geschäftsführung? Ich bin kein Excel-Profi, also bitte Schritt für Schritt.</td><td valign="top">Ich habe eine Excel-Tabelle mit den monatlichen Umsätzen der letzten 12 Monate für unsere 8 Filialen. Ich bin kein Excel-Profi.<br><br>1. Erkläre Schritt für Schritt, wie ich herausfinde, welche Filialen schwächeln.<br>2. Nenne, welche Diagramme sich für die Präsentation vor der Geschäftsführung eignen.<br><br>Nummerierte Schritte in einfacher Sprache, so knapp wie möglich, aber vollständig.</td></tr>
</table>

Skill's notes to the user: Geändert: Zwei Fragen als nummerierte Aufgaben getrennt, Füllwörter entfernt, Format ergänzt (aus "Schritt für Schritt" und "kein Excel-Profi").

**Meaning check:** Same. The two questions become two numbered tasks; "Schritt für Schritt" and "kein Excel-Profi" become the format line (numbered steps, simple language, as brief as possible but complete).

**Longer than the original (+11 words).** The extra words are the numbered structure and the format line.

---

### 11. Clear translation request in always mode

Work · English · Passed through

<table>
<tr><th width="50%">Original (12 words)</th><th width="50%">Result (12 words)</th></tr>
<tr><td valign="top">Translate into French: "The meeting has moved to 3 pm on Friday."</td><td valign="top">Translate into French: "The meeting has moved to 3 pm on Friday."</td></tr>
</table>

Passed through unchanged. Reply: "« La réunion a été déplacée à 15 h vendredi. »"

**Meaning check:** Passed through as intended: the prompt was already clear, so it was answered directly with no comment.

---

### 12. Team offsite agenda

Work · English · Light

<table>
<tr><th width="50%">Original (49 words)</th><th width="50%">Tidied (57 words)</th></tr>
<tr><td valign="top">can you help me plan the agenda for our team offsite? it's a full day, 9 to 5, 12 people. we want to look back at last year, set goals for next year and do some team building. lunch is 12-1. we've got a meeting room and the garden</td><td valign="top">Plan the agenda for our team offsite. It's a full day, 9 to 5, for 12 people, with lunch 12-1. We want to look back at last year, set goals for next year and do some team building. We have a meeting room and the garden. Give a time-slotted agenda that says which space each session uses.</td></tr>
</table>

Skill's notes to the user: Changed: tightened the wording and asked for a timed agenda that names the space for each session, since you mentioned both spaces.

**Meaning check:** Same. "9 to 5", "12 people", "lunch 12-1", both spaces and all three goals are kept as written.

**Longer than the original (+8 words).** The extra words ask for a time-slotted agenda that names the space for each session.

## Enhance tests

Added on 8 October 2026 for the `enhance` depth. Run with `claude plugin eval` in Claude Code 2.1.285 on Claude Opus 5.5, each a fresh, isolated session with only this plugin loaded and a blank profile. Each is a single run, copied as returned. Enhance is meant to produce a longer, more detailed prompt, so these counts are kept out of the totals above.

The twelve tests above were run on 3 October 2026 with the previous version of the skill and have not been re-run. Since then the prompt block is wrapped at about 80 characters, so the same prompts now come back with line breaks.

| # | Test | How it was asked | Before | After |
| --- | --- | --- | --- | --- |
| 13 | Script to clean a customer CSV | `maid: enhance: [prompt]` | 19 | 186 |
| 14 | Website for a dog walking business | `maid: enhance`, then the prompt | 16 | 175 |
| 15 | Email with nothing to go on | `maid: write the email...` | 10 | question asked |

### 13. Script to clean a customer CSV

Work · English · Enhance, in one message

Original (19 words): `maid: enhance: need a script that cleans up our customer csv, theres dupes and the emails are a mess, python pls`

Enhanced (186 words):

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

Notes from the skill: "Changed: expanded into an agent-ready prompt with steps, output and a "done when" check." "Assumption: duplicates are matched on email, and "a mess" means stray spaces, mixed case and invalid addresses. Change these if your data is different."

Meaning check: same request (a Python script, remove duplicates, fix the emails). Everything the user did not say is under Assumptions, including "standard library only", which a user who wanted pandas would need to change.

### 14. Website for a dog walking business

Everyday · English · Enhance, set with `maid: enhance` and sent as the next message without the prefix

Original (16 words): `make me a little website for my dog walking business, needs prices and a contact form`

Enhanced (175 words):

```text
Goal: Build a small website for my dog walking business.

Task:
1. Create a simple static site (HTML and CSS) in the current working
   directory.
2. Include a prices section.
3. Include a contact form.
4. Tell me how to open the site and what I need to fill in.

Constraints:
- Keep it little: one page with the sections above, and nothing else.

Assumptions:
- The business name, prices and contact details are placeholders that are
  clearly marked so I can replace them.
- Contact form fields: name, email, phone, message.
- There is no backend, so the form sends through a placeholder form-service
  URL (for example Formspree) that I replace with my own. Add a comment that
  explains how.
- Plain HTML and CSS with no build step. The page works on mobile.

Output: The site files, then a short note listing the placeholders to replace
and how to view the page.

Done when: The page opens in a browser, shows the prices and the contact form,
and every placeholder is clearly marked.
```

Notes from the skill: "Changed: expanded into a detailed agent prompt with steps, output and a finish check." "Assumption: the prices and business details aren't given, so they're placeholders. Send them now if you'd like them included."

Meaning check: same request (a small site with prices and a contact form). The form fields, the form service and the technology are assumptions and are labelled as such. An earlier run put invented form fields in the Task section; the rule was tightened and this is the re-run.

### 15. Email with nothing to go on

Everyday · English · asks first

Original (10 words): `maid: write the email to her about the thing we discussed`

Reply: the skill did not write a prompt. It said it had no earlier conversation to draw on and asked who the email is to and what it should say, with an example answer.

Meaning check: nothing was invented. The rule is one short question; this run asked one question with two parts.

## Automated checks

`evals/` holds fourteen cases that `claude plugin eval .` runs and scores: the commands, each depth, a prompt that only looks like a setting, a missing-detail prompt, pasted text with an embedded instruction, a Spanish prompt, line wrapping, and two messages that must not load the skill. On 8 October 2026 all fourteen passed on Claude Opus 5.5 (one run each, twice). On Claude Haiku 4.5 between six and eight of the fourteen passed per run, with different cases failing each time: it sometimes asked several questions, treated `maid: on Friday...` as a setting, changed a detail, or did not load the skill. Prompt Maid is not reliable on the smallest model tier.

---
name: bug-report
description: Turn rough testing notes, logs or screenshots into a clear bug report. Use when the user asks to write, clean up or format a bug report, defect or issue from their notes.
---

# Bug report

Write a report that a developer can reproduce on the first try without asking the tester anything.

## The one rule

**Only write what the tester observed.** The notes are the source. If something needed for the report is missing, such as the build, the account or the exact input, list it under "Open questions" instead of filling it in. Never invent a step, a value or an error message.

## Format

```
Title: [what is wrong, where, under which condition]

Severity: [proposed, with one line of reasoning]
Environment: [URL or build, browser or device, account or role, date]

Steps
1. ...
2. ...

Expected
[what should happen, and where that expectation comes from]

Actual
[what happened, in the words on the screen where possible]

Impact
[who is affected and what they cannot do]

Evidence
[screenshots, logs, request and response, video]

Open questions
[anything the notes did not say]
```

## How to write each part

- **Title**: a sentence someone can find later by searching. "Order can be placed with an empty cart", not "Checkout bug".
- **Steps**: numbered, one action each, starting from a known state such as "logged in as a standard user with an empty cart". Include the exact data typed. Remove steps that are not needed to reproduce.
- **Expected**: name the source: a requirement, a design, the same feature elsewhere in the product, or common practice. If there is no source, say the expectation is the tester's judgement.
- **Actual**: quote messages exactly. Include what did not happen, for example "no error message is shown".
- **Severity**: propose one and give the reason. The tester decides. Use the project's scale if the user gives one; otherwise Critical (cannot complete a main task, or data is wrong), Major (a main function gives a wrong result), Minor (wrong but easy to work around).
- **Impact**: write for a product owner. One or two sentences.

## Checks before returning the report

- Could someone who has never seen the feature follow the steps?
- Is there exactly one problem in the report? If the notes describe two, write two reports.
- Does the report contain passwords, tokens or personal data? Remove them and say that you did.
- Is every statement traceable to the notes? If not, move it to open questions.

---
name: test-charter
description: Write exploratory test charters for a feature. Use when the user asks for test charters, an exploratory testing plan, test ideas, or "what should I test" for a feature, user story or change.
---

# Test charter

Turn a feature description into a small set of exploratory test charters that a tester can pick up and run.

## Before writing

Read what the user gave you and identify:

- **Who uses the feature** and what they are trying to get done.
- **What can go wrong that would matter**: lost data, wrong money, blocked users, security, misleading information.
- **What changed**, if this is a change to an existing feature. New code is where the risk is.

If the description does not say what the feature is for or who uses it, ask one question before continuing. Do not invent requirements.

## Write the charters

Write three to five charters. Each one follows this form:

> Explore **[area]** with **[resources, data or technique]** to discover **[the information we want]**.

Rules:

- One risk per charter. If a charter has "and" in the area, split it.
- Order them by risk, highest first, and say in one line why that order.
- Each charter fits in one session of 30 to 60 minutes.
- Name concrete data or techniques: boundary values, interrupted flows, two tabs, a slow network, another role. "Various inputs" is not a technique.
- Include at least one charter about state: reload, back button, session expiry, concurrent edits.
- Do not write step by step test cases. A charter gives direction, the tester chooses the steps.

## For each charter, add

- **Why it matters**: one sentence that ties it to a user or business risk.
- **Starting ideas**: three to six specific things to try first.
- **Stop when**: what tells the tester the charter is done, besides the clock.

## End with the notes template

```
Charter:
Tester:            Date:            Build or environment:

What I tried

What I found
- Bugs:
- Questions:
- Surprises:

What I did not get to

Coverage: enough / needs another session
```

## Do not

- Do not claim anything about how the feature behaves. You have not tested it.
- Do not assign severity to imagined bugs.
- Do not pad the list. Three good charters are better than five thin ones.

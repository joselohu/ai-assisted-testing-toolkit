# AI-Assisted Testing Toolkit

Three Claude skills and a browser automation setup that I use to speed up the parts of testing that are mostly writing, while keeping the judgement with the tester.

| Skill | Input | Output |
|---|---|---|
| [`test-charter`](skills/test-charter/SKILL.md) | A feature description or user story | Risk based exploratory charters with a notes template |
| [`bug-report`](skills/bug-report/SKILL.md) | Rough notes, logs or a screenshot | A bug report a developer can reproduce without asking questions |
| [`playwright-test-review`](skills/playwright-test-review/SKILL.md) | A Playwright test file | A review for flakiness, weak assertions and missing cleanup |

The repository also contains an [MCP configuration](.mcp.json) for the Playwright MCP server, which lets Claude drive a real browser, and a description of the [workflow](docs/workflow.md) that ties the pieces together.

## Install

Claude Code loads skills from a `.claude/skills` folder. To use these in a project:

```bash
git clone https://github.com/joselohu/ai-assisted-testing-toolkit
cp -r ai-assisted-testing-toolkit/skills/* your-project/.claude/skills/
cp ai-assisted-testing-toolkit/.mcp.json your-project/.mcp.json   # optional, browser automation
```

Then ask in plain language, for example "write test charters for the checkout feature" or "turn these notes into a bug report".

## Examples

Each example shows an input and the result the skill is designed to produce, using material from my other portfolio repositories.

| Example | What it shows |
|---|---|
| [Charter](examples/01-charter.md) | One sentence about a feature becomes three charters |
| [Bug report](examples/02-bug-report.md) | Four lines of notes become a complete report |
| [Test review](examples/03-test-review.md) | A test that passed on two browsers and failed on the third, and why |

## Rules I work by

AI output in testing is a draft. These rules are part of the skills, and I apply them by hand as well.

1. **Nothing is reported that was not observed.** A bug report only contains steps that were run and results that were seen. If the model fills a gap with a guess, the guess is marked as an open question.
2. **Expected results come from a source.** A requirement, a design, or the behaviour of a comparable feature. "The model thinks it should" is not a source.
3. **Generated tests are read line by line before they are committed.** A test that passes proves little. The review asks what would make it fail.
4. **No real data in prompts.** No customer data, credentials or production logs. Examples use public demo applications.
5. **The tester decides severity and priority.** The model can propose, the person who knows the product decides.

## Limits

These skills do not replace exploratory testing. They make the paperwork around it faster. A charter is a starting direction, and the useful findings usually come from what the tester notices on the way.

# Contribution: fix: use consistent error formatting across all commands

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Jingyi He
**GitHub Username:** jing2003
**Issue:** https://github.com/Raftersecurity/rafter-cli/issues/34
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built and evaluated an issue-scout for open-source contribution selection**

I upgraded my issue-select skill into issue-scout, added a personalized fit profile, and created three GitHub search queries for JavaScript, TypeScript, and Python with metadata-based ranking filters. My first scan discovered 300 issues and graded five candidates, while manual grading helped me narrow my choices to Rafter CLI #34 and Kaoto #3527. The process revealed limitations in my search strategy, including a preference for recently updated issues with zero comments, and manual review uncovered issues that already had active pull requests despite being open and unassigned. I documented these findings in `scan-notes.md` and kept my existing rubric unchanged for Unit 5, leaving further scope improvements for Unit 6.

**Unit 6: [one line on the tool work]**

[2-4 sentences: the voice-guard, the repo-memory file. What broke or
fell short, and what changed because of it. "Nothing broke" counts when
it is true - say how you know.]

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

In Unit 5, I upgraded my issue-select skill into issue-scout and used it to search GitHub for contribution opportunities that matched my JavaScript, TypeScript, and Python experience. My first scan discovered 300 unique issues and graded five candidates. After manually reviewing additional issues, I narrowed my choices to Rafter CLI #34 and Kaoto #3527. My scout accepted Rafter CLI #34 because it describes a concrete error-formatting inconsistency and provides a grep command to locate the affected code. I chose this issue because it aligns with my technical background and gives me an opportunity to gain experience working in an unfamiliar open-source codebase, understanding existing conventions, and maintaining consistency between TypeScript and Python implementations.

The selection process also revealed weaknesses in my scout. Its ranking favored recently updated issues with no comments, and some open, unassigned issues already had related pull requests that the initial ranking could not detect. In Unit 6, I replaced the restrictive `newcomer-scope` check with `scope-feasible` and added difficulty classifications. Rafter CLI remained accepted with moderate difficulty, while Kaoto and VueTorrent were classified as ambitious. Rafter CLI remained my preferred choice because its starting point is clearer, although the number of affected files and the dual-implementation requirement make it more challenging than a simple replacement. I documented the scout's limitations and verified that the upstream issue was available before posting my claim.

**Claim comment:** https://github.com/Raftersecurity/rafter-cli/issues/34#issuecomment-6436006358

**Toolkit**

- **Tool:** issue-scout, using my personalized fit profile, GitHub search strategy, and grading rubric to discover and evaluate contribution candidates.
- **What it produced:** A scan of 300 unique issues, five initial candidate evaluations, and additional manual grading. Rafter CLI #34 was accepted under both the original and updated rubrics.
- **Difficulties:** The initial ranking favored recently updated, zero-comment issues and could not reliably detect competing pull requests from search metadata alone. The original scope check was also too restrictive toward issues with unresolved design questions.
- **What changed:** I documented these limitations in `scan-notes.md`, replaced `newcomer-scope` with `scope-feasible`, added difficulty notes, and regraded my shortlisted issues before finalizing my selection.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]

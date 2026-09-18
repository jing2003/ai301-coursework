# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/55

**Verdict output**

Candidate is in the scoped repo (codepath/pathreview-ai301-fa26-s1). Graded live against today's date, 2026-09-18.

- maintainer-active — pass. Newest default-branch commit 2026-09-16 by non-bot Aburke225, 2 days old.
- repo-in-use — pass. Not archived; last push 2026-09-16, well inside 180 days.
- newcomer-scope — pass. One named function (\_detect_languages in ingestion/parsers/skill_extractor.py), an exact reproduction command, and five named xfailed tests as the acceptance oracle.
- unclaimed — pass. No assignee, no linked or mentioned PR (the repo has zero PRs in any state), no comments. The house rule on classmate claims doesn't need to fire.
- contribution-policy — pass. docs/CONTRIBUTING.md requires green CI, passing tests, and removal of the @pytest.mark.xfail marker as part of the fix — conditions, not an AI ban.

Accepted, and a good fit for you: a Python bug with a single-command local repro and failing tests that tell you exactly when you're done, which is the debugging practice you said you wanted. Note the CONTRIBUTING requirement that your PR both fix the bug and delete the xfail markers from all five tests — CI fails with XPASS(strict) if you leave them in.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/55",
  "checks": [
    {
      "name": "maintainer-active",
      "grade": "pass",
      "evidence": "Newest default-branch commit 2026-09-16T21:42:18Z by non-bot Aburke225, 2 days before capture date 2026-09-18 (within 90 days)."
    },
    {
      "name": "repo-in-use",
      "grade": "pass",
      "evidence": "archived:false; pushedAt 2026-09-16T21:48:27Z, 2 days before capture (within 180 days)."
    },
    {
      "name": "newcomer-scope",
      "grade": "pass",
      "evidence": "Finite bug in one named function `_detect_languages` (ingestion/parsers/skill_extractor.py) with repro `pytest tests/unit/test_skill_extractor.py -q` and five named failing tests; not an umbrella issue, not a support question, no unresolved design debate."
    },
    {
      "name": "unclaimed",
      "grade": "pass",
      "evidence": "assignees: 0; no cross-referenced or connected PRs in the timeline; repo has 0 PRs in any state; 0 comments."
    },
    {
      "name": "contribution-policy",
      "grade": "pass",
      "evidence": "docs/CONTRIBUTING.md sets CI/testing/xfail-removal conditions but states no AI ban; no AI_POLICY file in the repo."
    }
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. `agreement: 0/1 scored items`
   `2 item(s) errored; fix and re-run.`
2. `agreement: 2/3 scored items`
3. `agreement: 1/1 scored items`
4. `agreement: 18/20 scored items  (bar: 18/20: PASS)`
5. `agreement: 18/20 scored items  (bar: 18/20: PASS)`

**Issue analysis**

`issue-15  reject  accept   NO     graded accept`

My rubric decided `accept`, while the gold label was `reject`. The required checks did not reject the issue because the repository was active, AI-assisted contributions were allowed, there was no current assignee or open linked PR, and the issue still described a concrete behavior change. The weakness was in my `newcomer-scope` check. Although it tells the grader to fail unresolved design debate, it does not give a concrete threshold for a very long issue history or multiple abandoned attempts. As a result, the rubric treated the issue as a bounded feature rather than recognizing the years of discussion and failed attempts as evidence that the work was more difficult than it first appeared.

**Check rationale**

> `| newcomer-scope | Issue body and comment thread, including linked or mentioned prior PR attempts | Pass if the issue describes a finite, concrete deliverable or one cohesive set of related edits with enough direction to start. Multiple files or subtasks may still pass when they serve one stated goal. Fail if the issue is explicitly an umbrella or tracking issue meant to be split into separate work, is a pure support question, has unresolved design or product debate with no settled direction, or a maintainer states that the fix requires core-internal changes unsuitable for a newcomer. | required |`

I chose this wording after the initial smoke run rejected `issue-01` on `newcomer-scope`. My original wording required "one bounded change," which was too narrow because a well-scoped contribution can involve several related files while still producing one cohesive result. I changed the check to focus on whether there is a finite, concrete deliverable with enough direction to start, while still rejecting umbrella issues, support questions, unresolved design discussions, and work that maintainers identify as requiring unsuitable core-internal changes.

**Trade-offs**

The broader `newcomer-scope` wording gives up the simplicity of requiring a single small change. It can accept work that spans multiple files or subtasks when they contribute to one goal, which means some accepted issues may still be larger than I personally want for a first contribution.

The canary I used was `issue-01`. Before the revision, the smoke run reported:

`issue-01  accept  reject   NO     failed: newcomer-scope`

After changing the check, I reran only that issue and got:

`issue-01  accept  accept   yes`

`agreement: 1/1 scored items`

---

## Selection rationale

**Selection rationale**

1. Issue #55 fits what I want to practice because it is an actual debugging task rather than only a documentation change. I have experience with JavaScript/TypeScript and some Python, and I want to improve my ability to understand an unfamiliar codebase, reproduce a bug, use tests to guide the fix, and verify that my change works. It is also labeled tier-1 and already provides one test command and five failing tests, so the scope feels reasonable for the time I have.

2. The verdict correctly identified that the repository is active, the issue is unclaimed, the contribution policy does not block AI-assisted work, and the problem has a clear local reproduction path. Outside of the rubric, I also compared it with the other accepted issues. Issue #37 looked lower risk but was mostly documentation work, while issue #39 was closer to my React/TypeScript experience but was a tier-3 issue estimated at 5–8 hours and touched both the frontend and backend. I chose #55 because it gives me more debugging practice without taking on the larger scope of #39.

3. I expect claiming the issue to be relatively straightforward because it currently has no assignee, linked PR, or comments. Since this is the Path Review classroom repository, another student claiming the same issue would not block me under the course house rule. The main thing I need to be careful about is following the Unit 2 claiming procedure correctly before I start working on it.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.

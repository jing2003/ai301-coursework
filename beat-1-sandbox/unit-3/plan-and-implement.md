# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

jing2003

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/55#issuecomment-5973264613

I reproduced all five issue-#55 failures and traced them to detection patterns that do not cover the inputs exercised by the tests.

For JavaScript/TypeScript, `_detect_languages()` currently relies on filename hints, `package.json`, or an `import`/`require` regex that requires whitespace after the keyword. That misses the test's `require('fs')` call and its TypeScript `export interface` syntax. The PostgreSQL test uses `psycopg2`, while database detection currently looks for the literal database name, and the Docker tests use Dockerfile/Compose structure without the literal word `docker`.

My plan is to make targeted changes in `ingestion/parsers/skill_extractor.py` to recognize those existing test patterns without broadly rewriting the extractor: support `require(...)` and a specific TypeScript syntax signal, treat `psycopg2` as PostgreSQL evidence, and add bounded Dockerfile/Compose structural signals. I will keep the current detection/output model and avoid unrelated detector changes.

I will verify the change first with the same reproduction command, `pytest tests/unit/test_skill_extractor.py -q --runxfail`, expecting the five underlying failures to become passes. Once they do, I will remove the five issue-#55 `xfail` markers and run the test file normally, expecting all 18 tests to pass.

The main risk I will watch for is false positives from patterns that are too broad, so I will prefer specific syntax or combinations of indicators over isolated generic keywords.

---

## Your branch

**Branch**

`fix/55-skill-extractor-detection`

**Evidence**

Before the fix, I ran the Unit 2 reproduction command:

```bash
.venv/Scripts/pytest tests/unit/test_skill_extractor.py -q --runxfail
```

The output showed the five issue-#55 assertions failing:

```text
5 failed, 13 passed in 0.71s
```

The failures were:

```text
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_text_with_typescript_files
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_database_technology_detection
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_devops_tool_detection
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_javascript_detection
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_docker_compose_detection
```

After building the change, I re-ran the same reproduction command:

```bash
.venv/Scripts/pytest tests/unit/test_skill_extractor.py -q --runxfail
```

```text
..................                                                                   [100%]
18 passed in 0.19s
```

After removing the five issue-#55 `xfail` markers, I also ran the test file normally:

```bash
.venv/Scripts/pytest tests/unit/test_skill_extractor.py -q
```

```text
..................                                                                   [100%]
18 passed in 0.15s
```

The full unit suite also completed with:

```text
380 passed, 48 xfailed, 2 warnings in 36.92s
```

---

## Eval iterations

**Run history**

- **Run 1 — full eval:** `agreement: 19/20 scored items  (bar: 18/20: PASS)`. The only disagreement was `pkg-14`, where the gold verdict was `accept` and my rubric returned `reject` because `uncertainty-honesty` failed.
- **Run 2 — targeted rerun:** `agreement: 4/5 scored items`. I reran `pkg-14` with `pkg-01`, `pkg-04`, `pkg-06`, and `pkg-10` as canaries after revising the uncertainty wording. The four canaries still matched, but `pkg-14` still rejected.
- **Run 3 — targeted rerun:** `agreement: 5/5 scored items`. After separating honesty about uncertainty from whether an unresolved detail blocks execution, `pkg-14` changed to `accept` while all four canaries remained correct.
- **Run 4 — final full eval:** `agreement: 20/20 scored items  (bar: 18/20: PASS)`. All category floors passed: clear-accept `7/7`, scope-creep `4/4`, thread-convention `2/2`, unbuildable `3/3`, and wrong-cause `4/4`.

One targeted invocation was interrupted before it produced any package verdicts or agreement score, so it is not listed above as a scored run.

**Package analysis**

I analyzed `pkg-14`.

In my first full run, the result was:

```text
pkg-14  clear-accept       accept  reject   NO     failed: uncertainty-honesty
```

The gold label was **accept**, while my rubric returned **reject**.

The package was explicit about what was still unknown. For example, its plan said:

> “exact functions to be pinned in the PR after tracing the query issuance with debug logs”

and:

> “I cannot test the Windows session-switch variant reported here”

My original `uncertainty-honesty` check was doing two jobs at once. It asked whether the author represented unknowns honestly, but it also treated unresolved implementation details as a reason the plan might not be safe to start. That second question was already covered by my separate `execution-ready` check.

Because of that overlap, the rubric rejected a plan that was actually transparent about its uncertainty and still provided a concrete way to proceed.

I revised `uncertainty-honesty` so it judges whether claims are stated with a level of certainty supported by the evidence and whether material unknowns are identified honestly. Whether an unknown prevents implementation from starting is handled by `execution-ready`.

After the revision, the targeted rerun reported:

```text
pkg-14  clear-accept       accept  accept   yes
```

and the final full run also accepted `pkg-14`.

**Check rationale**

I chose the `uncertainty-honesty` check. Its final rubric row is:

> `| uncertainty-honesty | The plan's diagnosis, risks, unknowns, and implementation claims read against the evidence available in the package. | Pass when claims are stated with a level of certainty supported by the available evidence, and material assumptions, risks, or unresolved details are identified as uncertain rather than presented as established facts. | required |`

I revised this check after the first full run rejected `pkg-14`. The earlier version effectively mixed two different questions: whether the author was honest about uncertainty and whether an unresolved detail made the plan impossible to execute.

`pkg-14` showed why those should be separate. It openly stated that the exact functions still needed to be pinned down and that the author could not test the Windows variant, but it also gave a concrete tracing method, a bounded Unix scope, and a specific implementation direction.

I therefore changed `uncertainty-honesty` to judge only whether the plan distinguishes supported claims from assumptions or unresolved details. I left the question of whether those unknowns prevent someone from beginning the work to the separate `execution-ready` check.

**Trade-offs**

The revised `uncertainty-honesty` check is more permissive about plans that still contain unresolved implementation details. A plan can now pass this check when an exact function, regex, platform variant, or other detail is not yet settled, as long as that uncertainty is represented honestly.

The trade-off is that this check by itself no longer rejects a plan merely because an important implementation detail is unresolved. That responsibility is intentionally left to `execution-ready`, which asks whether another developer can actually begin the work without inventing the missing core approach.

I checked that the revision did not broadly loosen the rubric by rerunning `pkg-14` with four already-correct canaries from other failure categories:

```text
pkg-01  wrong-cause        reject  reject   yes
pkg-04  thread-convention  reject  reject   yes
pkg-06  scope-creep        reject  reject   yes
pkg-10  unbuildable        reject  reject   yes
pkg-14  clear-accept       accept  accept   yes

agreement: 5/5 scored items
```

That changed the intended `pkg-14` result from reject to accept while the wrong-cause, thread-convention, scope-creep, and unbuildable canaries remained rejected.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.

# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

jing2003

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/55#issuecomment-5841477743

Hi, I'd like to investigate this issue. I'll attempt to reproduce the reported JavaScript and TypeScript language-detection behavior in the skill extractor, review the related failing tests, and report back with my environment, reproduction steps, and observed results.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/55#issuecomment-5842192565

I reproduced the reported skill-extractor detection failures on my local environment.

**Environment**

- Microsoft Windows [Version 10.0.26200.9457]
- Git Bash
- PathReview commit: `f89c06f`
- Python: 3.14.6
- pytest: 9.1.1

**Reproduction**

From the repository root, I first ran the test file referenced in the issue:

```bash
.venv/Scripts/pytest tests/unit/test_skill_extractor.py -q -rx
```

Result:

```text
13 passed, 5 xfailed in 2.72s
```

The five xfailed tests were:

```text
test_text_with_typescript_files
test_database_technology_detection
test_devops_tool_detection
test_javascript_detection
test_docker_compose_detection
```

All five are marked with:

```text
issue #55: skill extractor does not detect JavaScript/TypeScript
```

To expose the assertion failures underneath the `xfail` markers without modifying the tests, I then ran:

```bash
.venv/Scripts/pytest tests/unit/test_skill_extractor.py -q --runxfail
```

Result:

```text
5 failed, 13 passed in 0.71s
```

For example, `test_javascript_detection` failed on its JavaScript detection assertion:

```text
>       assert any("javascript" in s.lower() or "js" in s.lower() for s in skill_names)
E       assert False
E        +  where False = any(<generator object ...>)

tests\unit\test_skill_extractor.py:195: AssertionError
```

The observed failures were:

- `test_text_with_typescript_files`: expected TypeScript to appear in the detected skill names, but the assertion was false.
- `test_database_technology_detection`: expected PostgreSQL or SQL to be detected from the `psycopg2` example, but the assertion was false.
- `test_devops_tool_detection`: expected Docker to be detected from the Dockerfile-style input, but the assertion was false.
- `test_javascript_detection`: expected JavaScript or JS to be detected from the `require('fs')` example, but the assertion was false.
- `test_docker_compose_detection`: expected Docker to be detected from the Docker Compose YAML, but the assertion was false.

This matches the behavior described in Issue #55: the skill extractor does not recognize these technologies from the provided text patterns in these tests.

I did not modify `skill_extractor.py` or remove any of the `xfail` markers while reproducing the issue.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

- **Run 1 — full eval:** `18/20 scored items`. The two disagreements were `pkg-09` and `pkg-20`. The run also missed the disclosure category floor (`0/1`), so it was below the required bar even though the raw agreement score was 18/20.
- **Run 2 — targeted rerun:** `2/2 scored items`. I reran `pkg-09` and `pkg-20` after revising the rubric, and included `calib-02` as a canary. `pkg-09` changed to accept, `pkg-20` changed to reject, and `calib-02` remained reject.
- **Run 3 — final full eval:** `20/20 scored items (bar: 18/20: PASS)`. All category floors passed: clear-accept `8/8`, disclosure `1/1`, no-evidence `4/4`, unfollowable-comms `3/3`, and wrong-target `4/4`. This is the run saved in `eval-run.txt`.

**Package analysis**

I analyzed `pkg-20`.

In my first full eval run, my rubric decided **accept**, while the gold label was **reject**.

The package had strong reproduction evidence, so most of my checks passed. The problem was `repo-conventions`. The repo facts explicitly stated:

> “All AI usage in any form must be disclosed, stating the tool used and the extent of the assistance”

They also stated that:

> “AI-assisted issues and comments must be reviewed and edited by a human before submission”

However, the candidate claim and reproduction comments did not include an AI-assistance disclosure.

My original `repo-conventions` check was too general. It asked whether the comments followed repository requirements, but it did not state clearly enough that a missing required AI-use disclosure must cause that check to fail. Because of that ambiguity, the rubric accepted the package even though it violated a stated repository policy.

I revised the check so that if a repository explicitly requires AI-assistance disclosure for comments, the candidate comments must contain that disclosure; otherwise `repo-conventions` fails.

After the revision, I reran `pkg-20`, and my rubric changed from **accept** to **reject**, matching the gold label.

**Check rationale**

I chose the `repo-conventions` check. Its final pass condition is:

> Pass if the comments comply with every applicable repository requirement and are specific to the issue rather than generic boilerplate. If the repository's stated policy requires disclosure of AI assistance for issues or comments, the candidate comments must contain the required disclosure; its absence fails this check. A claim posted before reproduction must state what the contributor intends to investigate and report without asserting results that have not yet been observed.

I revised this check after `pkg-20` was incorrectly accepted in my first full eval run. The package had good technical reproduction evidence, but its repository required AI-assistance disclosure and the candidate comments did not include it. My earlier wording said to follow repository conventions, but it was not explicit enough that a missing required disclosure must fail the check.

I changed the pass condition to make that consequence explicit: when the repository requires AI disclosure for comments, the disclosure must appear in the candidate comments or the check fails. I also kept the requirement that a pre-reproduction claim describe the intended investigation without asserting a result that has not yet been observed, because claim comments are evaluated before reproduction evidence exists.

**Trade-offs**

One trade-off came from revising `behavior-matches-issue` and `claims-match-evidence` after `pkg-09`.

In my first full eval run, `pkg-09` was incorrectly rejected even though the gold label was accept. The reproduction report explicitly said:

> “Result: I could NOT reproduce scenario 2”

It also disclosed why the attempt might not have reached the necessary trigger condition:

> “my padding approach may not achieve that, since fd appears to flush both command buffers at the same file-count boundary on this input”

The package therefore documented a real reproduction attempt, showed the observed result, and clearly explained an important limitation. My original checks were too strict because they effectively expected the reported failure itself to appear for the package to pass.

I loosened the checks so an honest cannot-reproduce report can still pass when it shows the actual result of a relevant attempt and clearly states the limitation or uncertainty that may explain why the target behavior did not occur.

The trade-off is that this makes the rubric more permissive: a cannot-reproduce package can pass even without showing the reported failure, so the checks must rely more heavily on whether the attempt was relevant, rerunnable, and transparent about its limitations.

To make sure I had not loosened the rubric too far, I reran `pkg-09` together with `pkg-20` and the calibration package `calib-02` as a canary. After the revision, `pkg-09` changed to accept as intended, while `pkg-20` and `calib-02` still rejected. This gave me evidence that the change fixed the honest cannot-reproduce case without broadly accepting weak packages.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.

# Issue #55 Implementation Plan

Issue: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/55
Branch: `fix/55-skill-extractor-detection`

## Diagnosis

I reproduced all five tests associated with issue #55.

The normal test run reported:

> `13 passed, 5 xfailed`

Running the same test file with `--runxfail` exposed the underlying failures:

> `5 failed, 13 passed`

The failing tests were:

- `test_text_with_typescript_files`
- `test_database_technology_detection`
- `test_devops_tool_detection`
- `test_javascript_detection`
- `test_docker_compose_detection`

The current detection logic does not recognize several technology-specific patterns exercised by these tests.

For JavaScript and TypeScript, `_detect_languages()` currently detects JS/TS from `.js` or `.ts` filename hints, `package.json`, or the regex `\b(import|require)\s+`. The JavaScript repro uses `require('fs')`, which has no whitespace after `require`, so that regex does not match. The TypeScript repro uses syntax such as `export interface User` and typed fields without a filename, import/require statement, or `package.json`, so none of the existing JS/TS signals fire.

The database test uses `psycopg2`, while `_detect_databases()` currently checks whether a database's configured name, such as `postgresql`, appears literally in the text. As a result, the PostgreSQL client-library reference is not recognized.

The Docker tests use Dockerfile structure (`FROM`, `RUN`, `EXPOSE`) and Docker Compose structure (`services:`, `build:`, `ports:`), while `_detect_tools()` currently recognizes Docker only when the literal string `docker` appears in the input.

Together, these explain the five reproduced failures: the extractor's current detectors recognize literal names and a limited set of syntax patterns, but the failing tests use valid technology-specific indicators that are outside those patterns.

## Scope

### In scope

I will make a bounded change to the skill extractor's existing detection logic so that the patterns exercised by the five issue-#55 tests can be recognized.

The change will cover:

- JavaScript `require(...)` calls where there is no whitespace between `require` and `(`.
- TypeScript-specific syntax represented by the existing TypeScript test, using a sufficiently specific structural signal rather than a generic word match.
- PostgreSQL detection from the `psycopg2` client-library reference used by the existing database test.
- Docker detection from the Dockerfile-style syntax exercised by the existing test.
- Docker detection from the Docker Compose-style YAML structure exercised by the existing test.
- Removal of the five issue-#55 `xfail` markers after the underlying assertions pass normally.

### Out of scope

I will not:

- redesign the overall skill-extraction architecture;
- replace the existing confidence-scoring system;
- broadly rewrite detection for unrelated languages, databases, frameworks, or tools;
- add unrelated cleanup or refactoring;
- attempt to recognize every possible JavaScript, TypeScript, PostgreSQL, Dockerfile, or Docker Compose syntax pattern;
- change tests unrelated to issue #55.

The goal is to extend the existing detectors with targeted signals that address the reproduced failures without turning this into a general parser rewrite.

## Files to change

### `ingestion/parsers/skill_extractor.py`

Update the existing detection logic in:

- `_detect_languages()`
- `_detect_databases()`
- `_detect_tools()`

The implementation will keep the current `SkillDetection` output structure and confidence-scoring approach.

### `tests/unit/test_skill_extractor.py`

Remove the five `@pytest.mark.xfail(...)` markers associated with issue #55 once their assertions pass with the implementation change.

I do not currently expect to change the assertions themselves because they already describe the behavior the issue expects.

## Implementation approach

### 1. JavaScript detection

Adjust the JavaScript/CommonJS detection so that a normal function-style call such as:

`require('fs')`

is recognized without requiring whitespace after `require`.

The pattern should remain specific to an actual `require(...)`-style construct rather than matching arbitrary occurrences of the word `require`.

### 2. TypeScript detection

Add a targeted TypeScript syntax signal for the structure exercised by the existing test, such as an interface declaration.

The signal should be specific enough to distinguish TypeScript source syntax from ordinary prose. When a TypeScript-specific signal is present, the detected language should be `TypeScript` rather than relying only on a `.ts` filename.

### 3. PostgreSQL detection

Extend database detection so that the PostgreSQL client-library identifier `psycopg2` is treated as evidence for PostgreSQL.

I will keep this within the existing database-detection flow rather than introducing a new general dependency parser.

### 4. Dockerfile detection

Add a bounded structural signal for Dockerfile-style input represented by the test.

I will avoid treating a single generic word such as `RUN` as sufficient Docker evidence by itself. The implementation should use a combination or sufficiently Docker-specific pattern from the existing test input to reduce false positives.

### 5. Docker Compose detection

Add a bounded signal for the Docker Compose YAML structure represented by the existing test, using the combination of Compose-style keys rather than treating a generic YAML key alone as proof of Docker.

### 6. Remove expected-failure markers

After the implementation makes all five underlying assertions pass with `--runxfail`, remove the five issue-#55 `xfail` markers from `tests/unit/test_skill_extractor.py`.

The test assertions themselves should remain unchanged unless implementation work reveals that one is inconsistent with the issue's intended behavior.

## Test plan

The saved reproduction before the fix is:

```bash
.venv/Scripts/pytest tests/unit/test_skill_extractor.py -q --runxfail
```

Before the change:

```text
5 failed, 13 passed
```

The five failures are the issue-#55 JavaScript, TypeScript, PostgreSQL, Dockerfile, and Docker Compose detection tests.

### After the implementation

First, while the `xfail` markers are still present, re-run:

```bash
.venv/Scripts/pytest tests/unit/test_skill_extractor.py -q --runxfail
```

Expected result:

```text
18 passed
```

This verifies that the implementation fixes the assertions underneath the expected-failure markers.

Then remove the five issue-#55 `xfail` markers and run the normal test command:

```bash
.venv/Scripts/pytest tests/unit/test_skill_extractor.py -q
```

Expected result:

```text
18 passed
```

This verifies that the five tests are now ordinary passing regression tests rather than expected failures.

I will also inspect the detected skill names for the five reproduced inputs if a test failure or unexpected extra detection appears while implementing the patterns.

Before preparing the pull request, I will also run the repository-required checks:

```bash
make check
make test-unit
```

## Risks and unknowns

The main risk is false-positive detection from patterns that are too broad. JavaScript/TypeScript keywords, Dockerfile instructions, and YAML keys can appear in text that is not actually source code for those technologies.

To limit that risk, I will prefer recognizable structural combinations or syntax patterns over isolated generic words.

The exact regexes or indicator combinations are implementation details that I will confirm while building and testing. The affected detector functions and intended outcomes are known, so these details do not prevent implementation from starting.

There is also a possibility that adding new indicators causes an input to produce an additional skill alongside an existing detection. One known example is the TypeScript test's `id: string` syntax: the current Python type-annotation regex can match the `str` prefix of `string`. Issue #55 only requires the missing technologies to be detected, so I will avoid expanding this fix into unrelated language-classification cleanup unless it prevents the targeted change from working correctly.

I will review the targeted test output and avoid unrelated changes to the extractor's existing multi-skill behavior.

## Deviations

The implementation followed the planned scope and approach. I updated the existing language, database, and tool detection logic and removed the five issue-#55 `xfail` markers after their underlying assertions passed.

The targeted skill-extractor tests passed with all 18 tests passing, and the full unit suite completed with 380 passed and 48 existing xfailed tests.

`make check` passed Ruff and Black but stopped during mypy because the installed NumPy type stubs use syntax that conflicts with the repository's Python 3.11 mypy target in my local environment. The reported error was inside `.venv/Lib/site-packages/numpy/__init__.pyi`, not in the files changed for issue #55, so I did not change project code or dependencies to work around it.

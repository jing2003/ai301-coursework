---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading


## The question

Determine whether exactly one candidate pull request (PR) package is ready to submit.

A PR package includes the proposed title and description, committed changes and diff, test evidence, and the implementation plan, including any documented deviations. Evaluate these artifacts against the related issue, the stated plan, and the repository's contribution requirements.

Use the rubric and procedure in this skill to make an evidence-based readiness decision. Do not review unrelated issues, grade multiple PR packages in one run, or substitute personal preferences for the defined checks.

## Inputs and modes

Determine the operating mode from the user's request or the evaluation context. Grade exactly one PR package per run.

### Live mode

Use live mode when reviewing a student's actual proposed pull request.

Read the following inputs:

1. **Implementation plan:** Read `plan.md`, including the test plan and any `## Deviations` section.
2. **Committed changes:** From the root of the student's Path Review working copy, run `git diff main...HEAD` to inspect all committed changes on the current branch relative to `main`. Do not substitute uncommitted changes for this diff.
3. **PR title and description:** Read the draft title and description from `pr_draft.md`.
4. **Test evidence:** Read `test_evidence.md`, including the before-and-after reproduction results and the repository's required checks.
5. **Issue context:** Read the specified issue's URL and thread to understand the reported problem, expected behavior, and relevant discussion.
6. **Repository requirements:** Read `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md` from the scoped Path Review repository.

Use the actual paths supplied by the user when they differ from these filenames.

For a house-chain submission, use the provided house issue, reproduction package, implementation plan, branch diff, PR draft, and testing evidence instead of the student's own artifacts. Apply the same rubric and verdict rule.

### Eval mode

Use eval mode when the evaluation harness supplies a frozen PR package from `eval/packages/`.

Treat the supplied package text as the complete and only source of evidence. Do not fetch external information, inspect the live repository, read local project files, or supplement the package with assumptions.

Evaluate every applicable rubric check using the evidence contained in the package, then apply the complete verdict rule. Do not skip checks or change grading standards between packages.

## The scope seam (live mode only)

In live mode, read `scope.md` before reading any PR artifacts or executing grading checks.

1. Identify the repository specified on the `Repo:` line and read the applicable scope rules.
2. If the `Repo:` line is missing or contains an unfilled placeholder, stop without grading. Instruct the user to configure the `Repo:` line in `scope.md` with their section's Path Review repository.
3. Verify that the proposed PR's intended base repository matches the repository specified in `scope.md`. Before the PR is opened, use the working copy's repository context and the intended PR destination to establish scope. If the destination is outside the permitted scope or cannot be verified, refuse to grade and explain the mismatch.
4. Follow all applicable house rules defined in `scope.md` throughout the review.
5. Continue to the remaining inputs and grading checks only after scope validation succeeds.

Do not guess the intended repository, silently change the configured scope, or override scope restrictions based on the PR's apparent quality.

In eval mode, ignore `scope.md` entirely. Grade the supplied frozen package without performing live repository scope validation.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` after validating `scope.md` and before reviewing the PR's outgoing text.

1. Review the proposed PR title and description in `pr_draft.md` against the writing rules in `voice-guide.md`.
2. Identify any violations of the guide, citing the specific rule and the relevant text from the draft.
3. Report violations in the readable review summary and suggest a concrete correction when appropriate.
4. Keep personal writing preferences separate from the formal readiness decision. A voice-guide violation must not change the final verdict unless a check in `rubric.md` explicitly evaluates that requirement.
5. Apply the rubric's universal communication-quality checks independently of the personal voice guide.

Do not invent additional writing rules, rewrite the PR without being asked, or reject a PR solely because its wording differs from your preferred style.

In eval mode, ignore `voice-guide.md` entirely. Evaluate communication quality only through the checks defined in `rubric.md` and the evidence provided in the frozen package.

## Component reads

Use the skill's components together to perform a consistent, evidence-based PR review.

1. Read `rubric.md` to identify all grading checks, their evidence requirements, pass conditions, weights, and the final verdict rule.
2. Read `references/evidence-guide.md` to determine where each type of evidence is located in the PR package and what constitutes sufficient evidence.
3. Read `procedure.md` and execute its steps as written, including the required read order, evidence gathering, check execution, and verdict assembly.
4. Apply every applicable rubric check using the evidence collected through the procedure. Record a `pass`, `fail`, or `unclear` grade and one specific supporting evidence line for each check.
5. Assemble the final verdict using only the rule defined in `rubric.md`. Do not invent additional checks, change weights, or override the verdict based on intuition.

Before grading, verify that `rubric.md` and `procedure.md` contain substantive, student-written instructions rather than only template comments or placeholders.

If either file has no substantive content, refuse to grade. Identify the incomplete component and explain that it must be completed before the review can proceed.

If `procedure.md` does not explain how to perform a necessary step, report the procedural gap rather than silently inventing a method. Do not present an unsupported conclusion as a completed review.

## Verdict and output

Return exactly one final verdict for each successfully graded PR package:

- `accept`: The PR is ready to submit according to the verdict rule in `rubric.md`.
- `reject`: The PR is not ready to submit and requires attention before submission.

Do not introduce additional verdicts, numerical scores, or conditional outcomes such as "accept with reservations."

Before the final JSON block, provide a concise, human-readable summary of the review. Identify each rubric check, its grade (`pass`, `fail`, or `unclear`), and the specific evidence supporting that grade. For failed or unclear checks, explain what needs attention.

Apply the verdict rule defined in `rubric.md` without overriding it based on personal judgment.

End every completed review with the exact fenced JSON structure below. Replace its placeholders with the PR URL or evaluation bundle ID, all rubric check results, their evidence, and the final verdict.

The JSON must be syntactically valid, preserve the required keys and their order, and contain no additional fields. Do not include any text after the closing JSON fence.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```


## Grading discipline

Follow these rules for every PR review:

1. **Evidence first:** Ground every check grade in a specific fact, file, command result, or quote from the permitted evidence. Record the evidence that determined the grade. Never use vague statements such as "looks good" as justification.

2. **Grade the artifact, not its polish:** Evaluate the actual changes, plan alignment, testing evidence, and repository requirements. Do not reward confident wording, attractive formatting, or unnecessary detail when the underlying evidence is insufficient. A concise but complete PR can pass.

3. **The rubric decides:** Apply each check's stated pass condition and weight exactly as written in `rubric.md`. Do not invent new checks, adjust requirements, or override a check because its result feels incorrect. If a rubric rule produces an unexpected result, report the concern separately without changing that run's grade.

4. **The procedure decides how:** Follow the read order, evidence gathering, check execution, and verdict assembly steps in `procedure.md`. If the procedure leaves a necessary action undefined, report the gap rather than silently inventing a process.

5. **Handle uncertainty explicitly:** Use `unclear` when the available evidence cannot establish whether a check passes or fails. Do not assume missing evidence is positive evidence. Apply the treatment of `unclear` specified in `rubric.md`; if the verdict rule is silent, treat an unverifiable claim as failing when determining the final verdict.

6. **Remain consistent:** Apply the same rubric, evidence standards, and verdict rule to every eligible PR package. Do not relax or tighten requirements based on the author, perceived effort, or whether a particular verdict seems desirable.

Base the final `accept` or `reject` verdict on the recorded check results and the rubric's verdict rule, not on intuition or an overall impression.

# Procedure: how this tool grades a PR package

## Read order

Before assigning any grades, read the permitted PR package evidence in the following order:

1. **Establish the review context.** Determine whether the run is in live or eval mode using `SKILL.md`. In live mode, validate `scope.md` before reviewing the package. In eval mode, use only the supplied frozen package.
2. **Read the issue and repository requirements.** Identify the reported problem, expected behavior, scope constraints, required PR information, and applicable testing or contribution standards.
3. **Read the implementation plan.** Record the intended changes, affected components, scope boundaries, test plan, and any documented deviations or deliberately omitted work.
4. **Read the committed diff.** In live mode, run `git diff main...HEAD` from the Path Review working copy. Record changed files, substantive code changes, supporting tests, and any potentially unrelated modifications. In eval mode, read the diff supplied in the package.
5. **Read the test evidence.** Identify the reproduction steps, before-and-after outcomes, verification commands, reported results, and any disclosed testing limitations.
6. **Read the PR title and description.** Identify claims about the implementation, issue reference, testing, limitations, and compliance with repository requirements.

Keep notes from each source before assigning grades. Read the plan before the diff so the intended work is established independently of the implementation. Read the description after the diff and test evidence so its claims can be checked against observable facts.

Use `references/evidence-guide.md` to locate equivalent evidence in live and eval modes. Do not retrieve external information in eval mode.

## Evidence gathering

Use `references/evidence-guide.md` to locate the relevant evidence in each mode. Gather and record facts before assigning check grades.

1. **Plan fidelity**
   - Extract the planned changes, scope boundaries, and documented deviations from the implementation plan.
   - Compare these against the diff's changed files and substantive behavior.
   - Record matches, unplanned changes, omitted planned work, and whether any differences are explicitly disclosed.

2. **Description accuracy**
   - Extract the PR title, summary, change descriptions, and testing claims.
   - Compare each material claim against the actual diff, implementation plan, and recorded test results.
   - Record accurate claims, unsupported statements, contradictions, and disclosed limitations.

3. **Test evidence**
   - Extract the reproduction steps and expected behavior from the issue and the plan's test section.
   - Compare the planned verification with the actual commands, inputs, and results in the test evidence.
   - Record observable before-and-after behavior where applicable, including whether the central fix is verified.
   - Identify missing evidence, failed tests, and honestly disclosed limitations.

4. **Repository checks**
   - Identify the repository's required testing and validation commands from its contribution requirements.
   - Compare those requirements against the commands attempted and results recorded in the test evidence.
   - Record which checks passed, failed, were unavailable, or were not attempted.
   - Distinguish accurately disclosed limitations from omitted checks or misleading success claims.

5. **Diff reviewability**
   - Inspect the changed files and individual diff hunks.
   - Identify debugging statements, commented-out code, unrelated edits, generated artifacts, and excessive formatting changes.
   - Compare each potentially unnecessary change against the issue and implementation plan.
   - Record whether the changes are relevant, focused, and understandable to a reviewer.

6. **Repository standards**
   - Identify applicable requirements for PR descriptions, issue references, contribution policies, and AI-use disclosure.
   - In live mode, obtain these from the scoped repository's PR template and contribution documentation.
   - In eval mode, use only the requirements stated in the frozen package's repo-facts block.
   - Compare each requirement against the PR title and description.
   - Record satisfied requirements, missing information, and any contradictions.

For every check, retain the specific evidence source and the fact or quote that supports the eventual grade.

If evidence is missing, record that absence rather than assuming success or failure. Do not invent commands, results, repository rules, or undocumented changes.

Use equivalent evidence locations for live and eval packages while applying the same rubric conditions.

## Check execution

After completing the read order and evidence gathering, evaluate every check in the order it appears in `rubric.md`.

Use the check names, pass conditions, evidence requirements, and weights exactly as defined in the current rubric. Do not skip a check or introduce additional checks.

For each check:

1. Read the check's evidence requirements, pass condition, and weight from `rubric.md`.
2. Use the evidence already gathered from the permitted sources. Revisit a source only when necessary to resolve a specific uncertainty.
3. Compare the recorded evidence directly against the check's pass condition.
4. Assign exactly one grade:
   - `pass`: The available evidence satisfies the pass condition.
   - `fail`: The available evidence demonstrates that the pass condition is not satisfied.
   - `unclear`: The permitted evidence is insufficient to establish whether the pass condition is satisfied.
5. Record one concise evidence line identifying the specific fact, result, contradiction, or missing information that determined the grade.
6. Continue evaluating the remaining checks, even if an earlier required check fails.

Do not invent evidence, assume that an undocumented test passed, or treat confident claims as proof.

Distinguish honestly disclosed limitations from hidden problems. A disclosed shortfall may satisfy a check when its stated pass condition allows it, but disclosure alone does not establish that the central fix works.

Use the same evidence standards in live and eval modes. In eval mode, never obtain additional evidence outside the frozen package.

If evidence for a check is absent or insufficient, grade it `unclear`. Grade it `fail` when the available evidence affirmatively shows that the pass condition was not satisfied, such as an explicitly omitted mandatory check or a test result contradicting the claimed fix.

Do not infer that an action was not performed merely because its output is missing.

Apply the rubric as written. Do not change grades based on the desired final verdict or the apparent quality of the overall PR.

## Verdict assembly

After evaluating all six rubric checks, assemble the final verdict using the rule in `rubric.md`.

1. Review the recorded grades and evidence for every check in rubric order.
2. Return `accept` only if every `required` check received `pass`.
3. Return `reject` if any `required` check received `fail` or `unclear`. Treat `unclear` as failing for verdict assembly because submission readiness has not been verified.
4. Never allow a `preferred` check to change the final verdict.
5. If the verdict is `reject`, identify the first required check graded `fail` or `unclear` in rubric order as the primary reason for rejection.
6. Quote or summarize the specific evidence that determined that primary check's grade. Also report other failed or unclear checks so the contributor can address all identified problems.
7. If the verdict is `accept`, briefly explain which evidence establishes that the required conditions were satisfied.

Before producing the final response, verify that:

- Every rubric check has exactly one grade: `pass`, `fail`, or `unclear`.
- Every check has a concise evidence line grounded in the permitted sources.
- Check names match `rubric.md` exactly and appear in rubric order.
- The final verdict follows the rubric's aggregation rule.
- No unsupported facts, additional verdict categories, or numerical scores were introduced.

Provide a concise, human-readable review summary before the machine-readable result.

End the completed review with the exact fenced JSON block defined in `SKILL.md`. Preserve the required schema and key order: `item`, `checks`, and `verdict`.

Use the PR URL as `item` when an actual PR exists. For a live draft that has not been opened, use an unambiguous identifier for the proposed PR, such as its intended repository and branch. For an eval package, use its bundle ID.

Do not add commentary after the final JSON block.

If a prerequisite requires refusal under `SKILL.md`, explain the refusal without inventing check grades or producing a fabricated verdict.

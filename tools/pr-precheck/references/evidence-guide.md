# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**Where it lives:**

- **Eval mode:** Read `## Issue` and `## Plan context` for the reported problem, planned implementation, affected files, scope boundaries, and test plan. Read `### Diff` under `## Candidate PR` for the actual changes, and `### Description` for claims about what was implemented. Use only the supplied package.
- **Live mode:** Read the GitHub issue thread and `plan.md`, including its scope boundaries and `## Deviations` section. Compare them against the committed branch changes from `git diff main...HEAD`. Read the title and description in `pr_draft.md` to verify that the proposed PR accurately represents those changes.

**What good looks like:**

Every substantive change in the diff belongs to the planned implementation or a documented, relevant deviation. Planned work that was intentionally omitted is disclosed rather than silently presented as complete.

The PR description accurately represents the implemented changes and their limitations. Silent drift occurs when the diff adds unplanned work, omits planned work without explanation, or contradicts the description's claims.

A documented deviation resolves a plan mismatch only when it is relevant to the issue; unrelated changes remain subject to the Diff reviewability check even when disclosed.

## Test evidence (harness category: not-tested)

**Where it lives:**

- **Eval mode:** Read the reproduction evidence and test plan in `## Plan context`. Compare the expected verification steps against `### Test evidence` under `## Candidate PR`. Use `## Repo facts` to identify any repository-stated testing or validation requirements. Read `### Description` for claims about testing outcomes.
- **Live mode:** Read the issue's reported behavior, the Unit 2 reproduction steps and evidence, and the test plan in `plan.md`. Compare them against `test_evidence.md`, which records the before-and-after reproduction and results of the repository's required checks. Read `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md` to identify required validation commands. Cross-check testing claims in `pr_draft.md`.

**What good looks like:**

The evidence identifies observable commands or verification steps, relevant inputs, expected outcomes, and actual results sufficient to establish that the central issue was addressed. Before-and-after reproduction demonstrates the behavioral change where applicable.

Repository-required checks are attempted and their outcomes are accurately reported. A failed, unavailable, or incomplete check is not automatically disqualifying when the limitation is disclosed and the remaining evidence establishes readiness. Unsupported statements such as "all tests passed" do not substitute for observable evidence.

## Diff quality (harness category: unreviewable)

**Where it lives:**

- **Eval mode:** Inspect `### Commits` and `### Diff` under `## Candidate PR`. Compare the changed files and diff hunks against the intended changes and scope boundaries in `## Plan context` and the reported problem in `## Issue`.
- **Live mode:** Inspect the committed branch diff using `git diff main...HEAD` and review the commit list using `git log main..HEAD --oneline`. Compare these changes against `plan.md`, including documented deviations, and the related GitHub issue.

**What good looks like:**

The diff presents a focused change that a maintainer can understand and evaluate against the reported issue. Supporting code, tests, and configuration changes are relevant to the fix, and no unrelated modifications obscure the implementation.

Look for debug statements, temporary files, commented-out code, generated artifacts, unnecessary formatting churn, and unrelated refactoring. A large diff is acceptable when its changes are necessary and reviewable; a small diff can still fail if it contains irrelevant or accidental modifications.

## Standards and comms (harness category: standards-wall)

**Where it lives:**

- **Eval mode:** Read `## Repo facts` for the repository's PR template requirements, contribution guidelines, and stated policies, including AI-use disclosure when applicable. Read `## Thread highlights` for any explicit maintainer instructions. Compare these requirements against `### Title` and `### Description` under `## Candidate PR`. Use only the frozen package's stated requirements; do not import policies from other repositories.
- **Live mode:** Read `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md` from the scoped Path Review repository. Check the related GitHub issue thread for explicit maintainer directions. Compare those requirements against the PR title and description in `pr_draft.md`, including its issue reference, testing information, reviewer notes, and AI-use disclosure.

**What good looks like:**

The PR satisfies the repository's explicitly applicable contribution requirements and responds to relevant maintainer instructions. Required information is present and meaningful rather than left as empty placeholders or unsupported boilerplate.

Equivalent wording or formatting is acceptable when it communicates the required information. Do not impose a PR template, AI-use disclosure, or other policy that the repository has not stated. Evaluate whether the description's implementation claims match the diff under Plan fidelity rather than duplicating that judgment here.

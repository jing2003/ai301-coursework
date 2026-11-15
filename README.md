# CodePath AI301 — Open-Source AI Engineering

This repository documents my coursework and learning experience in **CodePath AI301**, where I developed AI-assisted engineering workflows and applied them to real open-source contributions.

Throughout the course, I practiced evaluating GitHub issues, reproducing bugs, planning implementations, testing changes, reviewing pull requests, and collaborating with project maintainers.

## Highlights

- **Open-source contribution:** Contributed to [Rafter CLI](https://github.com/Raftersecurity/rafter-cli) through [PR #341](https://github.com/Raftersecurity/rafter-cli/pull/341), merged into upstream `main` on November 14, 2026.
- **Implementation:** Standardized error formatting in Node.js and Python backend commands (`run`, `get`, and `usage`), added regression tests, and updated the CLI specification.
- **Testing and validation:** Used isolated Docker environments to verify changes and investigate environment-related testing failures.
- **Maintainer collaboration:** Responded to code review feedback, revised the implementation, and revalidated the changes before merging.
- **AI-assisted workflows:** Developed and customized tools for issue evaluation, reproduction checks, implementation planning, and PR readiness.

PR #341 addresses the backend-command portion of [Rafter CLI issue #34](https://github.com/Raftersecurity/rafter-cli/issues/34). The broader issue remains open.

## Repository Structure

| Directory                                      | Contents                                                                                                          |
| ---------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| [`beat-1-sandbox/`](beat-1-sandbox/)           | Units 1–4: issue selection, reproduction, planning, implementation, PR preparation, and saved evaluation results. |
| [`beat-2-contribution/`](beat-2-contribution/) | Assignment 5: detailed open-source contribution history, testing evidence, challenges, and reflections.           |
| [`beat-3-portfolio/`](beat-3-portfolio/)       | Assignment 6: technical write-up, LinkedIn post content, and retained course materials.                           |
| [`tools/`](tools/)                             | Four rubric-driven AI skill implementations developed and evaluated during Units 1–4.                             |

## AI-Assisted Engineering Tools

The repository includes four skill implementations:

| Tool                                          | Purpose                                                                                       |
| --------------------------------------------- | --------------------------------------------------------------------------------------------- |
| [`issue-select`](tools/issue-select/SKILL.md) | Evaluate open-source issues against a structured rubric.                                      |
| [`repro-check`](tools/repro-check/SKILL.md)   | Assess the quality and readiness of bug reproduction evidence.                                |
| [`plan-check`](tools/plan-check/SKILL.md)     | Evaluate implementation plans for feasibility, scope, and supporting evidence.                |
| [`pr-precheck`](tools/pr-precheck/SKILL.md)   | Review pull requests for implementation fidelity, testing evidence, and submission readiness. |

Later course work also involved issue-scout, voice-guard, ship-gate, and PR-monitor workflows. Their development and application are documented in the [contribution story](beat-2-contribution/contribution-story.md).

## Open-Source Contribution and Portfolio

- [Rafter CLI PR #341 — Merged contribution](https://github.com/Raftersecurity/rafter-cli/pull/341)
- [Rafter CLI issue #34 — Original issue](https://github.com/Raftersecurity/rafter-cli/issues/34)
- [Contribution story](beat-2-contribution/contribution-story.md)
- [Technical write-up](beat-3-portfolio/technical-writeup.md)
- [LinkedIn post content](beat-3-portfolio/linkedin-post.md)

The coursework documents preserve the work, evidence, and project status recorded during the original assignments. For the latest contribution status, refer to the upstream GitHub pull request.

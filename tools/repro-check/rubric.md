# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check                  | Evidence                                                                                                                                                                                                                | Pass condition                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Weight   |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| env-recorded           | The reproduction report's environment record, read against the issue context and any relevant repo-facts or repository setup information described in `references/evidence-guide.md`.                                   | Pass if the report identifies the software/tool version and other environment details that are material to interpreting and repeating the reproduction attempt. If the environment differs in a meaningful way from the version or environment targeted by the issue, that difference is explicitly disclosed.                                                                                                                                                                                                                                                                                                  | required |
| steps-rerunnable       | The reproduction report's starting state, inputs or files, setup, commands, and actions, together with any clearly identified repository setup instructions it relies on, as located by `references/evidence-guide.md`. | Pass if another person could recreate the relevant starting state and input and repeat the attempt without guessing a material setup step, command, input, or action needed to trigger the target behavior.                                                                                                                                                                                                                                                                                                                                                                                                     | required |
| behavior-matches-issue | The issue's described actual/expected behavior read against the reproduction report's artifacts, such as output excerpts, errors, logs, screenshots, or test results, as located by `references/evidence-guide.md`.     | Pass if the artifacts show the outcome of an attempt aimed at the behavior described by the issue. For a successful reproduction, they must show the same target behavior rather than a different or adjacent failure. For a cannot-reproduce result, they must show the actual observed outcome of a relevant attempt, and the report must disclose any material condition or uncertainty that may explain why the target behavior did not occur. Failing to reach a suspected trigger condition does not by itself fail an honestly reported cannot-reproduce attempt when that limitation is clearly stated. | required |
| claims-match-evidence  | Material statements in the claim and reproduction report read against the environment record, reproduction steps, and artifacts described in `references/evidence-guide.md`.                                            | Pass if the package's material conclusions do not go beyond what the available evidence supports and any important uncertainty or limitation is disclosed. Claims that the issue was reproduced or claims about its cause require supporting evidence. Procedural statements about what the contributor tried may be supported by the reproduction report itself unless they are contradicted by the package; they do not each require a separate artifact.                                                                                                                                                     | required |
| repo-conventions       | The claim and reproduction comments read against the issue context and the repository's stated contribution requirements, templates, policies, or conventions located according to `references/evidence-guide.md`.      | Pass if the comments comply with every applicable repository requirement and are specific to the issue rather than generic boilerplate. If the repository's stated policy requires disclosure of AI assistance for issues or comments, the candidate comments must contain the required disclosure; its absence fails this check. A claim posted before reproduction must state what the contributor intends to investigate and report without asserting results that have not yet been observed.                                                                                                               | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept only if every applicable required check passes. Any required check graded `fail` causes a reject verdict.

In eval mode and full-package live mode, `unclear` on a required check counts as fail.

In claim-only live mode, checks that require reproduction-report evidence are excluded from the verdict as directed by `SKILL.md`; any other applicable required check graded `unclear` counts as fail.

Preferred checks, if added later, never change the verdict.

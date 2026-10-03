# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check               | Evidence                                                                                                                                      | Pass condition                                                                                                                                                                                                            | Weight   |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| diagnosis-evidence  | The plan's stated diagnosis read against the reproduced behavior, commands, and output in the repro evidence.                                 | Pass when the diagnosis is supported by the reproduced evidence and does not contradict what the reproduction actually demonstrates.                                                                                      | required |
| cause-targeting     | The plan's diagnosis and proposed approach read together against the repro evidence.                                                          | Pass when the planned change addresses the cause indicated by the evidence rather than only masking or working around the observed symptom.                                                                               | required |
| bounded-scope       | The plan's scope, files to change, stated non-goals, and proposed approach.                                                                   | Pass when the work is one bounded change needed to address the reproduced issue, without unrelated refactors, features, or unnecessary expansion.                                                                         | required |
| execution-ready     | The plan's files to change and implementation approach read against the repo facts and relevant code context included in the package.         | Pass when another developer could begin implementing the change from the plan without having to invent a missing core step, target, or decision.                                                                          | required |
| test-validity       | The plan's test plan read against the original reproduction steps and observed failure.                                                       | Pass when the proposed checks exercise the behavior that reproduced the issue and define an observable result that would distinguish the fixed behavior from the reproduced failure.                                      | required |
| uncertainty-honesty | The plan's diagnosis, risks, unknowns, and implementation claims read against the evidence available in the package.                          | Pass when claims are stated with a level of certainty supported by the available evidence, and material assumptions, risks, or unresolved details are identified as uncertain rather than presented as established facts. | required |
| thread-conventions  | The draft plan comment and plan read against the issue-thread highlights, repo-facts block, and stated repository conventions in the package. | Pass when the plan and comment do not contradict relevant thread decisions or repository requirements and follow applicable contribution and coordination conventions.                                                    | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept when every required check passes. Reject when any required check fails or is unclear. A grade of `unclear` counts as a failure because a plan should not be considered ready to build when the evidence is insufficient to determine whether a required condition is satisfied. Preferred checks, if added later, do not affect the verdict.

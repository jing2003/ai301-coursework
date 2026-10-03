# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

1. In live mode, read `scope.md` first. Confirm that the issue belongs to the scoped repository and note any Path Review house rules that affect the plan or plan comment.
2. Read `rubric.md` and `references/evidence-guide.md`. List every rubric check, the evidence each check requires, and the verdict rule before grading anything.
3. Read the issue context and relevant thread information. Record the reported behavior, requested outcome, constraints, maintainer or contributor guidance, and any decisions that affect what a valid plan may propose.
4. Read the reproduction evidence before reading the plan. Record the exact behavior reproduced, the commands or inputs that triggered it, the observed output, and any evidence about the likely cause. Do not let the plan's diagnosis replace what the reproduction actually proves.
5. Read the repo facts and stated repository conventions. Record relevant file locations, contribution requirements, testing expectations, and implementation constraints supplied by the package.
6. Read the complete plan. Record its diagnosis, proposed scope and non-goals, files or components it intends to change, implementation approach, test plan, and stated risks or unknowns.
7. Read the complete draft plan comment. Compare what it tells the issue thread with the full plan and note any material claim, scope, or test detail that differs.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

1. For `diagnosis-evidence`, compare the plan's stated diagnosis with the behavior, commands, output, and causal evidence recorded from the reproduction. Record the specific reproduction fact that supports or contradicts the diagnosis.
2. For `cause-targeting`, compare the diagnosed cause with the implementation approach. Record whether the proposed change acts on the component or behavior implicated by the evidence, or merely hides the visible symptom.
3. For `bounded-scope`, gather the plan's stated scope, non-goals, files or components to change, and implementation approach. Record any work that is unrelated to the reproduced issue or expands the change beyond what is needed to address it.
4. For `execution-ready`, gather the planned files or components and the concrete implementation steps, then compare them with the supplied repo facts and code context. Record whether an implementer has a clear starting point and core approach without needing to invent a missing decision.
5. For `test-validity`, place the proposed test plan next to the original reproduction steps and failure output. Record the input or behavior that will be exercised after the change and the observable result that is expected to differ from the reproduced failure.
6. For `uncertainty-honesty`, gather statements from the diagnosis, approach, risks, and unknowns that depend on evidence not established in the package. Record whether those points are identified as uncertain or are stated as confirmed facts.
7. For `thread-conventions`, compare the plan and draft comment with relevant thread decisions, repo facts, contribution requirements, and Path Review conventions. Record any conflict with an applicable instruction or convention.
8. Use only evidence available from the package in eval mode. In live mode, use the locations identified in `references/evidence-guide.md` in addition to the candidate plan and draft comment. Do not fill missing evidence with assumptions.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. Grade checks in this order: `diagnosis-evidence`, `cause-targeting`, `bounded-scope`, `execution-ready`, `test-validity`, `uncertainty-honesty`, then `thread-conventions`. This order establishes what the evidence says before judging whether the proposed implementation and verification follow from it.
2. For each check, apply only that check's pass condition from `rubric.md` to the evidence gathered for it.
3. Grade the check `pass` when the available evidence satisfies its pass condition.
4. Grade the check `fail` when the available evidence demonstrates that its pass condition is not satisfied.
5. Grade the check `unclear` only when evidence required to decide the check is genuinely absent or insufficient. Do not use `unclear` because the evidence is inconvenient to locate or because the decision is difficult.
6. Record one concise fact or quote that directly explains every grade. Do not grade from writing quality, section count, length, confidence, or formatting unless a repository convention explicitly makes one of those things relevant.
7. Reuse already gathered evidence when multiple checks depend on the same fact, but apply each check's own pass condition independently. A passing diagnosis does not automatically make cause targeting or execution readiness pass.
8. Do not invent a missing implementation detail, test expectation, repository fact, or thread decision in order to make a plan pass.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->

1. After all checks are graded, apply the verdict rule from `rubric.md` exactly as written.
2. Return `accept` only when every required check is `pass`.
3. Return `reject` when any required check is `fail` or `unclear`. Under this rubric, `unclear` counts as failure because the package has not provided enough evidence to establish that a required part of the plan is ready.
4. Preferred checks, if any are added later, may be reported but do not change the final verdict.
5. For a rejected package, make the evidence line for each failing or unclear check identify the concrete fact or missing evidence that prevented it from passing. For an accepted package, keep each evidence line tied to the fact that established the pass.
6. Produce only the binary verdict defined by the skill: `accept` for ready or `reject` for hold. Do not create an intermediate verdict.

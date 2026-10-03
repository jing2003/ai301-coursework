# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

**Where it lives**

- In an eval package, read the `Repro evidence` block for the reproduced steps, observed behavior, expected behavior, output, and any evidence that points toward a cause. Read the diagnosis or `Cause` statement in the `Candidate plan` against that evidence. Use the `Issue` section as context for the behavior the plan is intended to fix.
- In live mode, read the student's posted Unit 2 reproduction comment and the issue thread for the reproduced behavior, then compare those facts with the diagnosis in the draft `plan.md`.

**What good looks like**

The stated diagnosis explains behavior that the reproduction actually demonstrates and does not contradict the observed results. The proposed implementation target should follow from that diagnosis rather than addressing only a visible symptom with no connection to the reproduced evidence.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

**Where it lives**

- In an eval package, read the `Candidate plan` for the proposed change, named files or components, explicit in-scope work, and anything excluded from the change. Compare that scope with the reproduced issue and relevant `Repo facts`.
- In live mode, read the scope, files to change, non-goals, and approach in `plan.md`, alongside the reproduced issue and repository context.

**What good looks like**

The plan describes one bounded change needed to address the reproduced issue. Its named files or areas and non-goals keep unrelated refactors, additional features, and drive-by cleanup outside the work unless the evidence shows they are necessary.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

**Where it lives**

- In an eval package, read the files or components and implementation approach in the `Candidate plan`, then compare them with any relevant locations or constraints in `Repo facts`.
- In live mode, read the files and implementation approach in `plan.md` and inspect the repository locations needed to confirm that the proposed starting point and approach correspond to real code.

**What good looks like**

Another developer could identify where to begin and what core change to make without inventing the missing implementation strategy. The plan does not need to predict every line of code, but it must identify the relevant target and the concrete approach well enough to begin execution.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

**Where it lives**

- In an eval package, read the `Test` portion of the `Candidate plan` beside the steps, expected result, and actual result in `Repro evidence`.
- In live mode, compare the test plan in `plan.md` with the student's Unit 2 reproduction steps and artifacts. Also use repository testing conventions when they are relevant to how the behavior should be checked.

**What good looks like**

The test plan exercises the behavior that originally reproduced the issue and states an observable result that would distinguish the fixed behavior from the failure. Additional regression checks are useful when they exercise code affected by the same change, but they do not replace re-checking the original reproduced behavior.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

**Where it lives**

- In an eval package, read the diagnosis, approach, risks, unknowns, and other certainty claims in the `Candidate plan`. Compare those claims with what the `Repro evidence`, `Issue`, and `Repo facts` actually establish.
- In live mode, read the risks and unknowns in `plan.md` and compare factual claims with the reproduction evidence and repository code or documentation available to the student. After implementation begins, also read `## Deviations` for differences between the posted plan and the actual build.

**What good looks like**

Claims supported by evidence may be stated confidently. Material details that have not yet been established are identified as risks, assumptions, or unknowns rather than presented as facts. Honest uncertainty passes this evidence family; whether an unresolved detail makes the plan impossible to execute is evaluated under Executability, not Honesty. If implementation later differs from the plan, the deviation is stated rather than hidden.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

**Where it lives**

- In an eval package, read the `Candidate plan comment` against `Thread highlights`, `Repo facts`, the `Issue`, and the full `Candidate plan`. Repository requirements may appear in contribution-policy, templates, testing expectations, or AI-use/disclosure information in `Repo facts`.
- In live mode, read the draft `comment.md` against the live GitHub issue thread, including maintainer comments and decisions, and against relevant repository documentation such as `CONTRIBUTING.md`, issue or pull-request templates, and other stated contribution rules. Apply the Path Review house rules from `scope.md`.

**What good looks like**

The comment accurately represents the material diagnosis, scope, and intended verification from the plan and does not conflict with decisions already made in the issue thread. It follows applicable repository contribution and communication requirements, including disclosure rules when present, and is specific to the student's own reproduction rather than piggybacking on another contributor's plan.

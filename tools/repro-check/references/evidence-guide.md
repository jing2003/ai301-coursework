# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

**Where it lives:** In eval mode, look at the issue context, repo-facts block, and the reproduction report's environment information. In live mode, look at the GitHub issue, relevant repository setup documentation when needed, and the draft reproduction comment.

**What good looks like:** The report identifies the software/tool version and any environment details that are material to reproducing the issue. If the reproduction environment differs in a meaningful way from the environment or version targeted by the issue, the difference is explicitly disclosed.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

**Where it lives:** In eval mode, look at the reproduction report for the starting state, required inputs or files, setup, commands, and actions used to trigger the behavior. In live mode, look at the draft reproduction comment together with any repository setup instructions it relies on.

**What good looks like:** The report provides enough exact inputs, commands, setup, and actions for another person to repeat the attempt without guessing a material step. Ordinary setup may rely on clearly identified repository documentation instead of being unnecessarily repeated.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

**Where it lives:** In eval mode, compare the behavior described in the issue context with artifacts in the reproduction report, such as command output, error messages, logs, screenshots, or test results. In live mode, compare the GitHub issue's described behavior with the evidence included in the draft reproduction comment.

**What good looks like:** If the issue is reproduced, the evidence shows the same behavior described by the issue rather than a different or adjacent failure. If the issue cannot be reproduced, the evidence shows the actual result of a relevant reproduction attempt and the report identifies any material condition or uncertainty that may explain why the target behavior did not occur.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

**Where it lives:** Compare material conclusions in the claim and reproduction report with the environment record, reproduction steps, artifacts, and stated limitations. In live mode, use the draft comments and relevant issue-side evidence available on GitHub.

**What good looks like:** Material conclusions stay within what the evidence supports, and important uncertainties or limitations are stated rather than hidden. Claims that the issue was reproduced or claims about its cause require supporting evidence; ordinary procedural statements about what was attempted may be recorded directly in the reproduction report unless the package contradicts them.

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

**Where it lives:** In eval mode, compare the claim and reproduction comments with the issue context and every applicable repository convention or contribution requirement recorded in the repo-facts block. In live mode, check the draft comments against the issue thread, contribution documentation, templates, AI-use policies, and other stated repository requirements that apply.

**What good looks like:** The comments are specific to the issue and comply with applicable repository requirements. If the repository requires AI-assistance disclosure for issue comments or other comments, the required disclosure must appear in the candidate comments; missing a required disclosure is not compliant. A claim posted before reproduction should state what the contributor intends to investigate and report rather than claiming results that have not yet been observed.

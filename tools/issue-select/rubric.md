# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check               | Evidence                                                                                                                   | Pass condition                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Weight   |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| maintainer-active   | Repo-facts block: last 5 default-branch commit dates and authors; maintainer first-response sample                         | Pass if there is at least one non-bot default-branch commit within 90 days of the capture date OR the maintainer first-response sample shows a maintainer response within 30 days.                                                                                                                                                                                                                                                                                                                          | required |
| repo-in-use         | Repo-facts block: archived flag, latest release date, and last push to any branch                                          | Fail if the repository is archived. Otherwise pass if the latest release or last push occurred within 180 days of the capture date.                                                                                                                                                                                                                                                                                                                                                                         | required |
| newcomer-scope      | Issue body and comment thread, including linked or mentioned prior PR attempts                                             | Pass if the issue describes a finite, concrete deliverable or one cohesive set of related edits with enough direction to start. Multiple files or subtasks may still pass when they serve one stated goal. Fail if the issue is explicitly an umbrella or tracking issue meant to be split into separate work, is a pure support question, has unresolved design or product debate with no settled direction, or a maintainer states that the fix requires core-internal changes unsuitable for a newcomer. | required |
| unclaimed           | Repo-facts block: this issue's assignees and linked PRs; issue comment thread for explicit claim comments or mentioned PRs | Pass if the issue has no assignee and no open linked or mentioned PR showing active work. In normal live use, also fail on a recent explicit claim comment unless the scope file says to ignore classroom claims.                                                                                                                                                                                                                                                                                           | required |
| contribution-policy | Repo-facts block: contribution policy; CONTRIBUTING.md, AI policy files, and PR/issue templates when listed                | Pass if the repository does not ban AI-assisted contributions. Policies requiring disclosure, testing, understanding, or human review still pass; silence also passes.                                                                                                                                                                                                                                                                                                                                      | required |
|                     |                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |          |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept an issue only if every required check passes. Any failed required check rejects the issue. If the available evidence is insufficient to determine whether a required check passes, treat `unclear` as fail. Preferred checks, if added later, may affect ranking among accepted issues but never change the accept/reject verdict.

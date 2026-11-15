# Standardizing Error Formatting in Rafter CLI's Backend Commands

## Overview

Rafter CLI provides security tools that developers and AI agents can use through a command-line interface. Consistent error formatting matters because predictable error messages help scripts and AI agents parse errors reliably. The backend commands handled errors inconsistently across Node.js and Python. Some commands printed raw error messages instead of passing them through the shared formatter. I standardized error formatting for the `run`, `get`, and `usage` backend commands in both implementations. I also added regression tests and updated the CLI specification. Both full test suites passed in separate isolated Docker containers. After the maintainer reviewed my contribution, I addressed the feedback by updating Node.js so quiet mode reports quota errors consistently with Python. [PR #341](https://github.com/Raftersecurity/rafter-cli/pull/341) was successfully merged into upstream `main` on November 14, 2026, after I addressed the maintainer's feedback.

## What happened

### Choosing and investigating the issue

I chose Rafter CLI issue #34 because it was open, unassigned, and appeared manageable given my experience with Node.js and Python. I initially expected a straightforward formatting change, but investigating the backend commands revealed more complexity. Some Node.js commands printed unformatted errors, while Python used a mixture of plain messages and `Error:` prefixes. I also learned that `fmt.error()` returns a formatted string rather than printing it, and not every `console.error()` call was a bug because some printed progress or status messages. I decided to focus on the `run`, `get`, and `usage` backend commands in both implementations rather than changing every command.

### Implementation and testing — October 29–30

I updated these backend commands to use the shared error formatter and added regression tests and CLI specification changes. For example, this is an excerpt from my change to `node/src/commands/backend/get.ts`:

```diff
- console.error(`Scan '${scan_id}' not found`);
+ console.error(fmt.error(`Scan '${scan_id}' not found`));
```

During Docker testing, some unreadable-file tests initially failed because of container permissions. After troubleshooting the environment and running the tests as non-root users, both full test suites passed. Before opening the PR, I used Claude Code to help prepare and assess the draft, then manually reviewed the file changes and draft to make sure I understood what I was publishing. I opened PR #341 on October 30 (Hawaii time).

### Retrospective reproduction — November 6

After opening the PR, I compared the original CLI with my updated implementation using a local HTTP 404 fixture in isolated Docker containers. These are the actual recorded results for the Node.js `get` command in agent mode:

```text
Baseline (45b5fc1)
stderr: Scan 'does-not-exist' not found
exit code: 2

Updated implementation (34f3b8c)
stderr: [ERROR] Scan 'does-not-exist' not found
exit code: 2
```

My implementation added the expected `[ERROR]` prefix in agent mode without changing the exit code. This showed that the error-handling path used the shared formatter instead of printing the raw message. Preserving the exit code matters because scripts may depend on it to recognize a particular failure. This reproduction was performed after the first PR, not before I implemented the change, and it directly demonstrates only this Node.js `get` 404 path.

### Maintainer feedback and revisions — November 12–13

The maintainer confirmed that routing backend errors through `fmt.error()` and formatting HTTP errors as `HTTP <status> — <detail>` matched their expectations. However, they requested several changes before merging, including printing quota errors in quiet mode, clarifying documentation, addressing changes that went beyond the original scope, and rebasing onto the latest `main` branch.

I updated Node.js to print the quota error in quiet mode while preserving exit code 3, corrected the explanation of HTTP 403 behavior, explained why the `scan-status.ts` changes were intentional, reused an existing test helper, and rebased onto upstream `main`. I also updated the existing regression test to check that quiet mode still prints the error:

```ts
expect(exitCode).toBe(EXIT_QUOTA_EXHAUSTED);
expect(lines).toEqual(["[ERROR] Quota exhausted"]);
```

After addressing the feedback, I reran both full test suites in Docker and reported 2,487 passing Node.js tests and 2,066 passing Python tests, plus 231 passing Python subtests. I pushed the updates and replied to the maintainer. At the time of submission, the PR was still awaiting further review.

### Merge outcome — November 14

On November 14, 2026, my [PR #341](https://github.com/Raftersecurity/rafter-cli/pull/341) was successfully merged into Rafter CLI's upstream `main` branch after I completed Assignment 6.

The merged contribution standardizes error formatting in the Node.js and Python backend commands, adds regression tests, and updates the CLI specification.

The original [issue #34](https://github.com/Raftersecurity/rafter-cli/issues/34) remains open because my pull request addresses only the backend commands, not every command covered by the broader issue.

This completed my first merged contribution to Rafter CLI and gave me experience working through maintainer feedback, revising my implementation, and validating the changes before merging.

## Limitations and what's next

My contribution covers the `run`, `get`, and `usage` backend commands, not every command in issue #34. Other error and status messages would need to be investigated individually before changing them.

If I continued working on Rafter CLI after this assignment, I would improve how I start the next issue. I would verify that my development environment is properly configured and run the existing test suites before making any code changes. I would approach environment issues more systematically and avoid repeatedly troubleshooting the same problem without identifying its root cause. Looking back, I realized that I made more changes than I initially expected for this issue, so I would focus on smaller, more targeted changes in future contributions.

---
name: explain-branch
description: Explain how a local Git feature branch or current working-tree implementation works, from user-visible behavior through its important code paths and tests. Use for teaching-oriented branch walkthroughs and implementation handoffs; do not use for defect-first reviews, code-quality audits, or requests to fix the branch.
---

# Explain Branch

Teach the user how the selected implementation works. Connect product behavior to the code that produces it, without turning the walkthrough into a review.

## Invocation

Accept at most one optional argument:

```text
$explain-branch [local-branch]
```

Treat any supplied value as an exact local branch name. If more than one argument is supplied, explain the accepted form and stop successfully.

## Resolve the target without changing Git state

Remain read-only. Do not fetch, checkout, switch, create, edit, format, commit, push, or publish anything.

1. Confirm the current directory is a Git worktree. If not, ask the user to run the skill in a repository.
2. Detect the default branch from the local `refs/remotes/origin/HEAD` symbolic ref. If unavailable, fall back to a local `main` branch, then a local `master` branch. If none can be resolved, explain that the comparison base could not be determined and stop.
3. If an argument was supplied, verify that `refs/heads/<argument>` exists. Do not accept a remote-tracking branch, tag, raw commit, or similarly named revision. If it does not exist, ask for an existing local branch name.
4. If no argument was supplied, resolve the current symbolic branch:
   - When it is not the detected default branch, select it.
   - When it is the default branch, select its working tree only if staged, unstaged, or untracked changes exist.
   - For detached HEAD, or a clean default branch, ask the user to provide or switch to a local branch with changes.
5. Compute the merge base between the selected local branch and the detected default ref. Use the merge-base-to-selected-branch diff as the committed change that would merge.
6. Include staged, unstaged, and untracked changes only when the selected branch is currently checked out. Keep them visibly separate from committed branch changes. Inspect untracked files directly because ordinary Git diffs omit them.
7. If neither committed differences nor applicable working-tree changes exist, stop successfully and ask the user to provide or switch to a local branch with changes.

Use safe Git inspection commands such as `git symbolic-ref`, `git show-ref --verify`, `git merge-base`, `git diff`, `git status --short`, `git ls-files --others --exclude-standard`, and `git show`. Quote branch and path arguments safely, and use `--` before paths.

## Understand the implementation

Read applicable repository instructions, including a neighboring ignored `AGENTS.local.md` when present. Inspect the complete selected diff, then read enough surrounding code, call sites, tests, configuration, schemas, and types to understand the changed behavior. Follow important execution paths beyond changed lines when necessary.

Identify the branch's central behavior and organize the explanation around how it runs, not around an exhaustive file list. Adapt the depth and vocabulary to the implementation: frontend, backend, infrastructure, documentation, and refactoring branches need different structures.

Do not hunt for defects, assign severities, give a quality verdict, or recommend unsolicited fixes. If behavior is surprising, explain factually what the code does and where that behavior comes from.

## Reinforce the developer's mental model

Assume the user is an experienced developer who wants to remain actively involved in AI-generated implementation. Do not teach basic programming or define familiar artifacts such as controllers, services, routes, components, migrations, or tests unless their use here is unusual.

Explain the implementation in two passes when useful:

1. Establish the architectural map: where the behavior begins, how control and data move, which layer owns each decision, and where the important boundaries are.
2. Trace the core implementation closely enough that the user can follow its meaningful conditions, transformations, state changes, and failure paths without reconstructing them from the diff.

Reinforce engineering concepts through their role in this code. Name relevant concepts such as separation of concerns, dependency injection, state ownership, transactional boundaries, invariants, or defense in depth, then explain why each matters here and what tradeoff or boundary it creates. Repeat a concept concisely when it helps preserve the mental model; do not assume a prior walkthrough made repetition unnecessary.

Prefer peer-level explanations such as “this controller keeps HTTP concerns at the boundary and delegates account resolution.” Avoid generic definitions such as “a controller handles HTTP requests.” Do not merely report that a file or method was added: explain why this implementation needs it, what responsibility it owns, and how it connects to the rest of the flow.

## Calibrate depth by importance

Account for every changed file, but classify it by its importance to understanding the branch:

- **Core:** behavior-defining execution paths, state transitions, business rules, interfaces, and security or data-integrity boundaries. Walk these through closely and explain the important lines and conditions in execution order.
- **Supporting:** configuration, wiring, schemas, types, migrations, resources, and tests that enable or constrain the core behavior. Explain their architectural role and the relevant changes without narrating routine syntax.
- **Mechanical:** generated files, lockfiles, snapshots, formatting, and repetitive changes. Summarize these unless a specific change affects behavior.

Spend the most attention on the smallest set of changes the user must understand to reason confidently about the feature. Explicitly account for summarized files so the user knows they were inspected rather than overlooked. “Line by line” means tracing meaningful behavior and decisions, not reciting imports, braces, type annotations, or generated output.

## Write the walkthrough

Lead with a short statement of what the branch makes possible for the user or system, followed by what it does not implement.

When several layers or stages interact, show a compact text flow before discussing details. Then walk through the implementation in runtime or data-flow order:

- group files by responsibility rather than listing every changed file;
- highlight only the core files and link to exact local paths and relevant line numbers;
- quote small, central code blocks rather than reproducing large sections;
- trace what each important block does, why its boundary or abstraction exists, and what it passes to the next stage;
- connect validation, state, persistence, configuration, authentication, error handling, and external boundaries when they actually participate;
- explain how the change reuses or alters existing application behavior;
- use precise, plain language at an experienced-developer level, explaining unfamiliar or unusually applied concepts in context.

Treat tests as executable examples of the behavioral contract. Explain the important scenarios they cover and what those scenarios demonstrate. Distinguish clearly among:

- test or verification code merely present in the branch;
- checks actually executed during this walkthrough;
- manual, device, deployment, or external validation.

Never claim a check passed unless its result was observed in the current task or provided as trustworthy evidence. End with concise sections for verification evidence and for work that is not included or remains outstanding. If the selected branch has applicable uncommitted work, remind the user which explained behavior is not yet committed.

---
name: orchestrate
description: >
  Coordinate bounded independent assignments with Codex subagents while keeping
  decisions and synthesis in the parent. Use when the user asks to orchestrate
  or parallelize, independent work would crowd the parent context or consume
  disproportionate parent-model effort, useful parallel progress is available,
  or a consequential change benefits from independent review. Skip delegation
  when coordination and synthesis overhead would outweigh the benefit.
---

# Orchestrate

This skill requires Codex subagent tools and suitable runtime-configured roles.
Role definitions and model configuration are not bundled or installed by this
skill. Check the active runtime's available roles and capacity before delegating;
use the fallback below when a role is unavailable. Other harnesses need an
adapted version with their own tools and role configuration.

Keep scope, decisions, approvals, integration, and the final result with the parent.
Delegate bounded independent work when doing so improves evidence, quality, useful
parallel progress, parent-context quality, or avoids disproportionate use of an
expensive parent model.

Optimize for reliable completion with low rework. Weigh delegation, integration,
verification, and likely rework together with model usage and completion time.
Use a single agent when delegation would add more overhead than value.

Use the runtime-configured implementation role for delegated code, test,
configuration, and migration changes, including narrow or low-risk edits. Recommend
a high-capability coding model for that role. Reserve lightweight models for
bounded read-only research, such as retrieval, inventories, and straightforward
code tracing. Delegation can reduce expensive parent-model usage, but does not
guarantee fewer total tokens or lower account usage.

Keep tightly coupled reasoning, ambiguous decisions, and synthesis with the parent.
Avoid overlapping work, duplicated reasoning, and assignments whose prompt and
synthesis overhead approaches the work itself.

## Assignments and concurrency

- Usually use one or two children; use more only for distinct useful assignments.
- Respect the active runtime's concurrency limit. Available capacity is a ceiling, not a target; run assignments in successive batches when needed.
- Keep delegation to one level. Every child completes its assignment directly without spawning others.
- Use `fork_turns: "none"`. Supply the assignment, necessary context, output criteria, and task-specific tool or safety restrictions.
- Include in each child prompt: `Complete this assignment directly. Do not spawn other agents.`
- Give each assignment one owner. Default to one implementation owner at a time across the parent and all children. Independent read-only work may accompany implementation when it does not depend on changes still in progress.
- Allow concurrent implementation only when the parent establishes independent scopes before edits begin: separate file ownership, settled shared interfaces, and no concurrent changes to shared configuration, dependencies, or migrations. This applies equally to parent-child and child-child work. Never overlap writes. Keep coupled work with one implementer; separate worktrees can isolate edits but do not establish independence.
- The parent owns integration and verification of the combined result, including when children implement in separate worktrees.
- Use runtime-configured roles according to the responsibilities below.
- Reuse an existing agent for bounded follow-up work when its context remains relevant. If an assignment is blocked or repeatedly returns insufficient evidence, bring it back to the parent to resolve the missing requirement, access, or capability rather than spawning repeated retries.

## Handoffs and verification

Require a concise handoff with the result, evidence or changed files, checks
performed and their outcomes, and unresolved issues. Return useful references
and material uncertainty rather than raw exploration or test logs.

The implementation owner runs focused checks for its changes. The parent examines
the resulting diff, resolves integration issues, and confirms the combined
behavior with appropriate checks. Reuse valid verification evidence; repeat or
broaden checks when integration changes, failures, or unresolved concerns justify
it.

Use independent review for meaningful correctness, security, or regression risks.
Give the reviewer the requirements and relevant artifacts, and ask it to assess
them independently rather than endorse the implementer's conclusions. Review
does not replace testing or user approval.

## Model and role selection

Treat the active runtime's role definitions, model assignments, and reasoning
settings as authoritative. The roster describes responsibilities, not fixed model
or reasoning settings. Choose a role suited to the assignment's difficulty and
consequences; read-only work can still require substantial capability. Within
these constraints, consider cost only when it does not materially reduce quality.
Do not downgrade implementation or consequential judgment merely to save
parent-model usage.

Prefer a lightweight role for bounded checks with concrete evidence, such as
tracing callers, comparing schema constraints, or verifying deployment order.
Use a higher-capability reviewer for independent defect discovery across
interacting code paths or for judgment about a consequential edge case.
Before choosing a role configured for medium or higher reasoning, identify the
specific difficulty that warrants it. If a bounded check surfaces a question
that needs deeper reasoning, escalate that question with the evidence already
gathered.

- `explorer` — Inventories, locating code, tracing execution paths, and gathering evidence.
- Implementation role (commonly `worker`) — Bounded code, test, configuration, and migration changes, reproduction, and focused verification. Use the role the runtime designates for implementation.
- `analyst` — First-pass evidence synthesis into a bounded decision.
- `reviewer` — Difficult targeted correctness, security, and regression review.
- `specialist` — Independent analysis of a difficult, consequential question when it adds value beyond the parent's reasoning.

Preserve the runtime-configured defaults rather than overriding them from this
skill. If a required role is unavailable in this session, keep the assignment
with the parent or use a suitable available role that meets the same capability
requirements. Do not invent a role or tool capability.

## Synthesis

Combine findings into one coherent result with evidence and material uncertainty.
Resolve disagreements against the underlying sources. Keep approval decisions
with the user and report blocked assignments honestly. Avoid additional agents
or repeated checks once the requested evidence is sufficient.

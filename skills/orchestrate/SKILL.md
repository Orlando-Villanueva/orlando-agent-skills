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

This skill requires Codex subagent tools and the configured roles listed below.
Role definitions and model configuration are not bundled or installed by this
skill. Check the active runtime's available roles and capacity before delegating;
use the fallback below when a role is unavailable. Other harnesses need an
adapted version with their own tools and role configuration.

Keep scope, decisions, approvals, integration, and the final result with the parent.
Delegate bounded independent work when doing so improves evidence, quality, useful
parallel progress, parent-context quality, or avoids disproportionate use of an
expensive parent model.

Prefer an appropriately capable GPT-6 Luna child for self-contained retrieval,
inventories, straightforward code tracing, reproduction, verification, and narrow
low-risk implementation when the delegation overhead is smaller than doing the work
in the parent. Use GPT-6.1 Sol selectively when an assignment needs difficult reasoning,
independent confirmation, or a high-consequence correctness judgment. This can
reduce expensive parent-model usage, but does not guarantee fewer total tokens or
lower account usage.

Keep tightly coupled reasoning, ambiguous decisions, and synthesis with the parent.
Avoid overlapping work, duplicated reasoning, and assignments whose prompt and
synthesis overhead approaches the work itself.

## Assignments and concurrency

- Usually use one or two children; use more only for distinct useful assignments.
- The configured ceiling is five concurrent children, subject to the active runtime's capacity. It is a ceiling, not a target. If capacity is lower, use fewer children or run assignments in successive batches.
- Keep delegation to one level. Every child completes its assignment directly without spawning others.
- Use `fork_turns: "none"`. Supply the assignment, necessary context, output criteria, and task-specific tool or safety restrictions.
- Include in each child prompt: `Complete this assignment directly. Do not spawn other agents.`
- Give each assignment one owner. Do not overlap writes or parallelize implementation, including between parent and child. Independent read-only work may accompany one implementation owner.
- Use named agents from the roster below. Do not automatically use GPT-6.1 Sol for ordinary
  delegated work; reserve it for the difficult or consequential assignments
  described below.

## Model and role selection

Choose by the assignment's difficulty and consequences, not merely whether it is read-only.
Among roles capable of completing the assignment without material quality loss, prefer
the least expensive configured role and effort. Do not downgrade consequential judgment
merely to save parent-model usage.

- `explorer` — GPT-6 Luna High for inventories, locating code, tracing execution paths, and gathering evidence.
- `worker` — GPT-6 Luna High for bounded implementation, reproduction, and focused verification, including narrow edits.
- `analyst` — GPT-6 Luna High for first-pass evidence synthesis into a bounded decision.
- `reviewer` — GPT-6.1 Sol Medium for difficult targeted correctness, security, and regression review.
- `specialist` — GPT-6.1 Sol Medium for independent analysis of a difficult, consequential question when it adds value beyond the parent's reasoning.

Preserve these configured defaults. Further effort increases beyond a role's
baseline are an exception for demonstrated unresolved difficulty, not a routine
escalation. If a required role is unavailable in this session, keep the assignment
with the parent or use a suitable available role; do not invent a tool capability or
silently substitute a stronger model.

## Synthesis

Combine findings into one coherent result with evidence and material uncertainty.
Resolve disagreements against the underlying sources. Keep approval decisions
with the user and report blocked assignments honestly. Avoid additional agents
or repeated checks once the requested evidence is sufficient.

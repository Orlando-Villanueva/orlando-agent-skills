---
name: shape-issue
description: Shape or refine a work issue so its outcome, acceptance criteria, scope, and constraints are precise while implementation choices remain open for later collaboration. Use when preparing an issue for progressive implementation rather than writing a complete technical plan.
---

# Shape Issue

Create an issue that is **outcome-bounded and implementation-open**. It should tell a future implementer what must be true when the work is complete without prematurely deciding how the code or other implementation should be organized.

Use the user's tracker and its conventions when one is available. Keep the workflow independent of any particular tracker, agent harness, repository stack, or delivery process. Draft locally when no tracker is available. Publishing or modifying an external issue still requires the user's authorization.

## Shape the work

1. Establish the problem, intended outcome, affected users or systems, and why the work matters.
2. Clarify only ambiguities that materially change scope, behavior, acceptance, or non-negotiable constraints. Do not turn issue shaping into implementation planning.
3. Separate the available information into:
   - **settled decisions** that the implementation must preserve, with compact rationale and source context when a constraint is non-obvious;
   - **observable requirements** that define success;
   - **implementation questions** to resolve later against the real environment;
   - **suggestions or context** that may inform the implementation but are not requirements.
4. Write acceptance criteria that are observable and sufficient to judge completion. Include important exclusions, compatibility requirements, and failure behavior when they matter.
5. Check that the issue is bounded enough to begin work but does not prescribe a file sequence, internal names, commit plan, or architecture that has not actually been decided.

Do not erase technical decisions the user has already made. Record them as constraints. For a non-obvious constraint whose relaxation would materially change compliance, safety, compatibility, user access, coordination, or scope, include the minimum useful provenance: why it exists, what consequence it prevents or enables, and the authoritative source or parent decision when available. Keep this to a sentence or short clause, and link to deeper context instead of copying parent discussion. A parent link supplements but does not replace the rationale; a future implementer should not need to consult the parent merely to explain why an in-scope constraint exists. Omit rationale that would not affect an implementation or scope decision.

## Deliver the issue

Follow existing tracker or team conventions instead of imposing a universal template. When no convention is available, a compact issue will usually cover:

- outcome and context;
- acceptance criteria;
- scope and exclusions;
- settled constraints or decisions;
- open implementation questions, only when they are already known.

Before publishing, distinguish missing requirements from intentionally open implementation choices. Check that a future implementer can explain why each non-obvious in-scope constraint exists and what would be at risk if it were relaxed, while unrelated parent history remains omitted. Ask for confirmation when publishing would create or materially change an external issue.

If the user explicitly asks to use the environment's persistent goal mechanism, store the outcome and acceptance criteria as the goal. Do not use the goal to freeze a step-by-step implementation plan.

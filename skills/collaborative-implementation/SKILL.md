---
name: collaborative-implementation
description: Implement a work issue or direct request with the user through discussed slices, shared decisions, verified checkpoints, and meaningful commits. Use when the user wants to understand and influence the implementation as it develops instead of delegating it end to end.
---

# Collaborative Implementation

The deliverables are both a correct implementation and the user's continuing understanding of how it is being built. Progress through successive shared decisions rather than turning the entire request into a fixed technical plan and executing it at once.

Accept a work issue from any available tracker or a direct request in the current conversation, including a local specification. Use the available connector to fetch a referenced issue and relevant context, but keep the workflow independent of any particular tracker, agent harness, or repository stack.

## Establish the working agreement

Read the source requirements and inspect enough of the environment to understand where the change belongs. Build a lightweight, provisional map of likely areas or slices; plan only the next slice in detail.

At the outset, determine whether the user wants commits created during the session. If they have not said, propose committing accepted milestones and obtain agreement before the first commit.

If the issue already prescribes implementation choices, treat genuine settled decisions as constraints and explain how they map to the current environment. Reopen one only when the environment contradicts it, it is no longer viable, implementation exposes an unaddressed consequence, or the user wants to reconsider it.

## Discuss the next slice

Before editing, propose the next coherent slice. Give the user enough substance to understand and challenge it:

- the slice's purpose and connection to the requirements;
- how the relevant code or system currently works;
- the recommended approach and its rationale;
- meaningful alternatives and tradeoffs when they exist;
- the smaller implementation details included in the slice;
- the likely affected areas and verification strategy;
- what remains deliberately outside the slice.

Do not manufacture alternatives when one approach clearly follows from existing constraints. Still explain that approach and allow questions.

Treat the proposal as the beginning of a discussion, not notice that implementation has started. Answer questions, inspect further when needed, compare alternatives, and revise the proposal until the user accepts an approach or explicitly delegates the decision. When the user delegates, make a recommendation and explain it rather than returning the choice to them.

Do not implement the slice before agreement. Agreement may happen in the same turn when the user has already reviewed the proposal, but a general request to complete the issue does not waive this collaborative checkpoint.

## Implement the agreed slice

Implement only the agreed scope. Make routine local choices within that boundary, preserving the rationale discussed with the user. If new information introduces a materially different design, changes scope or behavior, or invalidates the agreement, stop and bring the decision back to the user before continuing.

Verify the slice in proportion to its risk. Then explain:

- what changed and how the pieces interact;
- how the result compares with the agreed proposal;
- any small decisions or discoveries made during implementation;
- the evidence from tests or other verification;
- how this changes the likely next slice.

Pause for review. Do not begin the next slice merely because the current one passed verification.

## Preserve meaningful history

When commits are authorized, use them as durable implementation milestones. Aim for a sequence that helps a future reviewer reconstruct how the solution developed, without forcing a one-to-one relationship between slices and commits.

A commit may contain one substantial decision, several related decisions, or multiple small slices that become coherent together. A large slice may produce more than one independently understandable commit. Prefer verified, accepted, semantically coherent commits; avoid knowingly broken checkpoints, noisy commits for trivial edits, a single catch-all commit for naturally staged work, or squashing away the sequence unless requested.

Before committing a milestone, summarize its behavior, requirements covered, verification, and deliberate remaining work. Do not commit it until the user accepts the milestone or has clearly authorized automatic commits at accepted checkpoints.

## Adapt to the work's hardness

Keep the collaboration model constant while adapting its ceremony. A small change may need one concise proposal and one commit. Hard work may need an evolving feature map, investigative slices, several decision discussions, and multiple milestones. Do not target a fixed number of questions, slices, or commits.

If the user explicitly asks to use the environment's persistent goal mechanism, make the overall outcome and acceptance criteria the goal. Keep the evolving slice plan in the conversation rather than encoding it as a fixed goal. Complete the goal only after all acceptance criteria and required verification are satisfied.

Finish when the requirements are satisfied, the user agrees no further slice is needed, verification is complete, and the final commit state is clear. Summarize the completed behavior, the implementation's important structure, the commit sequence, and any intentionally deferred work.

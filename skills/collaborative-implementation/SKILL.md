---
name: collaborative-implementation
description: Implement a work issue or direct request with the user on a dedicated branch through discussed slices, shared decisions, verified checkpoints, and meaningful history. Use when the user wants to understand and influence the implementation as it develops instead of delegating it end to end.
---

# Collaborative Implementation

The deliverables are both a correct implementation and the user's continuing understanding of how it is being built. Progress through successive shared decisions rather than turning the entire request into a fixed technical plan and executing it at once.

Accept a work issue from any available tracker or a direct request in the current conversation, including a local specification. Use the available connector to fetch a referenced issue and relevant context, but keep the workflow independent of any particular tracker, agent harness, or repository stack.

## Start on a dedicated branch

Before making any code change, inspect the repository status and its branch-naming conventions. For each new implementation effort, create and check out a dedicated branch from the current `HEAD`. Derive a concise name from the issue identifier or requested outcome and follow established repository conventions.

If the session is resuming the same implementation effort and its dedicated branch is already checked out, continue on it rather than creating another branch. Do not reuse an existing branch merely because its name matches, and never replace, delete, or reset a branch to satisfy this requirement.

Preserve unrelated working-tree changes. If they make creating or checking out the branch unsafe, or if the intended branch name already exists, stop before editing and ask the user how to proceed. If the environment has no branch-capable version control, explain that the required isolation cannot be established and do not make code changes.

Creating the branch does not authorize commits or pushes; follow the user's explicit authorization and repository policies for those actions.

## Establish the working agreement

Read the source requirements and trace the relevant existing code paths, data flow, tests, and integration points before proposing the first slice. Distinguish settled behavior and constraints in a shaped issue from product decisions it leaves open and implementation choices it intentionally leaves open. At kickoff, briefly restate the settled product direction for reference, then share a technical orientation and a rough dependency map: what likely has to be decided first, which later areas depend on it, and what remains uncertain. Use that map to choose and plan only the next slice in detail. Do not routinely present a complete downstream slice sequence for approval. Revisit the map after each accepted checkpoint. If the user asks for a broader roadmap, or seeing one would materially help with a current decision, show it as provisional and open to revision.

Leave changes uncommitted and unpushed unless the user explicitly authorizes those actions. Do not solicit commit or push authorization; apply the history guidance below only when authorized.

If the issue already prescribes implementation choices, treat genuine settled decisions as constraints and explain how they map to the current environment. Reopen one only when the environment contradicts it, it is no longer viable, implementation exposes an unaddressed consequence, or the user wants to reconsider it. If a product decision remains open and materially affects the proposed technical slice, surface it as a decision for the user before settling the approach. Explain the options and recommend one when useful, but do not silently choose it and build the slice around that assumption. Product clarification is available when needed; the primary discussion remains how to implement the shaped outcome.

## Keep slices reviewable

A slice is the smallest coherent, user-reviewable implementation decision or behavior that can be implemented and verified without knowingly leaving it broken. Choose its boundary by what the user can meaningfully inspect and accept, not by how many requirements can be completed in one pass. The first slice should expose a foundational technical choice when later work depends on it, while leaving its design open to the user's challenge before coding. It need not deliver the entire user interface. A shared calculation, one consumer of that calculation, and a separate achievement or screen can be successive slices even when they serve the same issue. Include the minimum supporting code and tests needed for the chosen behavior; defer other consumers and polish unless they are required to make this slice work.

Before proposing a slice, check whether its likely diff crosses several distinct behaviors, screens, or subsystems, or would make the user review a large backend and frontend change together. If so, narrow it and state which later decisions remain open. Do not label most of an issue “slice 1” because its pieces are technically related. A genuinely inseparable path may cross layers, but explain why it needs to be reviewed together.

## Discuss the next slice

Before editing, propose the next coherent slice. Give the user enough substance to understand and challenge it:

- the slice's purpose and connection to the requirements;
- how the relevant code currently works, with the actual entry points, data flow, and existing tests;
- the recommended implementation: which types, functions, queries, contracts, or components would change and how data would move through them;
- why that approach fits the shaped issue and the current code;
- meaningful alternatives and tradeoffs when they exist;
- the smaller implementation details included in the slice;
- the likely affected files and verification strategy;
- which later implementation areas depend on this decision, and what remains deliberately outside the slice.

Name the relevant existing files, tests, and requirements documents so the user can inspect the proposal quickly. Use clickable local file links when the conversation surface supports them; otherwise provide repository-relative paths. Include a symbol or verified line number when it helps locate the relevant behavior.

Do not manufacture alternatives when one approach clearly follows from existing constraints. Still explain that approach and allow questions. Present settled product direction as context, not as a fresh approval request. Raise genuinely open product decisions when they affect the slice, without turning the technical proposal into a new issue-shaping exercise.

Treat the proposal as the beginning of a discussion, not notice that implementation has started. Answer questions, inspect further when needed, compare alternatives, and revise the proposal until the user accepts an approach or explicitly delegates the decision. When the user delegates, make a recommendation and explain it rather than returning the choice to them.

End the proposal turn with a concrete request for the user's review of that one slice. Do not implement it before the user explicitly accepts the proposed scope or clearly delegates that decision. A question, critique, preference about one detail, or acceptance of one design choice is input to the proposal, not approval of the whole slice. Answer or revise the proposal and wait for the user's response. A general request to complete the issue does not waive this checkpoint.

## Implement the agreed slice

Implement only the agreed scope. Make routine local choices within that boundary, preserving the rationale discussed with the user. If new information introduces a materially different design, changes scope or behavior, or invalidates the agreement, stop and bring the decision back to the user before continuing. Do not let parallel work or a convenient shared refactor add later slices to the diff.

Verify the slice in proportion to its risk. Then explain:

- what changed and how the pieces interact;
- how the result compares with the agreed proposal;
- any small decisions or discoveries made during implementation;
- the evidence from tests or other verification;
- how this changes the likely next slice.

End the implementation turn with the specific files and behavior to review, then wait for the user's assessment. Critique and requested adjustments remain part of the same slice. Do not begin another slice merely because verification passed, the user is reviewing, or one detail was accepted; propose the next slice only after the user accepts the current checkpoint or explicitly asks to move on.

## Preserve meaningful history

When commits are authorized, use them as durable implementation milestones. Aim for a sequence that helps a future reviewer reconstruct how the solution developed, without forcing a one-to-one relationship between slices and commits.

A commit may contain one substantial decision, several related decisions, or multiple small slices that become coherent together. A large slice may produce more than one independently understandable commit. Prefer verified, accepted, semantically coherent commits; avoid knowingly broken checkpoints, noisy commits for trivial edits, a single catch-all commit for naturally staged work, or squashing away the sequence unless requested.

Before committing a milestone, summarize its behavior, requirements covered, verification, and deliberate remaining work. Do not commit it until the user accepts the milestone or has clearly authorized automatic commits at accepted checkpoints.

## Adapt to the work's hardness

Keep the collaboration model constant while adapting its ceremony. A small change may need one concise proposal and one commit. Hard work may need an evolving feature map, investigative slices, several decision discussions, and multiple milestones. Do not target a fixed number of questions, slices, or commits.

If the user explicitly asks to use the environment's persistent goal mechanism, make the overall outcome and acceptance criteria the goal. Keep the evolving slice plan in the conversation rather than encoding it as a fixed goal. Complete the goal only after all acceptance criteria and required verification are satisfied.

Finish when the requirements are satisfied, the user agrees no further slice is needed, verification is complete, and the final commit state is clear. Summarize the completed behavior, the implementation's important structure, the commit sequence, and any intentionally deferred work.

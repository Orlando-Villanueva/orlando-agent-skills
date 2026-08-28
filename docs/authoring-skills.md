# Authoring skills

## What belongs here

A skill should describe a reusable way for an agent to make decisions or carry
out work. It should have a clear trigger, a concrete user benefit, and
instructions that still make sense outside the environment in which it was
first written.

## Keep the contract portable

- Put every installable skill in `skills/<name>/SKILL.md`.
- Use a lowercase, hyphenated directory name that exactly matches the YAML
  `name` value.
- Write a description that says when the skill should be used.
- State outcomes and decision boundaries before prescribing mechanics.
- Mark an integration as optional when it depends on a particular host,
  connector, tracker, or repository convention.

## Review checklist

Before submitting a change, confirm that:

- the skill is independently understandable and installable;
- its instructions do not silently authorize external writes or publishing;
- requirements are observable where the skill defines a deliverable;
- any referenced files or tools are either portable or explicitly optional;
- `./scripts/validate-skills` passes.
## Evolving a skill

Prefer small changes supported by a real use case. Preserve behavior users may
already rely on, explain incompatible changes in the pull request or release
notes, and keep a harness-specific variant out of the core skill unless that
dependency becomes a deliberate compatibility commitment.

# Orlando Agent Skills

Portable, outcome-oriented skills for agents that work with people rather than
around them. Each skill is a standalone directory containing a `SKILL.md` file
with YAML front matter and Markdown instructions.

## Included skills

### `shape-issue`

Shapes work into a bounded, implementation-open issue. Use it to establish an
outcome, observable acceptance criteria, scope, constraints, and genuinely
open implementation questions before delivery begins.

### `collaborative-implementation`

Implements a direct request or shaped issue through shared decisions, coherent
slices, verification, and (when authorized) meaningful commits. It preserves
the user's understanding alongside the implementation.

The skills are intentionally independent. `shape-issue` is a useful upstream
companion when work is not yet clear; `collaborative-implementation` can begin
from any sufficiently clear request or issue.

### `explain-branch`

Explains a local feature branch or its checked-out working-tree changes from
user-visible behavior through the relevant code paths and tests. It is for
teaching-oriented implementation walkthroughs, rather than defect-first review
or repair work.

### `html-media-design`

Creates posters, feature graphics, announcement images, social cards, and other
exactly sized media as editable HTML/CSS rendered in a browser. Image generation
is an optional source for visual ingredients; final typography and composition
remain deterministic and reusable.

## Install

The recommended installer is the open `skills` CLI. Run the command for the
specific skill you want; it will guide you through choosing a supported agent
and install scope.

### `shape-issue`

```sh
npx skills add Orlando-Villanueva/orlando-agent-skills --skill shape-issue
```

### `collaborative-implementation`

```sh
npx skills add Orlando-Villanueva/orlando-agent-skills --skill collaborative-implementation
```

### `explain-branch`

```sh
npx skills add Orlando-Villanueva/orlando-agent-skills --skill explain-branch
```

### `html-media-design`

```sh
npx skills add Orlando-Villanueva/orlando-agent-skills --skill html-media-design
```

For a non-interactive, global installation into Codex, add `--global`, target
Codex with `--agent codex`, and accept the choices with `--yes`. For example:

```sh
npx skills add Orlando-Villanueva/orlando-agent-skills --skill shape-issue --global --agent codex --yes
```

If Node.js or the CLI cannot be used, manually copy a directory from `skills/`
into the configured skill location for your host. See the
[compatibility notes](docs/compatibility.md) for that fallback.

## Validate

The repository uses a dependency-free validator:

```sh
./scripts/validate-skills
```

It checks the portable repository conventions: each skill must have a
directory-matching `SKILL.md`, YAML front matter, a `name`, a `description`,
and a non-empty Markdown body. This is structural validation, not a claim that
every host will interpret every instruction identically.

## Contributing

Read [authoring guidance](docs/authoring-skills.md) before proposing a skill.
Keep skills specific enough to guide useful behavior, while avoiding harness,
tracker, or repository assumptions unless they are clearly declared as an
optional integration.

## License

This project is available under the [MIT License](LICENSE).

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

## Install one skill

Clone this repository, then copy or symlink only the skill directory your host
recognizes. For example, a host that reads skills from `~/.agents/skills`:

```sh
git clone https://github.com/Orlando-Villanueva/orlando-agent-skills.git
mkdir -p ~/.agents/skills
ln -s "$PWD/orlando-agent-skills/skills/shape-issue" ~/.agents/skills/shape-issue
```

To install `collaborative-implementation`, replace the directory name in both
places. Copying the directory instead of symlinking is equally valid and is
often better for immutable or managed environments.

See [compatibility notes](docs/compatibility.md) for the portable contract and
host-specific installation considerations.

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

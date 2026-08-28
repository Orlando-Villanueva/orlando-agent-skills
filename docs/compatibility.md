# Compatibility

## Portable contract

Every skill in this repository is self-contained in `skills/<name>/SKILL.md`.
The document begins with YAML front matter containing a stable `name` and a
short `description`, followed by Markdown instructions. Core skills do not
depend on a runtime, package manager, network connector, or repository stack.

This layout is designed for agent environments that discover or import a
directory containing `SKILL.md`. It is also simple to copy into a host's
configured skill directory.

Some skills may additionally include `agents/openai.yaml`. This is optional
OpenAI interface metadata for display and default-prompt integration; the
portable `SKILL.md` remains the core skill contract.

## Installation by host

Use the `skills` CLI for the normal path. It reads the repository's `skills/`
layout and installs a selected skill into a supported host:

```sh
npx skills add Orlando-Villanueva/orlando-agent-skills --skill <skill-name>
```

The CLI lets the user choose an agent and project or global scope. Consult the
host's documentation when its discovery location or managed-install policy is
unusual.

Manual copying is a fallback. Copy exactly one directory from `skills/` into
the host's configured skill location. For agents that use `~/.agents/skills`,
the destination is typically:

```text
~/.agents/skills/<skill-name>/SKILL.md
```

For Codex installations, the CLI target is `--agent codex`. A manual install
uses Codex's configured skills directory (commonly
`$CODEX_HOME/skills/<skill-name>/SKILL.md`) rather than assuming a particular
machine-wide path. A managed environment may need an administrator-approved
copy instead of a symlink.

## Compatibility principles

- A skill must remain useful when installed by itself.
- Core instructions must not require a particular tracker, shell, editor,
  repository layout, or provider connector.
- Harness-specific instructions belong in a separately named adaptation, not
  in the portable core.
- Optional tools may be mentioned conditionally, with a clear non-tool path.
- A new compatibility claim should be verified in that host before it is
  advertised as supported.

## Current scope

The repository validates the common on-disk format. It does not certify a
specific agent product or promise automatic discovery by every host.

# Skills

A small collection of public, provider-neutral skills for planning and coding work. Each skill is written as portable instructions rather than a dependency on a particular agent, tool API, ticketing system, or workspace layout.

## Layout

The canonical source for each skill lives at:

```text
skills/<name>/SKILL.md
```

This repository currently provides one skill:

- [`plan`](skills/plan/SKILL.md) — gathers requirements from the conversation and optional local files, examines relevant repositories, clarifies unresolved decisions, and writes a self-contained implementation plan.

## Using a skill

Copy or symlink a canonical skill directory into the location your coding-agent environment uses for local skills. For example, copy or link `skills/plan/` as a directory—not just its `SKILL.md` file—so future supporting files can remain alongside the skill.

Installation locations and invocation mechanisms vary by environment. Keep those environment-specific details outside the canonical skill; the instructions in `skills/plan/SKILL.md` are intentionally provider agnostic.

## Design policy

Skills in this repository should:

- use general capabilities such as reading files, searching repositories, and asking the user, rather than provider-specific APIs or commands;
- treat requirements in the conversation as the default input and support user-provided local files without requiring formal tickets or forms;
- follow project guidance and existing code conventions when available; and
- avoid assuming personal paths, internal systems, or organization-specific tools.

## License

This repository is available under the [MIT License](LICENSE).

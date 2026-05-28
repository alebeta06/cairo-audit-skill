# cairo-audit-skill

> AI-assisted security auditing for Cairo smart contracts on Starknet.
> An open-source Agent Skill for Claude Code.

<!-- 🇪🇸 NOTA: Este README es la cara pública del repo (lo ve la gente en GitHub), por eso va en
     inglés. Ojo a la diferencia: el SKILL.md lo consume Claude; este README es para HUMANOS. -->

> **Status:** 🚧 Early WIP — project scaffolding only. No audit content yet.

## What is this?

`cairo-audit-skill` is an [Agent Skill](https://docs.claude.com/en/docs/agents-and-tools/agent-skills)
that helps Claude Code assist with **security audits of Cairo smart contracts on Starknet**.

It **does not replace a human auditor** — it structures and accelerates the review: surfacing known
vulnerability patterns, guiding a methodical workflow, and helping write `snforge` security tests.

## Who is it for?

Cairo developers and Web3 security auditors.

## Installation

<!-- 🇪🇸 NOTA: Un skill se "instala" colocando su carpeta dentro de ~/.claude/skills/. El symlink
     es lo más cómodo en desarrollo: editas el repo y los cambios se reflejan al instante. -->

Make the skill discoverable by Claude Code by linking (or copying) this repo into your skills
directory:

```bash
# Option A — symlink (recommended while developing)
ln -s "$(pwd)" ~/.claude/skills/cairo-audit-skill

# Option B — copy
cp -r "$(pwd)" ~/.claude/skills/cairo-audit-skill
```

Then restart Claude Code. The skill activates automatically when you ask about auditing
Cairo/Starknet contracts.

## Usage

> 🚧 Coming soon. Once populated, ask Claude things like *"audit this Cairo contract"* and the skill
> will guide the review.

## Project structure

```
cairo-audit-skill/
├── SKILL.md            # Skill entry point (frontmatter + workflow)
├── patterns/           # Vulnerability patterns (one per file)
├── examples/           # Vulnerable vs. secure contract examples
├── tests-templates/    # snforge security test templates
├── docs/               # Extended documentation
├── CLAUDE.md           # Project context for Claude Code
├── README.md           # You are here
└── LICENSE             # MIT
```

## Contributing

Contributions welcome — this is documented audit knowledge, not compiled software. Project files
are in English; pedagogical comments may be added in Spanish using `<!-- 🇪🇸 NOTA: ... -->`.

## License

[MIT](LICENSE) © 2026 Alejandro Betancourt

# cairo-audit-skill

> AI-assisted security auditing for Cairo smart contracts on Starknet.
> An open-source Agent Skill for Claude Code.

<!-- 🇪🇸 NOTA: Este README es la cara pública del repo (lo ve la gente en GitHub), por eso va en
     inglés. Ojo a la diferencia: el SKILL.md lo consume Claude; este README es para HUMANOS. -->

> [![Status](https://img.shields.io/badge/status-active%20development%20paused-yellow)](#status-may-2026)
> **Active Development Paused** · Resuming July–August 2026

## Status (May 2026)

Active development is **temporarily paused** while the author completes a Master's
in Blockchain Systems & AI Engineering (CodeCrypto). This is a **strategic pause**,
not an abandonment — the repo stays open and the roadmap is intact.

**Completed so far**
- ✅ Day 1 Discovery: **31 vulnerability patterns** identified across the Cairo/Starknet threat landscape
- ✅ **PAT-001 → PAT-010** prioritized and queued for documentation
- ✅ Project scaffolding, `SKILL.md` skeleton, and MCP setup in place

**Timeline**
- ⏸️ Active development paused: **June 2026**
- ▶️ Resuming: **July–August 2026**, starting with **PAT-001**

**The repo stays open** — issues, discussions, and PRs are welcome and will be reviewed.

<!-- 🇪🇸 NOTA: Esta pausa es deliberada y estratégica, no un abandono. El autor está
     completando su Máster en Ingeniería de Sistemas Blockchain & IA (CodeCrypto) y
     prioriza terminarlo antes de seguir documentando patrones. La palabra "Abandoned"
     mata proyectos open source (la gente deja de contribuir y de usarlos); por eso
     usamos "Active Development Paused" con fecha de retorno concreta. Mantener el repo
     abierto a issues/PRs señala que el proyecto sigue vivo. -->

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

### MCP servers

This project ships a `.mcp.json` declaring the MCP servers it needs (`ruflo` for
multi-agent orchestration, `github` for issue/PR tooling). See
[`docs/MCP_SETUP.md`](docs/MCP_SETUP.md) for setup, required env vars and
troubleshooting.

<!-- 🇪🇸 NOTA: `.mcp.json` se versiona en git para que cualquier contribuidor
     levante el mismo entorno de servidores MCP al abrir el repo en Claude Code. -->

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

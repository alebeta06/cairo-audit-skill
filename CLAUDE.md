# CLAUDE.md — cairo-audit-skill

<!-- 🇪🇸 NOTA: Este archivo es la "memoria de largo plazo" del proyecto. Claude Code lo lee
     automáticamente al abrir el repo. Mantenlo conciso: es CONTEXTO, no documentación extensa. -->

## What this project is

`cairo-audit-skill` is an open-source **Agent Skill** (Anthropic `SKILL.md` format) that assists
security audits of Cairo smart contracts on Starknet.

**Philosophy:** it accelerates and structures the audit process — it does **not** replace a human
auditor. Findings are leads for a human to confirm, never a standalone "secure" verdict.

<!-- 🇪🇸 NOTA: Esto NO es una app ni una librería. Es un Agent Skill: la "lógica" vive en Markdown
     (SKILL.md + archivos de referencia) que GUÍA a Claude. No se compila ni se ejecuta como
     binario. Contribuir = escribir/mejorar prompts y conocimiento de auditoría, no features. -->

## What a "skill" repo is (important for contributors)

There is no binary to run. The "logic" lives in Markdown (`SKILL.md` plus reference files) that
*instructs* Claude. Contributing means improving that guidance and the documented audit knowledge,
not shipping compiled features.

## Tech stack (the ecosystem this skill reasons about)

| Area | Tool |
|---|---|
| Language | Cairo 2.x |
| Package manager / build | Scarb |
| Testing & fuzzing | Starknet Foundry (`snforge`) |
| Static analysis | Caracal |
| Contract library | OpenZeppelin Contracts for Cairo |
| Skill format | Anthropic Agent Skills (`SKILL.md`) |

## Conventions

- **Project files in English** (OSS standard).
- **Pedagogical notes in Spanish**, embedded as:
  - Markdown: `<!-- 🇪🇸 NOTA: ... -->`
  - Cairo / Rust / TS code: `// 🇪🇸 NOTA: ...`
- **Progressive disclosure**: keep `SKILL.md` short; push detail into `patterns/`, `examples/`,
  `docs/` and link to them.
- Keep files under 500 lines.
- `SKILL.md` lives at the repo root so relative links survive packaging into `.claude/skills/`.

## Folder structure

| Path | Purpose |
|---|---|
| `SKILL.md` | Skill entry point (frontmatter + workflow). |
| `patterns/` | Documented Cairo/Starknet vulnerability patterns (one per file). |
| `examples/` | Vulnerable vs. secure contract examples. |
| `tests-templates/` | `snforge` security test templates. |
| `docs/` | Extended documentation. |

## Build & test (placeholders — no Cairo code yet)

<!-- 🇪🇸 NOTA: Comandos de referencia para cuando haya código. Hoy no hacen nada porque las
     carpetas están vacías. Los dejamos documentados para no olvidarlos. -->

```bash
scarb build         # TODO: build example contracts
snforge test        # TODO: run snforge tests
caracal detect .    # TODO: run static analysis
```

## Key references

- Anthropic Agent Skills: https://docs.claude.com/en/docs/agents-and-tools/agent-skills
- The Cairo Book: https://book.cairo-lang.org
- The Starknet Book: https://book.starknet.io
- OpenZeppelin Contracts for Cairo: https://docs.openzeppelin.com/contracts-cairo
- Starknet Foundry (snforge): https://foundry-rs.github.io/starknet-foundry
- Caracal (static analyzer): https://github.com/crytic/caracal

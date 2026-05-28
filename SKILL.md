---
name: cairo-audit-skill
description: Assist with security audits of Cairo smart contracts on Starknet. Use when reviewing Cairo/Starknet contracts for vulnerabilities, running audits, threat modeling, or writing snforge security tests. Triggers on "audit", "Cairo", "Starknet", "vulnerability", "security review".
allowed-tools: Read, Grep, Glob, Bash
---

<!-- 🇪🇸 NOTA: El bloque de arriba entre "---" es el FRONTMATTER (metadatos en formato YAML).
     DEBE ser lo PRIMERO del archivo: ningún texto ni comentario puede ir antes del primer "---",
     o Claude Code no detectará el skill. Solo 'name' y 'description' son obligatorios. -->

<!-- 🇪🇸 NOTA: 'description' es lo ÚNICO que Claude lee SIEMPRE (Nivel 1 de "progressive
     disclosure"). Por eso lleva las palabras-gatillo (audit, Cairo, Starknet, vulnerability...)
     al frente: con ellas Claude decide si activar el skill. El cuerpo de abajo solo se carga
     cuando el skill se activa (Nivel 2). -->

<!-- 🇪🇸 NOTA: 'allowed-tools' limita qué herramientas puede usar el skill. Aquí solo lo necesario
     para auditar: Read (leer código), Grep/Glob (buscar patrones) y Bash (correr scarb/snforge/
     caracal). Más adelante podríamos añadir Agent/Task para escaneo en paralelo. -->

# Cairo Audit Skill

> Status: 🚧 Skeleton — the workflow and reference files below are placeholders to be filled in
> future sessions.

## What This Skill Does

Guides AI-assisted security audits of Cairo smart contracts on Starknet. It structures the review
process, surfaces known vulnerability patterns, and helps write `snforge` security tests. It
**does not replace a human auditor** — it accelerates and organizes their work.

## When to Use

- Reviewing a Cairo/Starknet contract before merge or deployment.
- Threat modeling a Starknet protocol (accounts, upgrades, cross-domain messaging).
- Writing or reviewing `snforge` security / fuzz tests.

## When NOT to Use

- Writing new feature code (this skill is read-and-review oriented).
- Deployment-only operations.
- Non-Cairo ecosystems (use a Solidity- or Rust-specific skill instead).

<!-- 🇪🇸 NOTA: "Reference Files" es el corazón del progressive disclosure: el SKILL.md se queda
     corto y APUNTA a archivos externos que Claude carga SOLO cuando los necesita (Nivel 3). Hoy
     están vacíos (placeholders); en próximas sesiones llenaremos patterns/, examples/ y docs/. -->

## Reference Files

| Context | Path |
|---|---|
| Vulnerability patterns (by category) | `patterns/` _(TODO)_ |
| Vulnerable vs. secure contract examples | `examples/` _(TODO)_ |
| snforge security test templates | `tests-templates/` _(TODO)_ |
| Extended documentation | `docs/` _(TODO)_ |

## Audit Workflow

<!-- 🇪🇸 NOTA: Estos pasos son un PLACEHOLDER. La metodología real (qué buscar en cada paso y qué
     comandos correr) se documentará en próximas sesiones. -->

1. **Initial read** — understand the architecture before hunting for bugs. _(TODO)_
2. **Threat model** — who attacks, what they want, their capabilities. _(TODO)_
3. **Static analysis** — run Caracal. _(TODO)_
4. **Manual line-by-line review** — where the real bugs live. _(TODO)_
5. **Property testing & fuzzing** — `snforge`. _(TODO)_
6. **Report** — severity + recommendations. _(TODO)_

## Principles

- Assume every external call is hostile.
- Assume any balance, price, or cross-domain message can be manipulated in the current block.
- Hunt for implicit invariants the developer assumed but never validated.
- Never declare code "secure" — declare "no issues found under this threat model".

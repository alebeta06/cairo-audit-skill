# MCP Setup

How to configure the Model Context Protocol (MCP) servers required by
`cairo-audit-skill` so contributors get a reproducible Claude Code environment.

<!-- 🇪🇸 NOTA: MCP (Model Context Protocol) es el protocolo abierto de Anthropic que
     permite a Claude Code hablar con servidores externos (APIs, BBDD, herramientas).
     Cada "servidor MCP" expone un conjunto de tools que Claude puede invocar. -->

## TL;DR

1. Install [Claude Code](https://docs.claude.com/en/docs/claude-code).
2. Export `GITHUB_PERSONAL_ACCESS_TOKEN` in your shell.
3. Open this project in Claude Code — `.mcp.json` is picked up automatically.
4. Verify with `claude mcp list`.

## Required servers

| Server | What it provides | Required? |
|---|---|---|
| `ruflo` | Multi-agent orchestration (swarm, memory, hooks, AgentDB). | Yes |
| `github` | Issue and PR management for this repo. | Yes (for contribution workflows) |

<!-- 🇪🇸 NOTA: Estos son los ÚNICOS servidores que necesita el skill para funcionar.
     Si tienes otros servidores configurados a nivel global (gdrive, Vercel, etc.),
     siguen funcionando — `.mcp.json` AÑADE servidores al proyecto, no los reemplaza. -->

## The `.mcp.json` file

`.mcp.json` lives at the repo root and is committed to git, so every contributor
runs the same MCP servers.

```json
{
  "mcpServers": {
    "ruflo": {
      "command": "npx",
      "args": ["-y", "ruflo@latest", "mcp", "start"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_PERSONAL_ACCESS_TOKEN}"
      }
    }
  }
}
```

### Field-by-field

<!-- 🇪🇸 NOTA pedagógica: aquí explico cada campo en español para que entiendas
     qué hace y por qué está como está. Si en el futuro añades otro servidor MCP,
     vas a copiar esta misma estructura. -->

**`mcpServers`** *(object, required)*
> Root object. Each key is the **alias** of an MCP server.
>
> <!-- 🇪🇸 El alias se convierte en el prefijo de las tools en Claude Code:
>      `ruflo` → `mcp__ruflo__swarm_init`, `mcp__ruflo__memory_store`, etc.
>      Cambiar el alias rompe cualquier referencia que dependa de ese nombre. -->

**`command`** *(string, required)*
> The executable that starts the server.
>
> <!-- 🇪🇸 Usamos `npx` para no obligar a instalar nada globalmente. `npx`
>      descarga el paquete (si no está en caché), lo ejecuta y se va.
>      Alternativas posibles: `node`, `python`, `docker`, una ruta absoluta. -->

**`args`** *(array of strings, required)*
> Arguments passed to `command`.
>
> <!-- 🇪🇸 Para `ruflo`:
>      - `-y` → flag de npx; acepta automáticamente la descarga si el paquete
>              no está instalado. Sin esto, npx pregunta interactivamente y el
>              servidor MCP nunca arranca.
>      - `ruflo@latest` → siempre la última versión publicada en npm.
>      - `mcp start` → subcomando del CLI de ruflo que arranca el servidor MCP
>                     en modo stdio (el transporte por defecto). -->

**`env`** *(object, optional)*
> Environment variables passed to the server process.
>
> <!-- 🇪🇸 Sintaxis `${VAR}` → Claude Code SUSTITUYE en tiempo de carga con la
>      variable de entorno de tu shell. NO se commitea ningún secreto.
>      Si la variable no existe, Claude Code lo reporta como warning al cargar. -->

**`type`** *(string, optional, default `"stdio"`)*
> Transport: `"stdio"` (default), `"sse"` or `"http"`.
>
> <!-- 🇪🇸 No aparece en nuestro JSON porque omitirlo = usar el default `stdio`,
>      que es lo correcto para servidores locales. `sse`/`http` son para
>      servidores remotos. -->

## Setting up `GITHUB_PERSONAL_ACCESS_TOKEN`

Generate a token at https://github.com/settings/tokens with these scopes:

- `repo` (full control of private repositories — needed for PR/issue tooling)
- `read:org` (read org membership — used by some workflows)

Export it in your shell:

```bash
# bash / zsh — add to ~/.bashrc or ~/.zshrc to persist
export GITHUB_PERSONAL_ACCESS_TOKEN="ghp_xxxxxxxxxxxxxxxxxxxx"
```

<!-- 🇪🇸 NOTA: NUNCA pongas el token literal en `.mcp.json`. Ese archivo se
     versiona en git → cualquier fuga = token comprometido = revocación inmediata
     y posible compromiso de tu cuenta. La interpolación `${VAR}` existe
     precisamente para evitar esto. -->

Restart your shell (or `source ~/.bashrc`) and verify:

```bash
echo $GITHUB_PERSONAL_ACCESS_TOKEN  # should print the token
```

> **Advanced alternative:** for setups with multiple projects each needing a
> different token, a per-project `.env` file is also a valid pattern. This guide
> does not cover that workflow — `.env` is already in `.gitignore` if you choose
> to use it.
>
> <!-- 🇪🇸 NOTA: solo mencionar que existe la alternativa. Para el flujo estándar,
>      una sola variable de entorno exportada en tu shell es suficiente y más simple. -->

## Verifying the setup

Inside the project directory:

```bash
claude mcp list
```

Expected output (your other globally-registered servers may also appear):

```
ruflo:  npx -y ruflo@latest mcp start - ✓ Connected
github: npx -y @modelcontextprotocol/server-github - ✓ Connected
```

Inside a Claude Code session, you can also run `/mcp` to see the connected servers.

## Relationship with `.claude/settings.local.json`

`.claude/settings.local.json` (already in `.gitignore`) controls **per-user**
settings — including which `.mcp.json` servers are enabled or disabled locally:

```json
{
  "enabledMcpjsonServers": ["ruflo", "github"],
  "disabledMcpjsonServers": []
}
```

<!-- 🇪🇸 NOTA importante:
     - `.mcp.json` = qué servidores PROPONE el proyecto (versionado, compartido).
     - `settings.local.json` = qué servidores AUTORIZAS tú localmente (no versionado).
     Claude Code te pregunta la primera vez si confías en el `.mcp.json` del repo;
     tu respuesta se guarda en `settings.local.json`. Por eso ambos archivos coexisten. -->

## Troubleshooting

**`claude mcp list` shows the server as `✗ Failed`:**
- Run the server command manually to see the error (e.g. `npx -y ruflo@latest mcp start`).
- Check Node.js ≥ 18 (`node --version`).

**GitHub tool calls return 401 / 403:**
- The token expired or lacks scopes. Regenerate at https://github.com/settings/tokens.
- Verify it's exported in the shell that launched Claude Code (not just any terminal).

**The server doesn't appear at all:**
- Make sure you opened Claude Code **inside this directory** (`.mcp.json` is
  resolved relative to the project root).
- Check that `enabledMcpjsonServers` in `.claude/settings.local.json` includes
  the server name, or accept the trust dialog when Claude Code prompts.

## Further reading

- [MCP specification](https://modelcontextprotocol.io)
- [Claude Code MCP configuration](https://docs.claude.com/en/docs/claude-code/mcp)
- [Ruflo / claude-flow](https://github.com/ruvnet/claude-flow)

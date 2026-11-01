# Opensquad — Project Instructions

This project uses **Opensquad**, a multi-agent orchestration framework.

## Quick Start

Type `/opensquad` to open the main menu, or use any of these commands:
- `/opensquad create` — Create a new squad
- `/opensquad run <name>` — Run a squad
- `/opensquad help` — See all commands

## Directory Structure

- `_opensquad/` — Opensquad core files (do not modify manually)
- `_opensquad/_memory/` — Persistent memory (company context, preferences)
- `squads/` — User-created squads
- `squads/{name}/_investigations/` — Sherlock content investigations (profile analyses)
- `squads/{name}/output/` — Generated content and files
- `_opensquad/_browser_profile/` — Persistent browser sessions (login cookies, localStorage)

## How It Works

1. The `/opensquad` skill is the entry point for all interactions
2. The **Architect** agent creates and modifies squads
3. During squad creation, the **Sherlock** investigator can analyze reference profiles (Instagram, YouTube, Twitter/X, LinkedIn) to extract real content patterns
4. The **Pipeline Runner** executes squads automatically
5. Agents communicate via persona switching (inline) or subagents (background)
6. Checkpoints pause execution for user input/approval

## Rules

- Always use `/opensquad` commands to interact with the system
- Do not manually edit files in `_opensquad/core/` unless you know what you're doing
- Squad YAML files can be edited manually if needed, but prefer using `/opensquad edit`
- Company context in `_opensquad/_memory/company.md` is loaded for every squad run

## Regras de conteúdo e layout dos posts (squad youtube-to-instagram)

Aprovadas pelo usuário. Os templates em `squads/youtube-to-instagram/_templates/` já trazem esses valores: use-os
como fonte da verdade.

- **Post único 1 (`single-post-template.html`), barra de CTA em dois níveis:** `{{CTA_TEXT}}` é uma **pergunta
  aberta** com gatilho mental (curiosidade ou prova social), em Montserrat 900, branco, 46px; `{{CTA_SUB}}` é uma
  instrução de ação curta (ex.: "Responda nos comentários!"), em Inter 500, lavanda `#DDD6FE`, 26px. A `.cta-bar`
  empilha os dois (`flex-direction: column; gap: 8px`). Nunca usar CTA de palavra única nem comando direto como
  texto principal (ex.: "Comenta CONTRATO" foi rejeitado).
- **Post único 2 (`single-post-2-template.html`), imagem de IA escurecida em dois níveis**, para o texto ficar
  legível: `filter: brightness(0.45)` na imagem e, em `.ai-image-wrap::before`, o gradiente
  `linear-gradient(180deg, rgba(13,13,16,0.72) 0%, rgba(13,13,16,0.45) 50%, transparent 100%)`. Se a imagem gerada
  já for muito escura, subir o brightness para 0,55 a 0,60; se for muito clara, manter 0,45 ou baixar para 0,35.
- **Post único 3 (`single-post-3-template.html`, fundo branco e lavanda):** sem tag de categoria no cabeçalho, só
  o logo colorido centralizado. Nunca incluir `{{TAG}}` nem a div `.tag`, e não passar o valor TAG ao substituir
  os placeholders.
- **Listas nos slides do carrossel:** itens `li` com `display: flex` e `gap`, nunca `position: absolute` com
  `padding-left`. Com fonte de 32px ou mais, o travessão do `::before` posicionado de forma absoluta sobrepõe a
  primeira letra do texto. CSS aprovado: `.content-card ul li { font-size: 32px; line-height: 1.5; display: flex;
  gap: 18px; align-items: flex-start; word-break: keep-all; overflow-wrap: break-word; }` e
  `.content-card ul li::before { content: "—"; color: #A855F7; font-weight: 700; flex-shrink: 0; line-height: 1.5; }`.

## Browser Sessions

Opensquad uses a persistent Playwright browser profile to keep you logged into social media platforms.
- Sessions are stored in `_opensquad/_browser_profile/` (gitignored, private to you)
- First time accessing a platform, you'll log in manually once
- Subsequent runs will reuse your saved session
- **Important:** The native Claude Code Playwright plugin must be disabled. Opensquad uses its own `@playwright/mcp` server configured in `.mcp.json`.

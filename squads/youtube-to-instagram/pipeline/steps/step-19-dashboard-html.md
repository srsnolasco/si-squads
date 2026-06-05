---
type: agent
agent: iago-instagram
execution: inline
inputFile: squads/youtube-to-instagram/output/{run-id}/Posts/post-content.md
outputFile: squads/youtube-to-instagram/output/{run-id}/Dashboard/dashboard-semanal-{slug}.html
---

# Step 19: Dashboard Semanal — HTML Unificado Auto-Suficiente

Iago gera um único arquivo HTML completamente auto-suficiente que agrupa todo o conteúdo do ciclo organizado por dia da semana. **Nenhuma referência a arquivos externos** — tudo embutido diretamente no HTML para que o arquivo possa ser copiado para qualquer destino e funcionar de forma independente.

## Context Loading

Antes de iniciar, Iago deve carregar e ler na íntegra:
- `squads/youtube-to-instagram/output/{run-id}/Posts/post-content.md` — legendas e conteúdo dos 5 posts
- `squads/youtube-to-instagram/output/{run-id}/Roteiros/roteiro-reel-viral-01-dom-{slug}.md` a `roteiro-reel-viral-06-sex-{slug}.md` — conteúdo completo dos 6 roteiros
- `squads/youtube-to-instagram/output/{run-id}/Stories/stories-01-dom-{slug}.md` a `stories-07-sab-{slug}.md` — conteúdo completo dos 7 stories
- `squads/youtube-to-instagram/output/{run-id}/lead-magnet-ideas.md` — isca digital aprovada
- `squads/youtube-to-instagram/output/{run-id}/Roteiros/roteiro-youtube-{slug}.md` — roteiro YouTube
- `squads/youtube-to-instagram/output/{run-id}/v1/doc-source-analysis.md` — relatório do vídeo
- `squads/youtube-to-instagram/output/{run-id}/v1/youtube-focus.md` — fonte e tipo de origem do conteúdo
- `squads/youtube-to-instagram/output/{run-id}/Prompts/media-prompts.md` — 3 prompts de imagem IA
- `_opensquad/_memory/company.md` — Perfil da Sucesso Imóvel

**PNGs dos posts — converter para base64:**
```bash
python3 -c "import base64; data = open('output/{run-id}/Posts/{slug}-single-post-1.png','rb').read(); print(base64.b64encode(data).decode())"
```
Repetir para cada PNG (single-post-1, single-post-2, single-post-3, todos os slides Seg-CT e Sex-CCTA).

**PDF da isca digital — converter para base64:**
```bash
python3 -c "import base64; data = open('output/{run-id}/Lead-Magnets/lead-magnet-{PALAVRA}-{slug}.pdf','rb').read(); print(base64.b64encode(data).decode())"
```

## Estrutura de Output

Um arquivo salvo na pasta Dashboard do run:
- `output/{run-id}/Dashboard/dashboard-semanal-{slug}.html`

## Instructions

Gerar um HTML 100% auto-suficiente com design Premium Dark da Sucesso Imóvel. **Toda imagem embutida como base64. Todo texto copiado diretamente dos arquivos MD. Nenhum `href` ou `src` apontando para arquivo externo.**

### Parte 0 — Card de Origem do Conteúdo

Preencher o bloco `source-card` logo abaixo do header:

1. **Tipo de origem** — ler `v1/youtube-focus.md` e identificar `source_type`:
   - `youtube` → classe `source-badge.youtube`, label "YouTube"
   - `local` → classe `source-badge.local`, label "Vídeo Local"
   - `document` → classe `source-badge.document`, label "Documento"
2. **Tema principal** — extrair o título/tema central da seção "1. Informações Básicas" do `doc-source-analysis.md`
3. **Resumo** — redigir em até 50 palavras uma síntese do conteúdo central, baseada nos Tópicos Principais do relatório; não copiar — sintetizar
4. **Metadados YouTube** — exibir o bloco `.source-meta` **somente** se `source_type = youtube`; extrair da seção "1. Informações Básicas" do `doc-source-analysis.md`:
   - Ano: extrair de "Data de publicação"
   - Visualizações: usar o campo "Visualizações" — se ausente, exibir "não disponível"
   - Se `source_type ≠ youtube`: remover o elemento `.source-meta` do HTML

### Layout Geral — Sidebar + 4 Views

O dashboard usa layout de **sidebar fixa à esquerda (220px)** com área de conteúdo à direita. A navegação principal é feita pela sidebar, que tem 4 botões:

| Botão | View | Conteúdo |
|---|---|---|
| Posts | `#view-posts` | Source card + nav por dia + todos os dias (Dom→Sáb) |
| Isca | `#view-isca` | Isca digital: título, palavra CTA, descrição, iframe do HTML da isca |
| Vídeo | `#view-video` | Relatório do vídeo (doc-source-analysis) + Roteiro YouTube em grid 2 colunas |
| Prompts | `#view-prompts` | 3 prompts Imagen com botões "Copiar prompt" e "Copiar legenda" |

JavaScript: `showView(name)` ativa a view correspondente e o botão da sidebar. Apenas uma view fica visível por vez (`.view { display:none }` / `.view.active { display:block }`).

O link "Suporte" da nav de dias é removido (conteúdo de suporte agora está nas views Vídeo e Prompts).

### Parte 1 — Calendário Semanal (por dia)

Uma seção por dia, na ordem Dom → Seg → Ter → Qua → Qui → Sex → Sáb. Cada seção contém o conteúdo completo publicado naquele dia.

| Dia | Conteúdo embutido |
|-----|------------------|
| Domingo | Reel 01-Dom completo (todos os 7 blocos + legenda) · Stories Dom completos |
| Segunda | Seg-CT (todos os slides PNG em base64 + legenda + hashtags) · Reel 02-Seg completo · Stories Seg completos |
| Terça | Ter-PU1 (PNG base64 + legenda + hashtags) · Reel 03-Ter completo · Stories Ter completos |
| Quarta | Qua-PU2 (PNG base64 + legenda + hashtags) · Reel 04-Qua completo · Stories Qua completos |
| Quinta | Qui-PU3 (PNG base64 + legenda + hashtags) · Reel 05-Qui completo · Stories Qui completos |
| Sexta | Sex-CCTA (slides PNG base64 + legenda + hashtags) · Reel 06-Sex completo · Stories Sex completos · Isca Digital (conteúdo + PDF embutido em base64) |
| Sábado | Stories Sáb completos |

### Parte 2 — Conteúdo de Suporte

Seções fixas independentes de dia:

- **Roteiro YouTube** — título, duração estimada, melhorias aplicadas + link para `roteiro-youtube-{slug}.html`
- **Prompts de Imagem IA** — os 3 prompts de `media-prompts.md` com ângulo e headline
- **Relatório do Vídeo** — resumo das 8 seções de `doc-source-analysis.md` + link para `doc-source-analysis.html`

---

## HTML Design

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <title>Dashboard Semanal — {TÍTULO} | Sucesso Imóvel</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@700;800;900&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: 'Inter', sans-serif;
      background: linear-gradient(160deg, #0A0012 0%, #1A0A2E 45%, #0D0D0D 100%);
      min-height: 100vh; color: #FFFFFF; padding: 48px 24px;
    }

    /* ── HEADER ── */
    .dashboard-header {
      max-width: 1200px; margin: 0 auto 56px;
      padding-bottom: 32px; border-bottom: 1px solid rgba(255,255,255,0.08);
    }
    .dashboard-header .label {
      font-size: 11px; font-weight: 700; color: #A855F7;
      text-transform: uppercase; letter-spacing: 2px; margin-bottom: 10px;
    }
    .dashboard-header h1 {
      font-family: 'Montserrat', sans-serif; font-size: 30px; font-weight: 900;
    }
    .dashboard-header .meta { font-size: 13px; color: rgba(255,255,255,0.4); margin-top: 8px; }

    /* ── SOURCE INFO ── */
    .source-card {
      max-width: 1200px; margin: -24px auto 40px;
      background: rgba(255,255,255,0.03);
      border: 1px solid rgba(168,85,247,0.2);
      border-radius: 16px; padding: 24px 32px;
      display: flex; align-items: flex-start; gap: 20px; flex-wrap: wrap;
    }
    .source-badge {
      font-size: 11px; font-weight: 700; text-transform: uppercase;
      letter-spacing: 1.5px; padding: 5px 14px; border-radius: 100px;
      white-space: nowrap; flex-shrink: 0; margin-top: 2px;
    }
    .source-badge.youtube  { background: rgba(255,80,80,0.12); color: #FF6B6B; border: 1px solid rgba(255,80,80,0.25); }
    .source-badge.local    { background: rgba(96,165,250,0.12); color: #60A5FA; border: 1px solid rgba(96,165,250,0.25); }
    .source-badge.document { background: rgba(52,211,153,0.12); color: #34D399; border: 1px solid rgba(52,211,153,0.25); }
    .source-content { flex: 1; min-width: 0; }
    .source-tema {
      font-family: 'Montserrat', sans-serif; font-size: 15px; font-weight: 700;
      color: #fff; margin-bottom: 8px;
    }
    .source-resumo { font-size: 13px; line-height: 1.6; color: rgba(255,255,255,0.65); }
    .source-meta { display: flex; gap: 20px; margin-top: 12px; flex-wrap: wrap; }
    .source-meta-item { font-size: 12px; color: rgba(255,255,255,0.4); }
    .source-meta-item strong { color: rgba(255,255,255,0.75); font-weight: 600; }

    /* ── NAV DIAS ── */
    .nav-dias {
      max-width: 1200px; margin: 0 auto 48px;
      display: flex; gap: 8px; flex-wrap: wrap;
    }
    .nav-dia {
      font-size: 12px; font-weight: 700; padding: 8px 18px;
      border-radius: 100px; cursor: pointer;
      background: rgba(255,255,255,0.06); color: rgba(255,255,255,0.6);
      border: 1px solid rgba(255,255,255,0.1);
      text-decoration: none; transition: all 0.2s;
    }
    .nav-dia:hover, .nav-dia.active {
      background: rgba(168,85,247,0.2); color: #A855F7;
      border-color: rgba(168,85,247,0.4);
    }

    /* ── DIA SECTION ── */
    .dia-section {
      max-width: 1200px; margin: 0 auto 64px;
      scroll-margin-top: 24px;
    }
    .dia-header {
      display: flex; align-items: center; gap: 16px; margin-bottom: 28px;
      padding-bottom: 16px; border-bottom: 2px solid rgba(168,85,247,0.25);
    }
    .dia-badge {
      font-family: 'Montserrat', sans-serif; font-size: 13px; font-weight: 800;
      background: #A855F7; color: #fff; padding: 6px 16px; border-radius: 100px;
    }
    .dia-title {
      font-family: 'Montserrat', sans-serif; font-size: 20px; font-weight: 800;
    }
    .dia-date { font-size: 13px; color: rgba(255,255,255,0.4); margin-left: auto; }

    /* ── CONTENT GRID ── */
    .content-grid {
      display: grid; grid-template-columns: repeat(auto-fit, minmax(340px, 1fr));
      gap: 20px;
    }

    /* ── CARD ── */
    .card {
      background: rgba(255,255,255,0.04); border: 1px solid rgba(255,255,255,0.08);
      border-radius: 16px; overflow: hidden;
    }
    .card-header {
      background: rgba(168,85,247,0.1); padding: 14px 20px;
      display: flex; align-items: center; gap: 10px;
      border-bottom: 1px solid rgba(168,85,247,0.15);
    }
    .card-type {
      font-size: 10px; font-weight: 700; text-transform: uppercase; letter-spacing: 1.5px;
      color: #A855F7; background: rgba(168,85,247,0.15);
      padding: 3px 10px; border-radius: 100px;
    }
    .card-title { font-family: 'Montserrat', sans-serif; font-size: 14px; font-weight: 700; }
    .card-body { padding: 20px; }

    /* Post PNG */
    .post-img { width: 100%; border-radius: 8px; margin-bottom: 16px; }

    /* Legenda */
    .legenda-label {
      font-size: 10px; font-weight: 700; color: rgba(255,255,255,0.35);
      text-transform: uppercase; letter-spacing: 1px; margin-bottom: 8px;
    }
    .legenda-text {
      font-size: 13px; line-height: 1.7; color: rgba(255,255,255,0.75);
      white-space: pre-wrap;
    }
    .hashtags { margin-top: 10px; font-size: 12px; color: #A855F7; }

    /* Reel summary */
    .reel-angulo {
      font-size: 12px; color: rgba(255,255,255,0.5); margin-bottom: 10px;
      font-style: italic;
    }
    .reel-cta {
      display: inline-block; background: rgba(168,85,247,0.15);
      color: #A855F7; font-size: 12px; font-weight: 700;
      padding: 4px 12px; border-radius: 100px; margin-top: 8px;
    }

    /* Story pills */
    .story-pills { display: flex; flex-direction: column; gap: 8px; }
    .story-pill {
      background: rgba(255,255,255,0.03); border-radius: 10px;
      padding: 10px 14px; display: flex; align-items: center; gap: 10px;
    }
    .story-time { font-size: 11px; font-weight: 700; color: #A855F7; min-width: 40px; }
    .story-tipo {
      font-size: 10px; font-weight: 700; text-transform: uppercase;
      padding: 2px 8px; border-radius: 100px; letter-spacing: 1px;
    }
    .story-tipo.teaser   { background: rgba(251,191,36,0.12); color: rgba(251,191,36,0.9); }
    .story-tipo.educacao { background: rgba(52,211,153,0.12); color: rgba(52,211,153,0.9); }
    .story-tipo.bastidor { background: rgba(96,165,250,0.12); color: rgba(96,165,250,0.9); }
    .story-tipo.prova    { background: rgba(244,114,182,0.12); color: rgba(244,114,182,0.9); }
    .story-tipo.cta      { background: rgba(168,85,247,0.18); color: #A855F7; }
    .story-texto { font-size: 12px; color: rgba(255,255,255,0.7); }

    /* Isca */
    .isca-word {
      display: inline-block; background: rgba(168,85,247,0.2);
      color: #A855F7; font-weight: 800; font-size: 14px;
      padding: 6px 16px; border-radius: 100px; margin: 12px 0;
    }
    .isca-link {
      display: inline-block; margin-top: 12px; font-size: 12px;
      color: #A855F7; text-decoration: none; font-weight: 600;
      border: 1px solid rgba(168,85,247,0.3); padding: 6px 14px; border-radius: 8px;
    }

    /* ── SUPORTE ── */
    .suporte-section {
      max-width: 1200px; margin: 0 auto 48px;
    }
    .suporte-header {
      font-family: 'Montserrat', sans-serif; font-size: 16px; font-weight: 800;
      color: rgba(255,255,255,0.4); text-transform: uppercase; letter-spacing: 2px;
      margin-bottom: 20px; padding-bottom: 12px;
      border-bottom: 1px solid rgba(255,255,255,0.06);
    }
    .link-card {
      display: inline-flex; align-items: center; gap: 10px;
      background: rgba(255,255,255,0.04); border: 1px solid rgba(255,255,255,0.08);
      border-radius: 12px; padding: 14px 20px; text-decoration: none;
      color: #FFFFFF; font-size: 14px; font-weight: 600;
      transition: border-color 0.2s;
    }
    .link-card:hover { border-color: rgba(168,85,247,0.4); }
    .link-card .icon { font-size: 18px; }
  </style>
</head>
<body>

  <!-- HEADER -->
  <div class="dashboard-header">
    <div class="label">Dashboard Semanal · Sucesso Imóvel</div>
    <h1>{TÍTULO DO TEMA}</h1>
    <div class="meta">Semana de publicação · Gerado em {YYYY-MM-DD}</div>
  </div>

  <!-- SOURCE INFO -->
  <div class="source-card">
    <span class="source-badge {youtube|local|document}">{YouTube | Vídeo Local | Documento}</span>
    <div class="source-content">
      <div class="source-tema">{TEMA PRINCIPAL — extraído da seção 1 do doc-source-analysis.md}</div>
      <div class="source-resumo">{RESUMO DO TEMA EM ATÉ 50 PALAVRAS — síntese do conteúdo central}</div>
      <!-- Exibir apenas se source_type = youtube: -->
      <div class="source-meta">
        <div class="source-meta-item">Publicado em <strong>{ANO}</strong></div>
        <div class="source-meta-item"><strong>{N visualizações}</strong> visualizações</div>
      </div>
    </div>
  </div>

  <!-- NAV DIAS -->
  <nav class="nav-dias">
    <a href="#dom" class="nav-dia">Dom</a>
    <a href="#seg" class="nav-dia">Seg</a>
    <a href="#ter" class="nav-dia">Ter</a>
    <a href="#qua" class="nav-dia">Qua</a>
    <a href="#qui" class="nav-dia">Qui</a>
    <a href="#sex" class="nav-dia">Sex</a>
    <a href="#sab" class="nav-dia">Sáb</a>
    <a href="#suporte" class="nav-dia">Suporte</a>
  </nav>

  <!-- DOM -->
  <section class="dia-section" id="dom">
    <div class="dia-header">
      <span class="dia-badge">01</span>
      <span class="dia-title">Domingo</span>
    </div>
    <div class="content-grid">
      <!-- Reel 01-Dom -->
      <div class="card">
        <div class="card-header">
          <span class="card-type">Reel Viral</span>
          <span class="card-title">01-Dom — Teaser Semanal</span>
        </div>
        <div class="card-body">
          <div class="reel-angulo">{ÂNGULO DO DOM-REEL}</div>
          <div class="legenda-label">Gancho</div>
          <div class="legenda-text">{BLOCO 1 FALA DO DOM-REEL}</div>
          <span class="reel-cta">CTA: {PALAVRA}</span>
        </div>
      </div>
      <!-- Stories Dom -->
      <div class="card">
        <div class="card-header">
          <span class="card-type">Stories</span>
          <span class="card-title">Domingo</span>
        </div>
        <div class="card-body">
          <div class="story-pills">
            {STORIES DO DIA — .story-pill com horário, tipo e texto}
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- SEG -->
  <section class="dia-section" id="seg">
    <div class="dia-header">
      <span class="dia-badge">02</span>
      <span class="dia-title">Segunda-feira</span>
    </div>
    <div class="content-grid">
      <!-- Seg-CT slides + legenda -->
      <div class="card">
        <div class="card-header">
          <span class="card-type">Seg-CT</span>
          <span class="card-title">{TÍTULO DO SEG-CT}</span>
        </div>
        <div class="card-body">
          {SLIDES PNG DO SEG-CT como <img class="post-img">}
          <div class="legenda-label">Legenda</div>
          <div class="legenda-text">{LEGENDA DO SEG-CT}</div>
          <div class="hashtags">{HASHTAGS}</div>
        </div>
      </div>
      <!-- Reel 02-Seg -->
      <div class="card">
        <div class="card-header">
          <span class="card-type">Reel Viral</span>
          <span class="card-title">02-Seg — Tema Principal</span>
        </div>
        <div class="card-body">
          <div class="reel-angulo">{ÂNGULO}</div>
          <div class="legenda-label">Gancho</div>
          <div class="legenda-text">{BLOCO 1 FALA}</div>
          <span class="reel-cta">CTA: {PALAVRA}</span>
        </div>
      </div>
      <!-- Stories Seg -->
      <div class="card">
        <div class="card-header">
          <span class="card-type">Stories</span>
          <span class="card-title">Segunda</span>
        </div>
        <div class="card-body">
          <div class="story-pills">
            {5 STORIES — 07:30 · 11:00 · 15:00 · 19:00 · 22:00}
          </div>
        </div>
      </div>
    </div>
  </section>

  {REPETIR MESMA ESTRUTURA PARA TER, QUA, QUI}

  <!-- SEX -->
  <section class="dia-section" id="sex">
    <div class="dia-header">
      <span class="dia-badge">06</span>
      <span class="dia-title">Sexta-feira</span>
    </div>
    <div class="content-grid">
      <!-- Sex-CCTA slides + legenda -->
      <div class="card">
        <div class="card-header">
          <span class="card-type">Sex-CCTA</span>
          <span class="card-title">{TÍTULO DO SEX-CCTA}</span>
        </div>
        <div class="card-body">
          {SLIDES PNG DO SEX-CCTA}
          <div class="legenda-label">Legenda</div>
          <div class="legenda-text">{LEGENDA DO SEX-CCTA}</div>
          <div class="hashtags">{HASHTAGS}</div>
        </div>
      </div>
      <!-- Reel 06-Sex -->
      <div class="card">
        <div class="card-header">
          <span class="card-type">Reel Viral</span>
          <span class="card-title">06-Sex — Isca Digital</span>
        </div>
        <div class="card-body">
          <div class="reel-angulo">{ÂNGULO}</div>
          <div class="legenda-label">Gancho</div>
          <div class="legenda-text">{BLOCO 1 FALA}</div>
          <span class="reel-cta">CTA: {PALAVRA}</span>
        </div>
      </div>
      <!-- Isca Digital -->
      <div class="card">
        <div class="card-header">
          <span class="card-type">Isca Digital</span>
          <span class="card-title">{TÍTULO DA ISCA}</span>
        </div>
        <div class="card-body">
          <div class="legenda-label">Formato</div>
          <div class="legenda-text">{FORMATO DA ISCA}</div>
          <div class="isca-word">{PALAVRA DO CTA}</div>
          <br>
          <a class="isca-link" href="Lead-Magnets/lead-magnet-{PALAVRA}-{slug}.pdf" target="_blank">Abrir PDF</a>
        </div>
      </div>
      <!-- Stories Sex -->
      <div class="card">
        <div class="card-header">
          <span class="card-type">Stories</span>
          <span class="card-title">Sexta</span>
        </div>
        <div class="card-body">
          <div class="story-pills">
            {5 STORIES}
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- SÁB -->
  <section class="dia-section" id="sab">
    <div class="dia-header">
      <span class="dia-badge">07</span>
      <span class="dia-title">Sábado</span>
    </div>
    <div class="content-grid">
      <div class="card">
        <div class="card-header">
          <span class="card-type">Stories</span>
          <span class="card-title">Sábado</span>
        </div>
        <div class="card-body">
          <div class="story-pills">
            {3 STORIES — 11:00 · 15:00 · 19:00}
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- SUPORTE -->
  <section class="suporte-section" id="suporte">
    <div class="suporte-header">Conteúdo de Suporte</div>
    <div class="content-grid">

      <!-- Roteiro YouTube -->
      <div class="card">
        <div class="card-header">
          <span class="card-type">Roteiro YouTube</span>
          <span class="card-title">{TÍTULO DO VÍDEO}</span>
        </div>
        <div class="card-body">
          <div class="legenda-label">Duração estimada</div>
          <div class="legenda-text">{DURAÇÃO ESTIMADA}</div>
          <div class="legenda-label" style="margin-top:16px">Melhorias Aplicadas</div>
          <div class="legenda-text">{LISTA DE MELHORIAS}</div>
          <div class="legenda-label" style="margin-top:16px">Estrutura</div>
          <div class="legenda-text">{BLOCOS DO ROTEIRO — resumo de cada bloco com timecode}</div>
        </div>
      </div>

      <!-- Relatório do Vídeo -->
      <div class="card">
        <div class="card-header">
          <span class="card-type">Relatório do Vídeo</span>
          <span class="card-title">{TÍTULO DO VÍDEO}</span>
        </div>
        <div class="card-body">
          <div class="legenda-label">Pontos Positivos</div>
          <div class="legenda-text">{SEÇÃO 2 DO RELATÓRIO}</div>
          <div class="legenda-label" style="margin-top:16px">Pontos Negativos</div>
          <div class="legenda-text">{SEÇÃO 3 DO RELATÓRIO}</div>
          <div class="legenda-label" style="margin-top:16px">Hook — Avaliação</div>
          <div class="legenda-text">{SEÇÃO 4 DO RELATÓRIO}</div>
          <div class="legenda-label" style="margin-top:16px">Insights-Chave</div>
          <div class="legenda-text">{SEÇÃO 5 DO RELATÓRIO}</div>
        </div>
      </div>

      <!-- Prompts de Imagem IA -->
      <div class="card">
        <div class="card-header">
          <span class="card-type">Prompts Imagem IA</span>
          <span class="card-title">3 ângulos — Alerta · Dado · Reflexão</span>
        </div>
        <div class="card-body">
          {PARA CADA PROMPT:
          <div class="legenda-label">{ÂNGULO}</div>
          <div class="legenda-text">{HEADLINE} — {SUB-HEADLINE}</div>
          <div class="legenda-text" style="margin-top:8px; font-family:monospace; font-size:11px; color:rgba(168,85,247,0.8)">{PROMPT EM INGLÊS}</div>
          }
        </div>
      </div>

    </div>
  </section>

</body>
</html>
```

Salvar em `output/{run-id}/dashboard-semanal-{slug}.html`.

## Quality Criteria

- [ ] Card de origem presente com: tipo de origem, tema principal e resumo (≤ 50 palavras)
- [ ] Classe CSS do badge corresponde ao tipo de origem (`youtube`, `local` ou `document`)
- [ ] Bloco `.source-meta` (ano + visualizações) exibido apenas quando `source_type = youtube`
- [ ] Todos os 7 dias presentes na ordem correta (Dom a Sáb)
- [ ] Cada dia com o conteúdo correto conforme tabela de estrutura
- [ ] Todos os PNGs embutidos como base64 — nenhum `src` com caminho de arquivo
- [ ] PDF da isca digital embutido como base64 na seção da Sexta
- [ ] Todos os roteiros de reels com conteúdo completo dos 7 blocos embutido
- [ ] Todos os stories com horário, tipo e texto embutidos
- [ ] Legenda e hashtags de cada post exibidas completas
- [ ] Seção de Suporte com conteúdo do roteiro YouTube, relatório do vídeo e prompts de imagem IA embutidos
- [ ] Nenhum `href` ou `src` apontando para arquivo externo
- [ ] Navegação por âncoras funcional
- [ ] Google Fonts é a única dependência externa permitida
- [ ] Arquivo salvo em `output/{run-id}/dashboard-semanal-{slug}.html`

## Veto Conditions

1. Algum dia ausente ou fora de ordem
2. Qualquer imagem referenciada por caminho de arquivo (deve ser base64)
3. PDF da isca não embutido (deve ser base64)
4. Qualquer `href` apontando para arquivo externo
5. Post sem legenda completa exibida
6. Conteúdo de reel ou story ausente ou incompleto
7. Arquivo salvo fora da raiz de `output/{run-id}/`

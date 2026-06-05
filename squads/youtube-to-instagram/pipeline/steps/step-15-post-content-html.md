---
type: agent
agent: iago-instagram
execution: inline
inputFile: squads/youtube-to-instagram/output/Posts/post-content.md
outputFile: squads/youtube-to-instagram/output/Posts/post-content.html
---

# Step 15: Iago Instagram — Gerar HTML do Conteúdo dos Posts

Iago gera um arquivo HTML completo e visualmente rico a partir do `post-content.md`, usando a identidade visual da Sucesso Imóvel (Premium Dark). Este arquivo serve como **brief visual** — permite revisar todo o conteúdo dos posts de forma organizada e bonita, sem precisar abrir o Markdown bruto.

## Context Loading

- `squads/youtube-to-instagram/output/Posts/post-content.md` — conteúdo dos 5 posts (já escrito)
- `squads/youtube-to-instagram/pipeline/data/visual-identity.md` — paleta de cores e tipografia SI

## Objetivo

Gerar `output/Posts/post-content.html` — um documento HTML auto-suficiente que apresenta os 5 posts (3 posts únicos + 1 Seg-CT + 1 Sex-CCTA) com:
- Design Premium Dark da Sucesso Imóvel
- Cards individuais por post com todas as seções
- Legenda e hashtags formatadas
- Indicadores visuais de tipo de post, tom de voz e CTA
- Totalmente auto-suficiente (CSS inline + Google Fonts apenas)

## HTML Structure

O HTML deve seguir exatamente esta estrutura e design:

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Post Content — {TÍTULO DA SÉRIE} | Sucesso Imóvel</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700;800;900&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet" />
  <style>
    /* Reset & Base */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: 'Inter', sans-serif;
      background: linear-gradient(160deg, #0A0012 0%, #1A0A2E 45%, #0D0D0D 100%);
      min-height: 100vh;
      color: #FFFFFF;
      padding: 48px 24px;
    }

    /* ── PAGE HEADER ── */
    .page-header {
      max-width: 960px;
      margin: 0 auto 56px;
      display: flex;
      align-items: center;
      gap: 20px;
      padding-bottom: 32px;
      border-bottom: 1px solid rgba(255,255,255,0.08);
    }
    .si-badge {
      width: 52px; height: 52px;
      border-radius: 14px;
      background: linear-gradient(135deg, #7B2FBE, #A855F7);
      display: flex; align-items: center; justify-content: center;
      font-family: 'Montserrat', sans-serif;
      font-weight: 900; font-size: 20px;
      color: #fff; flex-shrink: 0;
    }
    .page-header-text h1 {
      font-family: 'Montserrat', sans-serif;
      font-weight: 900; font-size: 22px;
      color: #fff;
    }
    .page-header-text p {
      font-size: 13px; color: #9B9B9B; margin-top: 4px;
    }
    .page-header-text p span {
      color: #A855F7; font-weight: 600;
    }

    /* ── LAYOUT ── */
    .posts-grid {
      max-width: 960px;
      margin: 0 auto;
      display: flex;
      flex-direction: column;
      gap: 40px;
    }

    /* ── POST CARD ── */
    .post-card {
      background: rgba(255,255,255,0.04);
      border: 1px solid rgba(123,47,190,0.35);
      border-radius: 20px;
      overflow: hidden;
      position: relative;
    }
    .post-card::before {
      content: '';
      display: block;
      height: 3px;
      background: linear-gradient(90deg, transparent, #7B2FBE, #A855F7, transparent);
    }

    /* ── CARD HEADER ── */
    .card-header {
      padding: 24px 32px 20px;
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 16px;
      border-bottom: 1px solid rgba(255,255,255,0.06);
    }
    .card-header-left { display: flex; align-items: center; gap: 14px; }
    .post-type-icon {
      width: 44px; height: 44px; border-radius: 12px;
      background: rgba(123,47,190,0.25);
      border: 1px solid rgba(168,85,247,0.4);
      display: flex; align-items: center; justify-content: center;
      font-size: 20px; flex-shrink: 0;
    }
    .post-type-label {
      font-family: 'Inter', sans-serif;
      font-size: 11px; font-weight: 700;
      letter-spacing: 2px; text-transform: uppercase;
      color: #A855F7; margin-bottom: 4px;
    }
    .post-title {
      font-family: 'Montserrat', sans-serif;
      font-weight: 800; font-size: 18px; color: #fff;
    }
    .card-badges { display: flex; gap: 8px; flex-wrap: wrap; align-items: flex-start; }
    .badge {
      padding: 4px 12px; border-radius: 20px;
      font-size: 11px; font-weight: 700;
      letter-spacing: 1.5px; text-transform: uppercase;
      white-space: nowrap;
    }
    .badge-tag { background: rgba(168,85,247,0.15); color: #A855F7; border: 1px solid rgba(168,85,247,0.3); }
    .badge-tom { background: rgba(255,255,255,0.06); color: #9B9B9B; border: 1px solid rgba(255,255,255,0.1); }
    .badge-template { background: rgba(123,47,190,0.12); color: #D4A0FF; border: 1px solid rgba(212,160,255,0.2); }

    /* ── CARD BODY ── */
    .card-body { padding: 28px 32px; display: flex; flex-direction: column; gap: 24px; }

    /* ── FIELDS GRID ── */
    .fields-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 16px;
    }
    .field { display: flex; flex-direction: column; gap: 6px; }
    .field-full { grid-column: 1 / -1; }
    .field-label {
      font-size: 10px; font-weight: 700;
      letter-spacing: 2px; text-transform: uppercase;
      color: #6B6B6B;
    }
    .field-value {
      font-size: 14px; font-weight: 500; color: #FFFFFF;
      line-height: 1.6;
    }
    .field-value .accent { color: #A855F7; }
    .field-value .accent-gold { color: #D4A0FF; }
    .field-headline {
      font-family: 'Montserrat', sans-serif;
      font-size: 18px; font-weight: 800;
      color: #fff; line-height: 1.4;
    }
    .field-headline .accent { color: #A855F7; }

    /* ── CTA PILL ── */
    .cta-pill {
      display: inline-flex; align-items: center; gap: 8px;
      padding: 8px 18px; border-radius: 24px;
      background: linear-gradient(135deg, rgba(123,47,190,0.3), rgba(168,85,247,0.2));
      border: 1px solid rgba(168,85,247,0.5);
      font-size: 14px; font-weight: 700; color: #A855F7;
      width: fit-content;
    }
    .cta-pill::before { content: '→'; font-size: 12px; }

    /* ── DIVIDER ── */
    .section-divider {
      height: 1px;
      background: rgba(255,255,255,0.06);
      margin: 0 -32px;
    }

    /* ── CAPTION BLOCK ── */
    .caption-block {
      background: rgba(255,255,255,0.03);
      border-radius: 12px;
      padding: 20px 24px;
      border-left: 3px solid #7B2FBE;
    }
    .caption-block .section-label {
      font-size: 10px; font-weight: 700;
      letter-spacing: 2px; text-transform: uppercase;
      color: #A855F7; margin-bottom: 12px;
    }
    .caption-text {
      font-size: 14px; color: #FFFFFF;
      line-height: 1.8; white-space: pre-wrap;
    }

    /* ── HASHTAGS ── */
    .hashtags-block { display: flex; flex-wrap: wrap; gap: 8px; }
    .hashtag {
      padding: 4px 12px; border-radius: 20px;
      background: rgba(123,47,190,0.12);
      border: 1px solid rgba(123,47,190,0.25);
      font-size: 12px; color: #9B9B9B; font-weight: 500;
    }

    /* ── SLIDES SECTION (CARROSSEL) ── */
    .slides-container { display: flex; flex-direction: column; gap: 16px; }
    .slide-item {
      background: rgba(123,47,190,0.08);
      border: 1px solid rgba(168,85,247,0.2);
      border-radius: 12px;
      padding: 20px 24px;
    }
    .slide-number {
      font-size: 10px; font-weight: 700;
      letter-spacing: 2px; text-transform: uppercase;
      color: #7B2FBE; margin-bottom: 10px;
    }
    .slide-headline {
      font-family: 'Montserrat', sans-serif;
      font-weight: 800; font-size: 16px;
      color: #fff; margin-bottom: 10px; line-height: 1.4;
    }
    .slide-headline .accent { color: #A855F7; }
    .slide-body {
      font-size: 13px; color: #9B9B9B;
      line-height: 1.7; white-space: pre-wrap;
    }

    /* ── SECTION LABEL ── */
    .section-label-lg {
      font-size: 11px; font-weight: 700;
      letter-spacing: 2px; text-transform: uppercase;
      color: #6B6B6B; margin-bottom: 14px;
    }

    /* ── PAGE FOOTER ── */
    .page-footer {
      max-width: 960px; margin: 64px auto 0;
      padding-top: 24px;
      border-top: 1px solid rgba(255,255,255,0.06);
      display: flex; align-items: center; justify-content: space-between;
    }
    .page-footer-brand { display: flex; align-items: center; gap: 10px; }
    .page-footer-brand .dot {
      width: 8px; height: 8px; border-radius: 50%;
      background: linear-gradient(135deg, #7B2FBE, #A855F7);
    }
    .page-footer-brand span { font-size: 13px; color: #6B6B6B; }
    .page-footer-brand span strong { color: #A855F7; }
    .page-footer-date { font-size: 12px; color: #6B6B6B; }
  </style>
</head>
<body>

  <!-- PAGE HEADER -->
  <header class="page-header">
    <div class="si-badge">SI</div>
    <div class="page-header-text">
      <h1>{TÍTULO DA SÉRIE}</h1>
      <p>Sucesso Imóvel · <span>{DATA}</span> · 4 posts gerados</p>
    </div>
  </header>

  <main class="posts-grid">

    <!-- ═══════════════════════════════════════════════════════════
         POST ÚNICO 1
    ═══════════════════════════════════════════════════════════ -->
    <article class="post-card">
      <div class="card-header">
        <div class="card-header-left">
          <div class="post-type-icon">📸</div>
          <div>
            <div class="post-type-label">Ter-PU1 · Dr. Jeorge</div>
            <div class="post-title">{TÍTULO DO POST ÚNICO 1}</div>
          </div>
        </div>
        <div class="card-badges">
          <span class="badge badge-tag">{TAG Ter-PU1}</span>
          <span class="badge badge-tom">{TOM Ter-PU1}</span>
          <span class="badge badge-template">Roxo/Preto</span>
        </div>
      </div>

      <div class="card-body">
        <!-- Fields grid -->
        <div class="fields-grid">
          <div class="field">
            <span class="field-label">Eyebrow</span>
            <span class="field-value">{EYEBROW Ter-PU1}</span>
          </div>
          <div class="field">
            <span class="field-label">Foto Dr. Jeorge</span>
            <span class="field-value">{FOTO Ter-PU1}</span>
          </div>
          <div class="field field-full">
            <span class="field-label">Headline</span>
            <div class="field-headline">{HEADLINE Ter-PU1 — renderizar HTML com accent}</div>
          </div>
          <div class="field field-full">
            <span class="field-label">Body Text</span>
            <div class="field-value">{BODY Ter-PU1 — renderizar HTML com accent}</div>
          </div>
          <div class="field">
            <span class="field-label">Badge Text</span>
            <span class="field-value">{BADGE Ter-PU1}</span>
          </div>
          <div class="field">
            <span class="field-label">CTA</span>
            <div class="cta-pill">{CTA Ter-PU1}</div>
          </div>
        </div>

        <div class="section-divider"></div>

        <!-- Caption -->
        <div>
          <div class="section-label-lg">Legenda</div>
          <div class="caption-block">
            <div class="caption-label section-label">Texto completo</div>
            <div class="caption-text">{LEGENDA Ter-PU1 — texto completo com quebras de linha}</div>
          </div>
        </div>

        <!-- Hashtags -->
        <div>
          <div class="section-label-lg">Hashtags</div>
          <div class="hashtags-block">
            {CADA HASHTAG COMO: <span class="hashtag">#tag</span>}
          </div>
        </div>
      </div>
    </article>


    <!-- ═══════════════════════════════════════════════════════════
         POST ÚNICO 2
    ═══════════════════════════════════════════════════════════ -->
    <article class="post-card">
      <div class="card-header">
        <div class="card-header-left">
          <div class="post-type-icon">🤖</div>
          <div>
            <div class="post-type-label">Qua-PU2 · Imagem IA</div>
            <div class="post-title">{TÍTULO DO POST ÚNICO 2}</div>
          </div>
        </div>
        <div class="card-badges">
          <span class="badge badge-tag">{TAG Qua-PU2}</span>
          <span class="badge badge-tom">{TOM Qua-PU2}</span>
          <span class="badge badge-template">Carvão/Roxo</span>
        </div>
      </div>

      <div class="card-body">
        <div class="fields-grid">
          <div class="field">
            <span class="field-label">Eyebrow</span>
            <span class="field-value">{EYEBROW Qua-PU2}</span>
          </div>
          <div class="field">
            <span class="field-label">Badge Text</span>
            <span class="field-value">{BADGE Qua-PU2}</span>
          </div>
          <div class="field field-full">
            <span class="field-label">Headline</span>
            <div class="field-headline">{HEADLINE Qua-PU2}</div>
          </div>
          <div class="field field-full">
            <span class="field-label">Body Text</span>
            <div class="field-value">{BODY Qua-PU2}</div>
          </div>
          <div class="field field-full">
            <span class="field-label">Prompt Imagem IA</span>
            <div class="field-value" style="font-family: monospace; font-size: 12px; color: #D4A0FF; background: rgba(212,160,255,0.06); padding: 12px; border-radius: 8px; line-height: 1.6;">{PROMPT IA Qua-PU2}</div>
          </div>
          <div class="field">
            <span class="field-label">CTA</span>
            <div class="cta-pill">{CTA Qua-PU2}</div>
          </div>
        </div>

        <div class="section-divider"></div>

        <div>
          <div class="section-label-lg">Legenda</div>
          <div class="caption-block">
            <div class="caption-label section-label">Texto completo</div>
            <div class="caption-text">{LEGENDA Qua-PU2}</div>
          </div>
        </div>

        <div>
          <div class="section-label-lg">Hashtags</div>
          <div class="hashtags-block">
            {HASHTAGS Qua-PU2}
          </div>
        </div>
      </div>
    </article>


    <!-- ═══════════════════════════════════════════════════════════
         POST ÚNICO 3
    ═══════════════════════════════════════════════════════════ -->
    <article class="post-card">
      <div class="card-header">
        <div class="card-header-left">
          <div class="post-type-icon">💬</div>
          <div>
            <div class="post-type-label">Qui-PU3 · Só Texto</div>
            <div class="post-title">{TÍTULO DO POST ÚNICO 3}</div>
          </div>
        </div>
        <div class="card-badges">
          <span class="badge badge-tag">{TAG Qui-PU3}</span>
          <span class="badge badge-tom">{TOM Qui-PU3}</span>
          <span class="badge badge-template">Branco/Lavanda</span>
        </div>
      </div>

      <div class="card-body">
        <div class="fields-grid">
          <div class="field">
            <span class="field-label">Eyebrow</span>
            <span class="field-value">{EYEBROW Qui-PU3}</span>
          </div>
          <div class="field">
            <span class="field-label">Badge Text</span>
            <span class="field-value">{BADGE Qui-PU3}</span>
          </div>
          <div class="field field-full">
            <span class="field-label">Headline</span>
            <div class="field-headline">{HEADLINE Qui-PU3}</div>
          </div>
          <div class="field field-full">
            <span class="field-label">Quote Text</span>
            <div class="field-value" style="font-style: italic; font-size: 16px; color: #D4A0FF; border-left: 3px solid #A855F7; padding-left: 16px; line-height: 1.6;">{QUOTE Qui-PU3}</div>
          </div>
          <div class="field field-full">
            <span class="field-label">Body Text</span>
            <div class="field-value">{BODY Qui-PU3}</div>
          </div>
          <div class="field">
            <span class="field-label">CTA</span>
            <div class="cta-pill">{CTA Qui-PU3}</div>
          </div>
        </div>

        <div class="section-divider"></div>

        <div>
          <div class="section-label-lg">Legenda</div>
          <div class="caption-block">
            <div class="caption-label section-label">Texto completo</div>
            <div class="caption-text">{LEGENDA Qui-PU3}</div>
          </div>
        </div>

        <div>
          <div class="section-label-lg">Hashtags</div>
          <div class="hashtags-block">
            {HASHTAGS Qui-PU3}
          </div>
        </div>
      </div>
    </article>


    <!-- ═══════════════════════════════════════════════════════════
         CARROSSEL
    ═══════════════════════════════════════════════════════════ -->
    <article class="post-card">
      <div class="card-header">
        <div class="card-header-left">
          <div class="post-type-icon">🎠</div>
          <div>
            <div class="post-type-label">Seg-CT · {N} Slides</div>
            <div class="post-title">{TÍTULO DO CARROSSEL}</div>
          </div>
        </div>
        <div class="card-badges">
          <span class="badge badge-tag">{TAG CARROSSEL}</span>
          <span class="badge badge-tom">Educativo Direto</span>
          <span class="badge badge-template">Premium Dark</span>
        </div>
      </div>

      <div class="card-body">

        <!-- Slides -->
        <div>
          <div class="section-label-lg">Slides</div>
          <div class="slides-container">

            <!-- Slide 1 — CAPA -->
            <div class="slide-item">
              <div class="slide-number">Slide 1 — Capa</div>
              <div class="slide-headline">{HEADLINE CAPA}</div>
              <div class="slide-body">Eyebrow: {EYEBROW CAPA}
Subtítulo: {SUBTITULO CAPA}
Botão: ← ARRASTE</div>
            </div>

            {SLIDES 2 a N-1 — repetir o bloco abaixo para cada slide de conteúdo:
            <div class="slide-item">
              <div class="slide-number">Slide N — {NOME DO SLIDE}</div>
              <div class="slide-headline">{HEADLINE DO SLIDE}</div>
              <div class="slide-body">{BODY TEXT DO SLIDE}</div>
            </div>
            }

            <!-- Último Slide — CTA -->
            <div class="slide-item" style="border-color: rgba(168,85,247,0.4); background: rgba(123,47,190,0.12);">
              <div class="slide-number">Slide {N} — CTA</div>
              <div class="slide-headline">{HEADLINE CTA}</div>
              <div class="slide-body">{BLOCO CTA — texto completo}</div>
            </div>

          </div>
        </div>

        <div class="section-divider"></div>

        <div>
          <div class="section-label-lg">Legenda</div>
          <div class="caption-block">
            <div class="caption-label section-label">Texto completo</div>
            <div class="caption-text">{LEGENDA CARROSSEL}</div>
          </div>
        </div>

        <div>
          <div class="section-label-lg">Hashtags</div>
          <div class="hashtags-block">
            {HASHTAGS CARROSSEL}
          </div>
        </div>
      </div>
    </article>

    <!-- ═══════════════════════════════════════════════════════════
         SEX-CCTA — CARROSSEL ISCA DIGITAL
    ═══════════════════════════════════════════════════════════ -->
    <article class="post-card">
      <div class="card-header">
        <div class="card-header-left">
          <div class="post-type-icon">🧲</div>
          <div>
            <div class="post-type-label">Sex-CCTA · {N} Slides</div>
            <div class="post-title">{TÍTULO DO CARROSSEL ISCA}</div>
          </div>
        </div>
        <div class="card-badges">
          <span class="badge badge-tag">{TAG Sex-CCTA}</span>
          <span class="badge badge-tom">Isca Digital</span>
          <span class="badge badge-template">Premium Dark</span>
        </div>
      </div>

      <div class="card-body">

        <!-- Palavra do CTA -->
        <div class="fields-grid">
          <div class="field field-full">
            <span class="field-label">Palavra do CTA</span>
            <div class="cta-pill">{PALAVRA DO CTA — extraída de lead-magnet-ideas.md}</div>
          </div>
        </div>

        <div class="section-divider"></div>

        <!-- Slides -->
        <div>
          <div class="section-label-lg">Slides</div>
          <div class="slides-container">

            <!-- Slide 1 — CAPA -->
            <div class="slide-item">
              <div class="slide-number">Slide 1 — Capa</div>
              <div class="slide-headline">{HEADLINE CAPA CCTA}</div>
              <div class="slide-body">Eyebrow: {EYEBROW CAPA CCTA}
Subtítulo: {SUBTITULO CAPA CCTA}
Botão: ← ARRASTE</div>
            </div>

            {SLIDES 2 a N-1 — repetir o bloco abaixo para cada slide de conteúdo:
            <div class="slide-item">
              <div class="slide-number">Slide N — {NOME DO SLIDE}</div>
              <div class="slide-headline">{HEADLINE DO SLIDE}</div>
              <div class="slide-body">{BODY TEXT DO SLIDE}</div>
            </div>
            }

            <!-- Último Slide — CTA -->
            <div class="slide-item" style="border-color: rgba(168,85,247,0.4); background: rgba(123,47,190,0.12);">
              <div class="slide-number">Slide {N} — CTA</div>
              <div class="slide-headline">{HEADLINE CTA CCTA}</div>
              <div class="slide-body">{BLOCO CTA — "Comenta [PALAVRA] aqui embaixo e receba..."}</div>
            </div>

          </div>
        </div>

        <div class="section-divider"></div>

        <div>
          <div class="section-label-lg">Legenda</div>
          <div class="caption-block">
            <div class="caption-label section-label">Texto completo</div>
            <div class="caption-text">{LEGENDA Sex-CCTA}</div>
          </div>
        </div>

        <div>
          <div class="section-label-lg">Hashtags</div>
          <div class="hashtags-block">
            {HASHTAGS Sex-CCTA}
          </div>
        </div>
      </div>
    </article>

  </main>

  <!-- PAGE FOOTER -->
  <footer class="page-footer">
    <div class="page-footer-brand">
      <div class="dot"></div>
      <span>Gerado por <strong>@sucessoimovel</strong> · Squad YouTube → Instagram</span>
    </div>
    <div class="page-footer-date">{DATA}</div>
  </footer>

</body>
</html>
```

## Instructions

1. Ler `output/Posts/post-content.md` na íntegra
2. Usar o template HTML acima como base
3. Substituir TODOS os `{PLACEHOLDERS}` com o conteúdo real do markdown
4. Para **headline e body text**: renderizar o HTML original (manter as tags `<span class="accent">`, `<br>`, etc.) — elas funcionam diretamente no HTML
5. Para **hashtags**: separar cada uma e criar um `<span class="hashtag">` individual
6. Para **legenda**: preservar as quebras de linha usando `white-space: pre-wrap` já aplicado no CSS
7. Para **slides do Seg-CT**: criar um `<div class="slide-item">` para cada slide
8. Para **slides do Sex-CCTA**: criar um `<div class="slide-item">` para cada slide; incluir a **Palavra do CTA** extraída de `lead-magnet-ideas.md` no campo correspondente
9. Para o **prompt da imagem IA**: incluir no campo correspondente do Qua-PU2 (ler de `output/{run-id}/Prompts/ai-image-prompt-post2.md`)
10. **Não alterar nenhum CSS** — apenas preencher o conteúdo
11. Salvar em `output/Posts/post-content.html`

## Output

Salvar o arquivo HTML completo em `output/Posts/post-content.html`.

## Quality Criteria

- [ ] Todos os 5 posts aparecem no HTML (Ter-PU1, Qua-PU2, Qui-PU3, Seg-CT e Sex-CCTA)
- [ ] Todos os campos do markdown estão presentes no HTML
- [ ] Tags HTML do conteúdo (`<span class="accent">`, `<br>`) estão renderizadas corretamente
- [ ] Cada hashtag é um elemento `<span class="hashtag">` separado
- [ ] Quebras de linha da legenda estão preservadas
- [ ] Prompt da imagem IA está incluído no card do Qua-PU2
- [ ] Palavra do CTA do Sex-CCTA está presente no card correspondente
- [ ] Arquivo salvo em `output/Posts/post-content.html`

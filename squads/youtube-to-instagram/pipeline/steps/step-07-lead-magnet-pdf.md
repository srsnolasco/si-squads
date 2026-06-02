---
type: agent
agent: diego-design
execution: subagent
inputFile: squads/youtube-to-instagram/output/{run-id}/Lead-Magnets/
outputFile: squads/youtube-to-instagram/output/{run-id}/Lead-Magnets/
---

# Step 07: Diego Design — Geração do PDF da Isca Digital

Diego gera um PDF profissional para a isca digital criada no step anterior. O design é limpo e formal — adequado para um documento entregue via DM — usando a identidade visual da Sucesso Imóvel.

## Context Loading

Antes de iniciar, Diego deve carregar:
- `squads/youtube-to-instagram/output/{run-id}/Lead-Magnets/*.md` — Conteúdo de cada isca aprovada
- `squads/youtube-to-instagram/pipeline/data/visual-identity.md` — Identidade visual da Sucesso Imóvel
- `_opensquad/_memory/company.md` — Perfil da Sucesso Imóvel

## Estrutura de Output

Gerar dois arquivos em `output/{run-id}/Lead-Magnets/`:
- `lead-magnet-{PALAVRA-CTA}-{slug}.html` — HTML intermediário de renderização
- `lead-magnet-{PALAVRA-CTA}-{slug}.pdf` — PDF final entregável

## Instructions

### Para cada isca digital em `Lead-Magnets/*.md`:

**1. Obter base64 do logo colorido:**
```bash
python3 -c "import base64; data = open('assets/imagens/logos/SI-Logo-Color-Transp.png','rb').read(); print(base64.b64encode(data).decode())"
```

**2. Gerar o HTML do documento** com o seguinte design:

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <title>{TÍTULO DA ISCA} | Sucesso Imóvel</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@600;700;800&family=Inter:wght@400;500;600&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    @page { size: A4; margin: 0; }

    body {
      font-family: 'Inter', sans-serif;
      background: #FFFFFF;
      color: #1A1A2E;
      width: 210mm;
      min-height: 297mm;
      padding: 0;
    }

    /* ── HEADER ── */
    .doc-header {
      background: linear-gradient(135deg, #1A0A2E 0%, #2D1052 100%);
      padding: 36px 48px 32px;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
    .doc-header img { height: 40px; }
    .doc-header-badge {
      font-size: 11px; font-weight: 700; color: rgba(255,255,255,0.6);
      text-transform: uppercase; letter-spacing: 1.5px;
    }

    /* ── TITLE SECTION ── */
    .doc-title-section {
      background: #F8F5FF;
      padding: 32px 48px;
      border-bottom: 3px solid #A855F7;
    }
    .doc-format-tag {
      display: inline-block; font-size: 11px; font-weight: 700;
      color: #7B2FBE; text-transform: uppercase; letter-spacing: 1.5px;
      background: rgba(168,85,247,0.1); padding: 4px 12px;
      border-radius: 100px; margin-bottom: 12px;
    }
    .doc-title {
      font-family: 'Montserrat', sans-serif;
      font-size: 26px; font-weight: 800; color: #1A1A2E; line-height: 1.3;
    }
    .doc-subtitle {
      font-size: 14px; color: #6B7280; margin-top: 8px; line-height: 1.5;
    }

    /* ── BODY ── */
    .doc-body { padding: 40px 48px; }

    .doc-intro {
      font-size: 14px; line-height: 1.7; color: #374151;
      background: #F9FAFB; border-left: 4px solid #A855F7;
      padding: 16px 20px; border-radius: 0 8px 8px 0;
      margin-bottom: 32px;
    }

    /* Checklist items */
    .checklist-category {
      font-family: 'Montserrat', sans-serif;
      font-size: 13px; font-weight: 700; color: #7B2FBE;
      text-transform: uppercase; letter-spacing: 1px;
      margin: 28px 0 12px;
    }
    .checklist-item {
      display: flex; gap: 12px; align-items: flex-start;
      padding: 10px 0; border-bottom: 1px solid #F3F4F6;
    }
    .checklist-box {
      width: 18px; height: 18px; min-width: 18px;
      border: 2px solid #A855F7; border-radius: 4px; margin-top: 2px;
    }
    .checklist-item-text { font-size: 14px; line-height: 1.6; color: #1A1A2E; }
    .checklist-item-note { font-size: 12px; color: #6B7280; margin-top: 4px; }

    /* Guide sections */
    .section-number {
      display: inline-flex; align-items: center; justify-content: center;
      width: 28px; height: 28px; background: #7B2FBE;
      color: #fff; font-family: 'Montserrat', sans-serif;
      font-size: 13px; font-weight: 800; border-radius: 50%;
      margin-right: 12px; flex-shrink: 0;
    }
    .section-header {
      display: flex; align-items: center;
      font-family: 'Montserrat', sans-serif;
      font-size: 16px; font-weight: 700; color: #1A1A2E;
      margin: 28px 0 12px;
    }
    .section-body { font-size: 14px; line-height: 1.75; color: #374151; }
    .section-example {
      background: #F8F5FF; border-radius: 8px;
      padding: 14px 18px; margin-top: 12px;
      font-size: 13px; color: #4B5563; line-height: 1.6;
    }
    .section-example::before {
      content: "Exemplo prático: ";
      font-weight: 700; color: #7B2FBE;
    }

    /* Glossary */
    .glossary-term {
      font-family: 'Montserrat', sans-serif;
      font-size: 14px; font-weight: 700; color: #7B2FBE;
      margin: 24px 0 6px;
    }
    .glossary-def { font-size: 14px; line-height: 1.7; color: #374151; }
    .glossary-application {
      font-size: 12px; color: #6B7280; margin-top: 6px;
      font-style: italic;
    }

    /* Model fields */
    .model-field {
      background: #F9FAFB; border: 1px dashed #D1D5DB;
      border-radius: 6px; padding: 12px 16px; margin: 8px 0;
      font-size: 14px; color: #374151;
    }
    .model-field-label {
      font-size: 11px; font-weight: 600; color: #7B2FBE;
      text-transform: uppercase; letter-spacing: 1px; margin-bottom: 4px;
    }
    .model-note {
      font-size: 12px; color: #6B7280; margin-top: 6px; font-style: italic;
    }

    /* ── FOOTER ── */
    .doc-footer {
      background: #F8F5FF; border-top: 1px solid #E9D5FF;
      padding: 20px 48px;
      display: flex; align-items: center; justify-content: space-between;
      margin-top: 48px;
    }
    .doc-footer-brand {
      font-size: 12px; font-weight: 600; color: #7B2FBE;
    }
    .doc-footer-note {
      font-size: 11px; color: #9CA3AF; max-width: 420px; text-align: right;
    }
  </style>
</head>
<body>

  <div class="doc-header">
    <img src="data:image/png;base64,{LOGO_COLOR_B64}" alt="Sucesso Imóvel" />
    <div class="doc-header-badge">Direito Imobiliário</div>
  </div>

  <div class="doc-title-section">
    <div class="doc-format-tag">{FORMATO — ex: Checklist / Guia / Modelo}</div>
    <div class="doc-title">{TÍTULO COMPLETO DA ISCA}</div>
    <div class="doc-subtitle">{SUBTÍTULO OU INSTRUÇÃO DE USO — extraído do conteúdo}</div>
  </div>

  <div class="doc-body">
    <div class="doc-intro">{INTRODUÇÃO — extraída do conteúdo Markdown}</div>

    {CONTEÚDO PRINCIPAL — renderizado conforme o formato:
      - Checklist: .checklist-category + .checklist-item para cada item
      - Guia: .section-header + .section-body + .section-example para cada seção
      - Modelo: .model-field para cada campo preenchível
      - Glossário: .glossary-term + .glossary-def + .glossary-application
      - Mini-guia: mesma estrutura do guia, condensada
    }
  </div>

  <div class="doc-footer">
    <div class="doc-footer-brand">Sucesso Imóvel — especialistas em direito imobiliário</div>
    <div class="doc-footer-note">Este material é de uso exclusivo do destinatário. Para dúvidas jurídicas específicas, consulte nossa equipe.</div>
  </div>

</body>
</html>
```

**3. Salvar o HTML** como `_html/lead-magnet-{PALAVRA-CTA}-{slug}.html`.

**4. Renderizar como PDF** usando Chrome headless:
```bash
"{CHROME_PATH}" \
  --headless=new \
  --print-to-pdf="squads/youtube-to-instagram/output/{run-id}/Lead-Magnets/lead-magnet-{PALAVRA-CTA}-{slug}.pdf" \
  --print-to-pdf-no-header \
  --no-margins \
  "squads/youtube-to-instagram/output/{run-id}/Lead-Magnets/lead-magnet-{PALAVRA-CTA}-{slug}.html"
```

Onde `{CHROME_PATH}` é o binário do Chrome disponível no sistema (verificar em `~/.cache/puppeteer/` ou `/Applications/Google Chrome.app/`).

**5. Verificar** que o PDF foi gerado e tem conteúdo legível.



## Quality Criteria

- [ ] Um PDF gerado para cada isca digital aprovada
- [ ] HTML intermediário salvo em `_html/`
- [ ] Design limpo e profissional — fundo branco, accent roxo SI
- [ ] Logo colorido da Sucesso Imóvel no header
- [ ] Formato correto por tipo (checklist com caixas, guia com seções numeradas, etc.)
- [ ] Rodapé com menção à Sucesso Imóvel e nota de uso exclusivo
- [ ] PDFs salvos em `output/{run-id}/Lead-Magnets/`
- [ ] Arquivos nomeados com prefixo `lead-magnet-{PALAVRA-CTA}-`

## Veto Conditions

1. PDF não gerado ou arquivo vazio
2. Conteúdo do MD não renderizado no HTML (campos em branco ou placeholders visíveis)
3. Logo ausente no header
4. Formato visual incorreto para o tipo de isca (ex: checklist sem caixas)
5. Arquivos salvos fora da pasta `Lead-Magnets/`

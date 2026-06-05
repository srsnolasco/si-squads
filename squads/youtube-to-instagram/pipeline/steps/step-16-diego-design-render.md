---
type: agent
agent: diego-design
execution: subagent
inputFile: squads/youtube-to-instagram/output/{run-id}/Posts/post-content.md
outputFile: squads/youtube-to-instagram/output/{run-id}/Posts/
skill: image-creator
---

# Step 16: Diego Design — Criação e Renderização dos Posts

Diego Design transforma o conteúdo aprovado em imagens PNG para os 5 posts: 3 posts únicos, 1 Seg-CT e 1 Sex-CCTA.

## Context Loading

Antes de iniciar, Diego deve carregar:
- `squads/youtube-to-instagram/output/{run-id}/Posts/post-content.md` — Conteúdo aprovado
- `squads/youtube-to-instagram/pipeline/data/visual-identity.md` — Identidade visual
- `squads/youtube-to-instagram/pipeline/data/template-reference.html` — Template Seg-CT Premium Dark
- `squads/youtube-to-instagram/_templates/single-post-template.html` — Template Ter-PU1 (roxo)
- `squads/youtube-to-instagram/_templates/single-post-2-template.html` — Template Qua-PU2 (carvão/roxo claro)
- `squads/youtube-to-instagram/_templates/single-post-3-template.html` — Template Qui-PU3 (branco/lavanda)
- `squads/youtube-to-instagram/_memory/memories.md` — Regras e especificações dos templates

## Estrutura de Output

Os arquivos são separados em duas pastas:

**`output/{run-id}/Posts/`** — apenas os PNGs finais (entregáveis):
- `{slug}-03-Ter-PU1.png` — Ter-PU1 (1080×1350)
- `{slug}-04-Qua-PU2.png` — Qua-PU2 (1080×1350)
- `{slug}-05-Qui-PU3.png` — Qui-PU3 (1080×1350)
- `{slug}-02-Seg-CT-slide-01.png` a `{slug}-02-Seg-CT-slide-NN.png` — Seg-CT (1080×1440)
- `{slug}-06-Sex-CCTA-slide-01.png` a `{slug}-06-Sex-CCTA-slide-NN.png` — Sex-CCTA (1080×1440)

**`output/{run-id}/_html/`** — HTMLs de renderização (fonte dos PNGs, para consulta futura):
- `{slug}-03-Ter-PU1.html`
- `{slug}-04-Qua-PU2.html`
- `{slug}-05-Qui-PU3.html`
- `{slug}-02-Seg-CT-slide-01.html` a `{slug}-02-Seg-CT-slide-NN.html`
- `{slug}-06-Sex-CCTA-slide-01.html` a `{slug}-06-Sex-CCTA-slide-NN.html`

## Instructions

### Tarefa 0: Preparação

1. Criar os diretórios necessários se não existirem:
   - `output/{run-id}/Posts/` — PNGs finais
   - `output/{run-id}/_html/` — HTMLs de renderização
2. **Extrair o slug do run-id** para usar como prefixo nos nomes de arquivo:
   ```bash
   python3 -c "run_id='{run-id}'; parts=run_id.split('-', 3); print(parts[3] if len(parts) > 3 else 'post')"
   ```
   Salvar o resultado na variável `SLUG`. Exemplo: run-id `2026-05-13-201921-definicao-de-posse` → `SLUG=definicao-de-posse`.
3. Obter base64 do logo branco: `python3 -c "import base64; data = open('assets/imagens/logos/SI-Logo-Branco-Transp.png','rb').read(); print(base64.b64encode(data).decode())"` — salvar na variável `LOGO_B64`.
4. Obter base64 do logo colorido (para Post 3, fundo claro): `python3 -c "import base64; data = open('assets/imagens/logos/SI-Logo-Color-Transp.png','rb').read(); print(base64.b64encode(data).decode())"` — salvar na variável `LOGO_COLOR_B64`.
5. Ler `output/{run-id}/selected-jeorge-photo.md` para saber qual foto usar no Ter-PU1 — extrair o campo `Arquivo:`.
6. Iniciar servidor HTTP apontando para `_html/`: `python3 -m http.server 8765 --directory "{absolute_path}/_html/" &`

---

### Tarefa 1: Ter-PU1 — Roxo (com foto Dr. Jeorge)

1. Ler o template `_templates/single-post-template.html`.
2. Ler `output/{run-id}/selected-jeorge-photo.md` — extrair o campo `Arquivo:`.
   Obter base64: `python3 -c "import base64; data = open('/Users/sandronolasco/Antigravity/Projetos/SucessoImovel/si-squads/assets/imagens/fotos-ceo/{nome-arquivo}','rb').read(); print(base64.b64encode(data).decode())"`
3. Substituir todos os placeholders `{{...}}` com o conteúdo do post-content.md.
   - `{{LOGO_B64}}` → LOGO_B64
   - `{{JEORGE_B64}}` → base64 da foto
   - `{{TAG}}`, `{{EYEBROW}}`, `{{HEADLINE}}`, `{{BODY_TEXT}}`, `{{BADGE_TEXT}}`, `{{CTA_TEXT}}`
4. Salvar como `_html/{SLUG}-single-post-1.html`.
5. Renderizar:
   - `browser_navigate` → `http://localhost:8765/_html/{SLUG}-single-post-1.html`
   - `browser_resize` → 1080 × 1350
   - `browser_take_screenshot` → `Posts/{SLUG}-single-post-1.png`
6. Verificar visualmente: logo legível (92px), headline completa sem truncamento, card centralizado, CTA proeminente.

---

### Tarefa 2: Qua-PU2 — Carvão/Roxo Claro (com imagem IA)

#### 2a. Gerar imagem com image-ai-generator

1. Ler o arquivo `output/{run-id}/ai-image-prompt-post2.md` para extrair o prompt em inglês. Ao usar o prompt, **sempre acrescentar ao final**: `absolutely no text, no words, no letters, no signs, no stamps anywhere in the image — purely visual, zero typography` — mesmo que o prompt já contenha essa instrução, reforçar sempre.
2. Verificar se já existe imagem gerada: `output/{run-id}/ai-image-2.png` ou `output/{run-id}/ai-image-2.jpg`.
   - Se existir: pular para o passo 2b diretamente.
   - Se não existir: gerar em **modo test** primeiro:
     ```bash
     source .env && python3 skills/image-ai-generator/scripts/generate.py \
       --prompt "{prompt extraído do ai-image-prompt-post2.md}" \
       --output "squads/youtube-to-instagram/output/{run-id}/ai-image-2-test.jpg" \
       --mode test
     ```
3. Verificar visualmente a imagem test gerada. Se composição e tema estiverem adequados:
   ```bash
   source .env && python3 skills/image-ai-generator/scripts/generate.py \
     --prompt "{mesmo prompt}" \
     --output "squads/youtube-to-instagram/output/{run-id}/ai-image-2.jpg" \
     --mode production
   ```
4. Se a geração falhar (ex: OPENROUTER_API_KEY ausente ou erro de API): usar placeholder CSS e registrar aviso — **não bloquear o pipeline**.

#### 2b. Renderizar Post 2

1. Ler o template `_templates/single-post-2-template.html`.
2. Obter base64 da imagem gerada `output/{run-id}/ai-image-2.jpg` (ou `ai-image-2.png`):
   ```bash
   python3 -c "import base64; data = open('squads/youtube-to-instagram/output/{run-id}/ai-image-2.jpg','rb').read(); print(base64.b64encode(data).decode())"
   ```
   - Se nenhuma imagem existir: usar placeholder SVG/gradiente escuro como fallback.
3. Substituir todos os placeholders com o conteúdo do post-content.md.
4. Salvar como `_html/{SLUG}-single-post-2.html`.
5. Renderizar:
   - `browser_navigate` → `http://localhost:8765/_html/{SLUG}-single-post-2.html`
   - `browser_resize` → 1080 × 1350
   - `browser_take_screenshot` → `Posts/{SLUG}-single-post-2.png`
6. Verificar: imagem hero visível (IA ou placeholder), headline legível, card com body text, CTA pede like.

---

### Tarefa 3: Qui-PU3 — Branco/Lavanda (só texto)

1. Ler o template `_templates/single-post-3-template.html`.
2. Substituir todos os placeholders com o conteúdo do post-content.md (campos do Qui-PU3).
   - `{{LOGO_B64}}` → **LOGO_COLOR_B64** (logo colorido — fundo claro!)
   - Incluir `{{QUOTE_TEXT}}` com o texto de destaque.
3. Salvar como `_html/{SLUG}-single-post-3.html`.
4. Renderizar:
   - `browser_navigate` → `http://localhost:8765/_html/{SLUG}-single-post-3.html`
   - `browser_resize` → 1080 × 1350
   - `browser_take_screenshot` → `Posts/{SLUG}-single-post-3.png`
5. Verificar: layout 100% tipográfico, quote box destacado, CTA pede para seguir.

---

### Tarefa 4: Seg-CT — Carrossel Tutorial Premium Dark Roxo

1. Ler `pipeline/data/template-reference.html` como modelo.
2. **Determinar a variação de cada slide** pela regra A→B→C definida em `pipeline/data/visual-identity.md`:
   - Slide 1 (Capa) → `var-a`
   - Slide 2 → `var-b`
   - Slide 3 → `var-c`
   - Slide 4 → `var-a` … ciclo continua
   - Último slide (CTA) → `var-a` sempre (bookend com a capa)
3. Para cada slide do Seg-CT:
   a. Criar HTML baseado no template Premium Dark; aplicar a classe da variação no `<body>` (ex: `<body class="var-b">`)
   b. Aplicar accent keywords em `color: #A855F7`
   c. **Header:** logo branco centralizado (`height: 112px`, `justify-content: center`); tag no canto superior direito absoluto (`position:absolute; top:44px; right:72px; border-radius:100px`)
   d. **Eyebrow:** `font-size: 30px` — mais destacado
   e. **Conteúdo:** iniciar em `top: 220px` para dar espaço ao header
   f. **Botão ARRASTE:** `← ARRASTE` (seta à ESQUERDA), estilo botão transparente levemente arredondado: `color:rgba(255,255,255,0.90); background:rgba(255,255,255,0.08); border:2px solid rgba(255,255,255,0.30); border-radius:12px; padding:16px 36px; font-size:36px; font-weight:700`
   g. **Slide CTA (último):** o bloco de CTA deve sempre incluir um argumento persuasivo para salvar e compartilhar — não usar a fórmula genérica "salva e compartilha". Em vez disso, criar uma frase que justifique o salvamento ("você vai precisar disso antes do próximo fechamento", "esse conteúdo aparece na hora certa") e o compartilhamento ("manda para o colega que fechou sem verificar", "um corretor que você conhece vai agradecer"). O argumento deve ser específico ao tema do Seg-CT.
   h. Salvar como `_html/{SLUG}-slide-01.html`, `_html/{SLUG}-slide-02.html`, etc.
4. Renderizar cada slide:
   - `browser_resize` → 1080 × 1440 (Seg-CT é mais alto que post único)
   - `browser_take_screenshot` → `Posts/{SLUG}-slide-01.png`, etc.
5. Verificar slide 1 antes de continuar o batch.

---

### Tarefa 5: Sex-CCTA — Carrossel Isca Digital Premium Dark Roxo

1. Ler `pipeline/data/template-reference.html` como modelo (mesmo template do Seg-CT).
2. Ler `lead-magnet-ideas.md` para extrair a **palavra do CTA** — usar exatamente essa palavra no último slide.
3. **Determinar a variação de cada slide** pela mesma regra A→B→C do Seg-CT:
   - Slide 1 (Capa) → `var-a`
   - Slide 2 → `var-b`
   - Slide 3 → `var-c`
   - Slide 4 → `var-a` … ciclo continua
   - Último slide (CTA) → `var-a` sempre
4. Para cada slide do Sex-CCTA:
   a. Criar HTML baseado no template Premium Dark; aplicar a classe da variação no `<body>` (ex: `<body class="var-c">`)
   b. Aplicar accent keywords em `color: #A855F7`
   c. **Header:** logo branco centralizado (`height: 112px`); tag no canto superior direito
   d. **Eyebrow:** `font-size: 30px`
   e. **Conteúdo:** iniciar em `top: 220px`
   f. **Botão ARRASTE:** `← ARRASTE` (seta à ESQUERDA), mesmo estilo do Seg-CT
   g. **Slide CTA (último):** "Comenta [PALAVRA] aqui embaixo e receba [referência genérica ao material]" — PALAVRA extraída de `lead-magnet-ideas.md`
   h. Salvar como `_html/{SLUG}-ccta-slide-01.html`, `_html/{SLUG}-ccta-slide-02.html`, etc.
5. Renderizar cada slide:
   - `browser_resize` → 1080 × 1440
   - `browser_take_screenshot` → `Posts/{SLUG}-ccta-slide-01.png`, etc.
6. Verificar slide 1 antes de continuar o batch.

---

### Tarefa 6: Encerramento

1. Parar servidor HTTP: `pkill -f "http.server 8765" 2>/dev/null || true`
2. Listar todos os PNGs gerados em `Posts/`.
3. Confirmar contagem: 3 single posts + N slides do Seg-CT + N slides do Sex-CCTA.

## Output Format

```
Posts gerados em output/{run-id}/Posts/:

POST ÚNICOS (1080×1350):
- {slug}-03-Ter-PU1.png ✅ — Roxo | {headline}
- {slug}-04-Qua-PU2.png ✅ — Carvão/Roxo Claro | {headline}
- {slug}-05-Qui-PU3.png ✅ — Branco/Lavanda | {headline}

Seg-CT — CARROSSEL TUTORIAL (1080×1440):
- {slug}-02-Seg-CT-slide-01.png ✅ — Capa
- {slug}-02-Seg-CT-slide-02.png ✅
[...]
- {slug}-02-Seg-CT-slide-NN.png ✅ — CTA (salvar)

Sex-CCTA — CARROSSEL ISCA DIGITAL (1080×1440):
- {slug}-06-Sex-CCTA-slide-01.png ✅ — Capa
- {slug}-06-Sex-CCTA-slide-02.png ✅
[...]
- {slug}-06-Sex-CCTA-slide-NN.png ✅ — CTA (comentar [PALAVRA])

Total: 3 posts únicos + N slides de Seg-CT + N slides de Sex-CCTA

HTMLs de renderização salvos em output/{run-id}/_html/:
- {slug}-03-Ter-PU1.html
- {slug}-04-Qua-PU2.html
- {slug}-05-Qui-PU3.html
- {slug}-02-Seg-CT-slide-01.html a {slug}-02-Seg-CT-slide-NN.html
- {slug}-06-Sex-CCTA-slide-01.html a {slug}-06-Sex-CCTA-slide-NN.html
```

## Quality Criteria

- [ ] Post 1: template roxo/preto, foto Dr. Jeorge selecionada no step-05, logo branco 92px
- [ ] Post 2: template carvão/roxo-claro (#C084FC), imagem IA (ou placeholder), CTA pede like
- [ ] Post 3: template branco/lavanda, 100% tipográfico, quote box presente, **logo colorido**, CTA pede seguir
- [ ] Seg-CT: logo 112px centralizado, eyebrow 30px, conteúdo top:220px, botão `← ARRASTE` estilo transparente branco, slides 1080×1440
- [ ] Seg-CT: slides alternam var-a → var-b → var-c → var-a…; capa e CTA sempre var-a
- [ ] Sex-CCTA: mesmo padrão visual do Seg-CT, CTA do último slide usa palavra extraída de `lead-magnet-ideas.md`, arquivos nomeados com prefixo `-ccta-slide-`
- [ ] Sex-CCTA: slides alternam var-a → var-b → var-c → var-a…; capa e CTA sempre var-a
- [ ] Todos os posts únicos: 1080×1350
- [ ] Card de conteúdo centralizado (bottom: 240px) em todos os posts únicos
- [ ] Nomenclatura correta: `{slug}-03-Ter-PU1`, `{slug}-04-Qua-PU2`, `{slug}-05-Qui-PU3`, `{slug}-02-Seg-CT-slide-NN`, `{slug}-06-Sex-CCTA-slide-NN`
- [ ] PNGs salvos em `Posts/`, HTMLs salvos em `_html/` — pastas separadas
- [ ] Servidor HTTP parado após o último slide

## Veto Conditions

1. Post 1 usa template carvão ou branco (deve ser roxo/preto)
2. Post 2 usa logo colorido (deve ser logo branco — fundo escuro)
3. Post 3 usa logo branco em vez do logo colorido (fundo claro exige logo colorido)
4. Post 3 tem foto de pessoa (deve ser 100% texto)
5. Seg-CT usa seta `ARRASTE →` (deve ser `← ARRASTE`)
6. Sex-CCTA usa seta `ARRASTE →` (deve ser `← ARRASTE`)
7. Seg-CT ou Sex-CCTA com todos os slides na mesma variação (alternância obrigatória)
8. Capa ou CTA de qualquer carrossel com variação diferente de var-a
7. Sex-CCTA com CTA usando palavra diferente da registrada em `lead-magnet-ideas.md`
8. Algum PNG não foi gerado
7. Arquivos gerados sem prefixo do slug (ex: `single-post-1.png` em vez de `{slug}-single-post-1.png`)

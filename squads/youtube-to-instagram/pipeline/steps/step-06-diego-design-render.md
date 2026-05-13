---
type: agent
agent: diego-design
execution: subagent
inputFile: squads/youtube-to-instagram/output/post-content.md
outputFile: squads/youtube-to-instagram/output/{run-id}/Posts/
skill: image-creator
---

# Step 06: Diego Design — Criação e Renderização dos Posts

Diego Design transforma o conteúdo aprovado em imagens PNG para os 4 posts: 3 posts únicos e 1 carrossel.

## Context Loading

Antes de iniciar, Diego deve carregar:
- `squads/youtube-to-instagram/output/post-content.md` — Conteúdo aprovado
- `squads/youtube-to-instagram/pipeline/data/visual-identity.md` — Identidade visual
- `squads/youtube-to-instagram/pipeline/data/template-reference.html` — Template carrossel Premium Dark
- `squads/youtube-to-instagram/_templates/single-post-template.html` — Template Post Único 1 (roxo)
- `squads/youtube-to-instagram/_templates/single-post-2-template.html` — Template Post Único 2 (carvão/roxo claro)
- `squads/youtube-to-instagram/_templates/single-post-3-template.html` — Template Post Único 3 (branco/lavanda)
- `squads/youtube-to-instagram/_memory/memories.md` — Regras e especificações dos templates

## Estrutura de Output

Todos os arquivos vão para `output/{run-id}/Posts/`, com prefixo `{slug}` no nome:
- `{slug}-single-post-1.html` + `{slug}-single-post-1.png` — Post Único 1 (1080×1350)
- `{slug}-single-post-2.html` + `{slug}-single-post-2.png` — Post Único 2 (1080×1350)
- `{slug}-single-post-3.html` + `{slug}-single-post-3.png` — Post Único 3 (1080×1350)
- `{slug}-slide-01.html` a `{slug}-slide-NN.html` + PNGs — Carrossel (1080×1440)

## Instructions

### Tarefa 0: Preparação

1. Criar o diretório `output/{run-id}/Posts/` se não existir.
2. **Extrair o slug do run-id** para usar como prefixo nos nomes de arquivo:
   ```bash
   python3 -c "run_id='{run-id}'; parts=run_id.split('-', 3); print(parts[3] if len(parts) > 3 else 'post')"
   ```
   Salvar o resultado na variável `SLUG`. Exemplo: run-id `2026-05-13-201921-definicao-de-posse` → `SLUG=definicao-de-posse`.
3. Obter base64 do logo branco: `python3 -c "import base64; data = open('assets/imagens/logos/SI-Logo-Branco-Transp.png','rb').read(); print(base64.b64encode(data).decode())"` — salvar na variável `LOGO_B64`.
4. Obter base64 do logo colorido (para Post 3, fundo claro): `python3 -c "import base64; data = open('assets/imagens/logos/SI-Logo-Color-Transp.png','rb').read(); print(base64.b64encode(data).decode())"` — salvar na variável `LOGO_COLOR_B64`.
5. Ler `output/{run-id}/selected-jeorge-photo.md` para saber qual foto usar no Post Único 1 — extrair o campo `Arquivo:`.
6. Iniciar servidor HTTP apontando para `Posts/`: `python3 -m http.server 8765 --directory "{absolute_path}/Posts/" &`

---

### Tarefa 1: Post Único 1 — Roxo (com foto Dr. Jeorge)

1. Ler o template `_templates/single-post-template.html`.
2. Usar o arquivo de foto lido em `output/{run-id}/selected-jeorge-photo.md` (campo "Arquivo:").
   Obter base64: `python3 -c "import base64; data = open('assets/imagens/jeorge/{nome-arquivo}','rb').read(); print(base64.b64encode(data).decode())"`
3. Substituir todos os placeholders `{{...}}` com o conteúdo do post-content.md.
   - `{{LOGO_B64}}` → LOGO_B64
   - `{{JEORGE_B64}}` → base64 da foto
   - `{{TAG}}`, `{{EYEBROW}}`, `{{HEADLINE}}`, `{{BODY_TEXT}}`, `{{BADGE_TEXT}}`, `{{CTA_TEXT}}`
4. Salvar como `Posts/{SLUG}-single-post-1.html`.
5. Renderizar:
   - `browser_navigate` → `http://localhost:8765/{SLUG}-single-post-1.html`
   - `browser_resize` → 1080 × 1350
   - `browser_take_screenshot` → `Posts/{SLUG}-single-post-1.png`
6. Verificar visualmente: logo legível (92px), headline completa sem truncamento, card centralizado, CTA proeminente.

---

### Tarefa 2: Post Único 2 — Carvão/Roxo Claro (com imagem IA)

#### 2a. Gerar imagem com image-ai-generator

1. Ler o arquivo `output/{run-id}/ai-image-prompt-post2.md` para extrair o prompt em inglês. Ao usar o prompt, **sempre acrescentar ao final**: `absolutely no text, no words, no letters, no signs, no stamps anywhere in the image — purely visual, zero typography` — mesmo que o prompt já contenha essa instrução, reforçar sempre.
2. Verificar se já existe imagem gerada: `output/{run-id}/ai-image-2.png` ou `output/{run-id}/ai-image-2.jpg`.
   - Se existir: pular para o passo 2b diretamente.
   - Se não existir: gerar em **modo test** primeiro:
     ```bash
     python3 skills/image-ai-generator/scripts/generate.py \
       --prompt "{prompt extraído do ai-image-prompt-post2.md}" \
       --output "squads/youtube-to-instagram/output/{run-id}/ai-image-2-test.jpg" \
       --mode test
     ```
3. Verificar visualmente a imagem test gerada. Se composição e tema estiverem adequados:
   ```bash
   python3 skills/image-ai-generator/scripts/generate.py \
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
4. Salvar como `Posts/{SLUG}-single-post-2.html`.
5. Renderizar:
   - `browser_navigate` → `http://localhost:8765/{SLUG}-single-post-2.html`
   - `browser_resize` → 1080 × 1350
   - `browser_take_screenshot` → `Posts/{SLUG}-single-post-2.png`
6. Verificar: imagem hero visível (IA ou placeholder), headline legível, card com body text, CTA pede like.

---

### Tarefa 3: Post Único 3 — Branco/Lavanda (só texto)

1. Ler o template `_templates/single-post-3-template.html`.
2. Substituir todos os placeholders com o conteúdo do post-content.md (campos do Post Único 3).
   - `{{LOGO_B64}}` → **LOGO_COLOR_B64** (logo colorido — fundo claro!)
   - Incluir `{{QUOTE_TEXT}}` com o texto de destaque.
3. Salvar como `Posts/{SLUG}-single-post-3.html`.
4. Renderizar:
   - `browser_navigate` → `http://localhost:8765/{SLUG}-single-post-3.html`
   - `browser_resize` → 1080 × 1350
   - `browser_take_screenshot` → `Posts/{SLUG}-single-post-3.png`
5. Verificar: layout 100% tipográfico, quote box destacado, CTA pede para seguir.

---

### Tarefa 4: Carrossel — Premium Dark Roxo

1. Ler `pipeline/data/template-reference.html` como modelo.
2. Para cada slide do carrossel:
   a. Criar HTML baseado no template Premium Dark (fundo roxo/preto, paleta #7B2FBE / #A855F7)
   b. Aplicar accent keywords em `color: #A855F7`
   c. **Header:** logo branco centralizado (`height: 112px`, `justify-content: center`); tag no canto superior direito absoluto (`position:absolute; top:44px; right:72px; border-radius:100px`)
   d. **Eyebrow:** `font-size: 30px` — mais destacado
   e. **Conteúdo:** iniciar em `top: 220px` para dar espaço ao header
   f. **Botão ARRASTE:** `← ARRASTE` (seta à ESQUERDA), estilo botão transparente levemente arredondado: `color:rgba(255,255,255,0.90); background:rgba(255,255,255,0.08); border:2px solid rgba(255,255,255,0.30); border-radius:12px; padding:16px 36px; font-size:36px; font-weight:700`
   g. **Slide CTA (último):** o bloco de CTA deve sempre incluir um argumento persuasivo para salvar e compartilhar — não usar a fórmula genérica "salva e compartilha". Em vez disso, criar uma frase que justifique o salvamento ("você vai precisar disso antes do próximo fechamento", "esse conteúdo aparece na hora certa") e o compartilhamento ("manda para o colega que fechou sem verificar", "um corretor que você conhece vai agradecer"). O argumento deve ser específico ao tema do carrossel.
   g. Salvar como `Posts/{SLUG}-slide-01.html`, `Posts/{SLUG}-slide-02.html`, etc.
3. Renderizar cada slide:
   - `browser_resize` → 1080 × 1440 (carrossel é mais alto que post único)
   - `browser_take_screenshot` → `Posts/{SLUG}-slide-01.png`, etc.
4. Verificar slide 1 antes de continuar o batch.

---

### Tarefa 5: Encerramento

1. Parar servidor HTTP: `pkill -f "http.server 8765" 2>/dev/null || true`
2. Listar todos os PNGs gerados em `Posts/`.
3. Confirmar contagem: 3 single posts + N slides do carrossel.

## Output Format

```
Posts gerados em output/{run-id}/Posts/:

POST ÚNICOS (1080×1350):
- {slug}-single-post-1.png ✅ — Roxo | {headline}
- {slug}-single-post-2.png ✅ — Carvão/Roxo Claro | {headline}
- {slug}-single-post-3.png ✅ — Branco/Lavanda | {headline}

CARROSSEL (1080×1440):
- {slug}-slide-01.png ✅ — Capa
- {slug}-slide-02.png ✅
[...]
- {slug}-slide-NN.png ✅ — CTA

Total: 3 posts únicos + N slides de carrossel
```

## Quality Criteria

- [ ] Post 1: template roxo/preto, foto Dr. Jeorge selecionada no step-05, logo branco 92px
- [ ] Post 2: template carvão/roxo-claro (#C084FC), imagem IA (ou placeholder), CTA pede like
- [ ] Post 3: template branco/lavanda, 100% tipográfico, quote box presente, **logo colorido**, CTA pede seguir
- [ ] Carrossel: logo 112px centralizado, eyebrow 30px, conteúdo top:220px, botão `← ARRASTE` estilo transparente branco, slides 1080×1440
- [ ] Todos os posts únicos: 1080×1350
- [ ] Card de conteúdo centralizado (bottom: 240px) em todos os posts únicos
- [ ] Todos os arquivos nomeados com prefixo `{slug}-`
- [ ] Servidor HTTP parado após o último slide

## Veto Conditions

1. Post 1 usa template carvão ou branco (deve ser roxo/preto)
2. Post 2 usa logo colorido (deve ser logo branco — fundo escuro)
3. Post 3 usa logo branco em vez do logo colorido (fundo claro exige logo colorido)
4. Post 3 tem foto de pessoa (deve ser 100% texto)
5. Carrossel usa seta `ARRASTE →` (deve ser `← ARRASTE`)
6. Algum PNG não foi gerado
7. Arquivos gerados sem prefixo do slug (ex: `single-post-1.png` em vez de `{slug}-single-post-1.png`)

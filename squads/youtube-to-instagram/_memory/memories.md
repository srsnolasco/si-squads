# Squad Memory: YouTube → Instagram

## Estilo de Escrita

- Usuário prefere tom Provocativo Inteligente sobre Alerta e Urgência para conteúdo jurídico do STJ.
- Hook contrarian aprovado: estrutura "Você aprendeu X. O STJ discordou." funciona para a audiência.
- Hook "dado implícito" aprovado: estrutura "Quando X acontece, Y é o resultado. É assim que Z." conecta causa e efeito de forma memorável.

## Design Visual

- Logo real da Sucesso Imóvel deve aparecer no header de todos os slides (usar versão branca para fundos escuros). Tamanho: 92px de altura.
- Fundo Premium Dark: `linear-gradient(155deg, #0C0018 0%, #1A0A2E 40%, #0A0A0A 100%)`.

## Template Aprovado — Post Único

Arquivo: `squads/youtube-to-instagram/_templates/single-post-template.html`
Aprovado em: 2026-06-04 (v11 — aprovado pelo usuário)

**Especificações obrigatórias:**
- Proporção: **1080×1350px** (4:5 — feed Instagram)
- Layout: fundo único + headline à esquerda + Dr. Jeorge à direita
- **SEM logo, SEM tag ({{TAG}}), SEM eyebrow, SEM divider** — esses elementos foram removidos do template
- Headline: `left: 80px; width: 420px; top: 60px` — subida para o topo
- Foto Dr. Jeorge: `right: 0; top: 0; width: 660px` — maior e a partir do topo, com mask-image fade na base
- Accent-line vertical roxa: `left: 60px; top: 80px`
- Card de conteúdo: `bottom: 240px; left/right: 52px`, fundo `rgba(5,0,12,0.50)` com blur
- Body text: 38px Inter 500
- **Badge:** `display: flex; width: fit-content; margin: 0 auto` — **centralizado horizontalmente**
- Badge: 26px Inter 600
- CTA bar: 200px, gradiente roxo sólido, Montserrat 900 46px, **sem emojis**, **sem @handle**
- Foto buscada em: `/Users/sandronolasco/Antigravity/Projetos/SucessoImovel/si-squads/assets/imagens/fotos-ceo/`

## Template Aprovado — Post Único 2

Arquivo: `squads/youtube-to-instagram/_templates/single-post-2-template.html`
Aprovado em: 2026-06-04 (v3.0 — tipografia e espaçamento finalizados pelo usuário)

**Layout de zonas fixas (nunca se sobrepõem):**
- `0–560px` — AI Image hero (fade inferior de 280px)
- `0–156px` — Header (logo 112px + tag) z-index 20
- `180–640px` — Headline zone (`max-height: 460px`, sobre a imagem) z-index 20
- `650–1050px` — Content card (400px, centralizado verticalmente) z-index 30
- `1140–1350px` — CTA bar (210px, gradiente roxo)

**Tipografia:**
- Logo: `height: 150px`
- Tag: Inter 600, 26px
- Eyebrow: Inter 600, 24px, letter-spacing 4px
- **Divider:** `margin: 0 auto 48px auto` — espaço de uma linha entre eyebrow e headline (obrigatório)
- **Headline:** Montserrat 900, `font-size: clamp(32px, 4vw, 52px)`, line-height 1.2, letter-spacing -0.5px, `max-width: 900px; margin: 0 auto`, centralizada
- **Body text:** Inter 500, **43px**, line-height 1.55, máx 4 linhas (`-webkit-line-clamp: 4`)
- Badge: Inter 600, 28px
- CTA: Montserrat 900, 48px, centralizado

**Regras obrigatórias:**
- Headline zone com `max-height: 460px; overflow: hidden` — nunca `height` fixo
- **Nunca usar `-webkit-line-clamp` na headline** — causa corte de texto
- **Nunca usar `<br>` no headline** — texto flui como prosa contínua para evitar palavras isoladas em linha
- Card com `justify-content: center`
- Logo branco (`SI-Logo-Branco-Transp.png`) — fundo sempre escuro
- CTA **sempre** pedido de like
- Imagem IA: sem texto, sem palavras, sem letras — acrescentar ao prompt: `absolutely no text, no words, no letters, no signs, no stamps anywhere in the image — purely visual, zero typography`
- Gerar imagem via `source .env && python3 skills/image-ai-generator/scripts/generate.py`

## Template Aprovado — Post Único 3

Arquivo: `squads/youtube-to-instagram/_templates/single-post-3-template.html`
Aprovado em: 2026-06-04 (v3.0 — aprovado pelo usuário)

**Layout de zonas fixas:**
- `0–156px` — Header: logo colorido **centralizado**
- `168–490px` — Headline zone (`max-height: 420px`, eyebrow + divider + headline, left-aligned)
- `510–720px` — Quote box (210px: sub-headline de destaque)
- `760–1100px` — Content card (`top: 760px; bottom: 250px`, **sem badge**, 40px de margem simétrica entre quote box e CTA)
- `1140–1350px` — CTA bar (210px, 2 linhas)

**Tipografia:**
- Logo: `height: 150px`, **centralizado** horizontalmente — logo **COLORIDO** (`SI-Logo-Color-Transp.png`)
- Eyebrow: Inter 600, 24px, letter-spacing 4px
- **Divider:** `margin-bottom: 48px` — espaço de uma linha antes da headline (obrigatório)
- **Headline:** Montserrat 900, `font-size: clamp(32px, 4vw, 52px)`, line-height 1.2 — **nunca usar font-size fixo nem `-webkit-line-clamp`** (causa corte)
- Quote text: Montserrat 900, 44px, line-height 1.15
- **Body text:** Inter 500, **46px**, line-height 1.5
- **Badge: REMOVIDO** — não usar o campo `{{BADGE_TEXT}}` neste template
- CTA label (fixo): Inter 600, 26px, `"Siga nosso perfil:"`
- CTA main: Montserrat 900, 48px

**Regras obrigatórias:**
- Paleta CLARO: fundo `linear-gradient(155deg, #FAFAFA, #F3EEFF, #F8F5FF)`
- Logo COLORIDO — nunca branco neste post
- CTA sempre começa com `"Siga nosso perfil:"` fixo no HTML
- Layout 100% tipográfico — sem foto, sem imagem IA
- Não passar `{{BADGE_TEXT}}` — campo removido do template HTML

## Template Aprovado — Carrossel Premium Dark

Arquivo de referência: `squads/youtube-to-instagram/pipeline/data/template-reference.html`
Aprovado em: 2026-06-04 (versão definitiva — aprovada pelo usuário)

**Layout geral:**
- Dimensões: 1080×1440px
- Fundo: `linear-gradient(155deg, #0C0018 0%, #1A0A2E 40%, #0A0A0A 100%)`
- Accent line topo: `height:3px; background:linear-gradient(90deg,transparent,#7B2FBE,#A855F7,transparent)`

**Header (todos os slides):**
- Logo branco (`SI-Logo-Branco-Transp.png`) base64, `height:112px`, header `justify-content:center` — logo **centralizado**
- Tag: `position:absolute; top:44px; right:72px; border-radius:100px; font-size:26px; font-weight:600; color:#A855F7; padding:13px 30px`

**Tipografia e espaçamento:**
- Eyebrow: `font-size:30px; font-weight:700; color:#A855F7; letter-spacing:3px; text-transform:uppercase; margin-bottom:64px` — **obrigatório o espaço de 64px antes da headline**
- Headline capa: Montserrat 900, 68px, `color:#fff`, accent `color:#A855F7`
- Headline slides conteúdo: Montserrat 900, 64px
- Subtítulo (capa): `font-size:44px; font-weight:500; color:#9B9B9B; line-height:1.55; margin-top:24px`
- Card body: `font-size:34px; font-weight:500; color:rgba(255,255,255,0.85); line-height:1.55`

**Botão ARRASTE (slides 1 a N-1, exceto último):**
- Texto: `← ARRASTE` (seta à ESQUERDA — NUNCA à direita)
- `color:rgba(255,255,255,0.90); background:rgba(255,255,255,0.08); border:2px solid rgba(255,255,255,0.30); border-radius:12px; padding:16px 36px; font-size:36px; font-weight:700`
- **border-radius:12px** (levemente arredondado — 100px "pílula" é PROIBIDO)

**Slide CTA — último slide (sem botão ARRASTE):**
- NUNCA usar fórmula genérica "salva e compartilha"
- Sempre dois argumentos persuasivos específicos ao tema
- Bloco CTA: `background:linear-gradient(135deg,#3B0764,#6B21A8); border-radius:16px; padding:36px 44px`
- Texto CTA: Montserrat 900, 38px, `color:#fff`; detalhe complementar em `color:#DDD6FE`

**Regras obrigatórias:**
- Logo branco embedado como base64 — nunca path relativo
- Seta SEMPRE à esquerda: `← ARRASTE`
- Placeholders `{{LOGO_B64}}` e `{{TAG}}` substituídos antes de renderizar

## Estrutura de Conteúdo

- Progressão Mito → Realidade → Impacto prático → Checklist acionável → CTA aprovada pelo usuário.
- Slide de checklist numerado com frase de encerramento ("X itens. Zero surpresa.") tem alto potencial de save.

## Hashtags Oficiais

Todos os posts e legendas devem usar **somente** estas 6 hashtags — sem adições, sem substituições:

```
#sucessoimovel #corretordeimoveis #direitoimobiliario #corretorimobiliario #imobiliaria #imobiliariabarradatijuca
```

Hashtags temáticas geradas por IA (ex: #contratonulo, #prazoscontrato, #checklistjuridico) são **proibidas**.

## Proibições Explícitas

- **EMOJIS PROIBIDOS** em qualquer tipo de post — headline, body text, badge, CTA, legenda, hashtags, roteiros. Aplica-se a todos os outputs: Post Único 1, 2, 3, Carrossel, roteiro YouTube e roteiros Reels. Sem exceção.
- **NUNCA mencionar o nome do canal, especialista ou criador do vídeo de origem** em nenhum campo de nenhum post (headline, body, badge, CTA, legenda). Todo conteúdo produzido deve parecer criado pelo Dr. Jeorge Sodré ou pela Sucesso Imóvel. Para atribuição de autoridade no badge, usar "Dr. Jeorge Sodré | Sucesso Imóvel" ou referência legal direta (ex: "Código Civil | Art. 722").
- **EM-DASH (—) PROIBIDO** em qualquer campo de qualquer post — headline, body text, badge, CTA, legenda, quote text, subtítulo. Nunca usar o traço (—) como separador ou recurso estilístico. Substituir por: ponto final (.), dois-pontos (:), vírgula (,) ou reescrever a frase sem o traço.
- Nunca usar seta à direita da palavra no botão de arraste do carrossel ("Arraste →" é proibido — usar "← Arraste").

## Técnico (específico do squad)

- Nome da pasta de output: `YYYY-MM-DD-HHmmss-tema-slug` (data + hora + 1 a 3 palavras do tema em kebab-case).
- **Estrutura completa de subpastas obrigatória:**

| Pasta | Conteúdo |
|---|---|
| `v1/` | `youtube-focus.md`, `video-transcript.md`, `doc-source-analysis.md`, `doc-source-analysis.html`, `post-ideas.md`, `lead-magnet-ideas.md`, `approved-ideas.md`, `review.md` |
| `Posts/` | `post-content.md`, `post-content.html`, `selected-jeorge-photo.md`, `ai-image-prompt-post2.md`, `ai-image-2.jpg`, `ai-image-2-test.jpg`, todos os PNGs finais |
| `Prompts/` | `media-prompts.md`, `media-prompts.html` |
| `Roteiros/` | roteiro YouTube, roteiros Reels, roteiros Stories HTMLs |
| `Stories/` | arquivos MD de stories diários |
| `Lead-Magnets/` | HTML e PDF da isca digital |
| `Dashboard/` | `dashboard-semanal-{slug}.html` |
| `_html/` | HTMLs intermediários de renderização dos posts |
| `_scripts/` | scripts auxiliares gerados durante a execução (ex: `render-posts.mjs`) |

- Arquivos soltos na raiz do run-id: apenas `state.json` (gerenciado pelo pipeline runner — não mover).
- Caminhos relativos no dashboard para `Lead-Magnets/` devem usar `../Lead-Magnets/` (um nível acima da pasta `Dashboard/`).
- **Prompts Imagen (step 14):** 3 prompts nomeados e derivados diretamente dos posts correspondentes:
  - `01-Ter-PU1` — derivado do post Ter-PU1 (headline e body text)
  - `02-Qua-PU2` — derivado do post Qua-PU2 (headline e body text)
  - `03-Qui-PU3` — derivado do post Qui-PU3 (headline e body text)
  - Cada prompt: headline em português + sub-headline em português + prompt em inglês + legenda do post + hashtags
  - SEM logo, SEM badge — apenas headline + sub-headline na imagem gerada
  - **`media-prompts.html` — estrutura obrigatória de cada card:**
    - Bloco de prompt em inglês (monospace, fundo escuro)
    - Botão **"Copiar prompt"** logo abaixo do bloco — copia o texto do prompt, exibe "Copiado!" com check verde por 2s
    - Legenda completa
    - Hashtags como texto simples (`div.caption-tags`) logo abaixo da legenda — visíveis e incluídas na cópia
    - Botão **"Copiar legenda"** logo abaixo das hashtags — copia legenda + `\n\n` + hashtags juntos, pronto para colar no Instagram
    - HTML auto-suficiente: CSS inline + Google Fonts + JavaScript inline (funções `copyPrompt` e `copyCaption`)
  - **O texto DEVE aparecer na imagem** — headline e sub-headline escritas LITERALMENTE dentro do prompt em inglês para que o Imagen as renderize
  - **NUNCA usar "no text", "no words", "purely visual", "zero typography"** — o texto é o produto, não pode ser proibido
  - Estrutura do prompt: [background conservador temático] + [accent line roxa muda] + [bloco de tipografia com frases exatas em português] + [mood obrigatório] + [proibições]
  - Palavra-chave da headline em **roxo primário mudo #7B2FBE** — nunca #A855F7 (elétrico) nas imagens IA
  - **Estilo obrigatório das imagens IA: "prestigious law firm, premium legal editorial, authoritative, classical"**
  - **Proibidos nos prompts IA:** orbes brilhantes, gradientes elétricos violeta, "neon", "electric", "glowing", "sci-fi", "cinematic orbs", "futuristic" — a Sucesso Imóvel é consultoria jurídica, não startup de tecnologia
  - Background IA: carvão profundo neutro `#0D0D0F` → `#141418` — sem roxo saturado no gradiente de fundo
  - Texturas permitidas: mármore, papel envelhecido, madeira nobre, silhueta arquitetônica, balança da justiça em outline, livros de direito — sempre em baixíssima opacidade como watermark
- Logo embedado como base64 data URI — nunca como path relativo.
- **Nomenclatura obrigatória dos PNGs** (prefixo `{slug}` + número do dia + identificador do post):
  - `{slug}-02-Seg-CT-slide-01.png` … `{slug}-02-Seg-CT-slide-NN.png`
  - `{slug}-03-Ter-PU1.png`
  - `{slug}-04-Qua-PU2.png`
  - `{slug}-05-Qui-PU3.png`
  - `{slug}-06-Sex-CCTA-slide-01.png` … `{slug}-06-Sex-CCTA-slide-NN.png`
  - HTMLs de renderização seguem o mesmo padrão em `_html/`

## Dashboard Semanal (step 19)

**Localização obrigatória:** o arquivo HTML do dashboard deve ser salvo dentro da subpasta `Dashboard/` no output do run:
```
output/{run-id}/Dashboard/dashboard-semanal-{slug}.html
```
Caminhos relativos para a pasta `Lead-Magnets/` devem usar `../Lead-Magnets/` (um nível acima).

**Layout obrigatório: sidebar fixa à esquerda (220px) + área de conteúdo à direita.**

A navegação principal é feita por 4 botões na sidebar — cada um exibe uma view exclusiva (`display:none` / `display:block` via `showView(name)`):

| Botão | View ID | Conteúdo |
|---|---|---|
| Posts | `#view-posts` | Source card + nav por dia (Dom→Sáb) com todos os posts, reels e stories |
| Isca | `#view-isca` | Título da isca, palavra CTA, descrição, iframe do HTML da isca e botão de download |
| Vídeo | `#view-video` | Relatório do vídeo (doc-source-analysis) + Roteiro YouTube em grid 2 colunas |
| Prompts | `#view-prompts` | 3 prompts Imagen com botões "Copiar prompt" e "Copiar legenda" (mesmo padrão do media-prompts.html) |

- View `Posts` começa ativa (`class="view active"`)
- Link "Suporte" removido da nav de dias — conteúdo redistribuído para Vídeo e Prompts
- A seção `support-section` antiga não existe mais no novo padrão
- JavaScript inline com `showView()`, `pvCopyPrompt()`, `pvCopyCaption()` e `copyLegendaBtn()` antes do `</body>`
- View Prompts usa classes `.pv-*` com botões de cópia idênticos ao `media-prompts.html`

**Botão "Copiar Legenda" — view Posts (obrigatório em todos os legenda-box):**

Todo bloco `.legenda-box` da view Posts deve conter um botão "Copiar Legenda" logo após o `.hashtags`:

```html
<div class="legenda-box">
  <div class="legenda-label">Legenda</div>
  <div class="legenda-text">{legenda completa}</div>
  <div class="hashtags">{hashtags}</div>
  <button class="copy-legenda-btn" onclick="copyLegendaBtn(this)">Copiar Legenda</button>
</div>
```

CSS obrigatório:
```css
.copy-legenda-btn {
  margin-top: 12px; display: inline-block;
  background: transparent; border: 1px solid rgba(168,85,247,0.3);
  border-radius: 8px; color: #A855F7;
  font-size: 12px; font-weight: 600; padding: 6px 14px;
  cursor: pointer; transition: all 0.18s; font-family: inherit;
}
.copy-legenda-btn:hover { background: rgba(168,85,247,0.16); border-color: rgba(168,85,247,0.5); color: #C084FC; }
.copy-legenda-btn.copied { color: #86efac; background: rgba(134,239,172,0.08); border-color: rgba(134,239,172,0.3); }
```

Função JS obrigatória (inclui fallback `execCommand` para `file://`):
```javascript
function copyLegendaBtn(btn) {
  var box = btn.closest('.legenda-box');
  var texto = box.querySelector('.legenda-text').innerText.trim();
  var tags = box.querySelector('.hashtags').innerText.trim();
  navigator.clipboard.writeText(texto + '\n\n' + tags).then(function() {
    btn.textContent = 'Copiado!'; btn.classList.add('copied');
    setTimeout(function() { btn.textContent = 'Copiar Legenda'; btn.classList.remove('copied'); }, 2000);
  }).catch(function() {
    var ta = document.createElement('textarea');
    ta.value = texto + '\n\n' + tags;
    document.body.appendChild(ta); ta.select(); document.execCommand('copy'); document.body.removeChild(ta);
    btn.textContent = 'Copiado!'; btn.classList.add('copied');
    setTimeout(function() { btn.textContent = 'Copiar Legenda'; btn.classList.remove('copied'); }, 2000);
  });
}
```

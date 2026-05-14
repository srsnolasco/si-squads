# Squad Memory: YouTube → Instagram

## Estilo de Escrita

- Usuário prefere tom Provocativo Inteligente sobre Alerta e Urgência para conteúdo jurídico do STJ.
- Hook contrarian aprovado: estrutura "Você aprendeu X. O STJ discordou." funciona para a audiência.
- Hook "dado implícito" aprovado: estrutura "Quando X acontece, Y é o resultado. É assim que Z." conecta causa e efeito de forma memorável.

## Design Visual

- Seta de arraste no carrossel: formato "← ARRASTE" (seta à ESQUERDA da palavra, não à direita).
- Logo real da Sucesso Imóvel deve aparecer no header de todos os slides (usar versão branca para fundos escuros). Tamanho: 92px de altura.
- Fundo Premium Dark: `linear-gradient(155deg, #0C0018 0%, #1A0A2E 40%, #0A0A0A 100%)`.

## Template Aprovado — Post Único

Arquivo: `squads/youtube-to-instagram/_templates/single-post-template.html`
Aprovado em: 2026-05-13 (v10)

**Especificações obrigatórias:**
- Proporção: **1080×1350px** (4:5 — feed Instagram)
- Layout: fundo único (sem painéis separados) + headline à esquerda + Dr. Jeorge à direita
- Headline: `left: 80px; width: 420px` — não sobrepõe a foto (foto começa em ~500px)
- Foto Dr. Jeorge: PNG com fundo transparente, `right: 0; top: 50px; width: 580px`; com mask-image fade na base
- Card de conteúdo: `bottom: 240px; left/right: 52px` — centralizado entre headline e CTA; fundo `rgba(5,0,12,0.50)` com blur
- Body text: 38px Inter 500; badge: 26px Inter 600
- CTA bar: 200px, gradiente roxo sólido, Montserrat 900 46px, texto **sem emojis**, **sem @handle**
- Orbes atmosféricos no fundo para profundidade (opacidades 0.22, 0.18, 0.42)
- Linha decorativa vertical roxa à esquerda (accent-line)

## Template Aprovado — Post Único 2

Arquivo: `squads/youtube-to-instagram/_templates/single-post-2-template.html`
Aprovado em: 2026-05-13 (v2.3)

**Layout de zonas fixas (nunca se sobrepõem):**
- `0–560px` — AI Image hero (fade inferior de 280px)
- `0–156px` — Header (logo 112px + tag) z-index 20
- `180–460px` — Headline zone (280px, **sobre** a imagem) z-index 20
- `650–1050px` — Content card (400px, centralizado verticalmente entre imagem e CTA) z-index 30
- `1140–1350px` — CTA bar (210px, gradiente roxo)

**Tipografia:**
- Logo: `height: 112px`
- Tag (ex: "JURÍDICO / POSSE"): Inter 600, 26px
- Eyebrow (ex: "Alerta Prático"): Inter 600, 24px, letter-spacing 4px
- Headline: Montserrat 900, 70px, line-height 1.05, **centralizada**, margens 16px (larga)
- Body text: Inter 500, 39px, line-height 1.55, **máx 4 linhas** (`-webkit-line-clamp: 4`)
- Badge: Inter 600, 28px
- CTA: Montserrat 900, 48px, centralizado

**Regras obrigatórias:**
- Headline **totalmente sobre a imagem** (zone 180–460px)
- Card **não começa antes de 580px** (abaixo da imagem)
- Card com `justify-content: center` — conteúdo centralizado verticalmente
- Logo branco (`SI-Logo-Branco-Transp.png`) — fundo sempre escuro neste post
- CTA **sempre** pedido de like
- Imagem IA: sem texto, sem palavras, sem letras — acrescentar ao prompt: `absolutely no text, no words, no letters, no signs, no stamps anywhere in the image — purely visual, zero typography`

## Template Aprovado — Post Único 3

Arquivo: `squads/youtube-to-instagram/_templates/single-post-3-template.html`
Aprovado em: 2026-05-13 (v2.1)

**Layout de zonas fixas (nunca se sobrepõem):**
- `0–156px` — Header: logo colorido **centralizado** + tag absoluta no canto superior direito
- `168–490px` — Headline zone (322px: eyebrow + divider + headline, left-aligned)
- `510–720px` — Quote box (210px: sub-headline de destaque, `align-items: center`)
- `740–1130px` — Content card (390px, `justify-content: center`)
- `1140–1350px` — CTA bar (210px, 2 linhas)

**Tipografia (alinhada ao Post 2):**
- Logo: `height: 112px`, **centralizado** horizontalmente
- Tag: Inter 600, 26px, posição `absolute; top: 54px; right: 56px`
- Eyebrow: Inter 600, 24px, letter-spacing 4px
- Headline: Montserrat 900, 70px, line-height 1.05, left-aligned, clamp 3 linhas
- Quote text: Montserrat 900, 44px, line-height 1.15
- Body text: Inter 500, 39px, line-height 1.55, máx 4 linhas
- Badge: Inter 600, 28px
- CTA label (fixo): Inter 600, 26px, `"Siga nosso perfil:"`
- CTA main (placeholder): Montserrat 900, 48px

**Regras obrigatórias:**
- Paleta CLARO: fundo `linear-gradient(155deg, #FAFAFA, #F3EEFF, #F8F5FF)`
- Logo **COLORIDO** (`SI-Logo-Color-Transp.png`) — nunca branco neste post
- Logo **centralizado** no header; tag posicionada absolutamente no canto direito
- CTA sempre começa com `"Siga nosso perfil:"` fixo no HTML, seguido de `{{CTA_TEXT}}`
- `{{CTA_TEXT}}` deve ser curto: handle `@sucessoimovel` ou frase de 1-3 palavras
- Layout 100% tipográfico — sem foto, sem imagem IA
- Linha decorativa vertical roxa à esquerda (`accent-line`) começa em `top: 248px`

## Template Aprovado — Carrossel Premium Dark

Arquivo de referência: `squads/youtube-to-instagram/pipeline/data/template-reference.html`
Aprovado em: 2026-05-13 (versão final)

**Layout geral:**
- Dimensões: 1080×1440px
- Fundo: `linear-gradient(155deg, #0C0018 0%, #1A0A2E 40%, #0A0A0A 100%)`
- Accent line topo: `height:3px; background:linear-gradient(90deg,transparent,#7B2FBE,#A855F7,transparent)`

**Header (todos os slides):**
- Logo branco (`SI-Logo-Branco-Transp.png`) base64, `height:112px`, header `justify-content:center`
- Tag: `position:absolute; top:44px; right:72px; border-radius:100px; font-size:26px; font-weight:600; color:#A855F7; padding:13px 30px`

**Conteúdo (top:220px em todos os slides):**
- Eyebrow: `font-size:30px; font-weight:700; color:#A855F7; letter-spacing:3px; text-transform:uppercase`
- Divider: `width:56px; height:4px; background:linear-gradient(90deg,#7B2FBE,#A855F7); border-radius:2px; margin-bottom:28px`
- Headline capa: Montserrat 900, 68px, `color:#fff`, accent `color:#A855F7`
- Headline slides conteúdo: Montserrat 900, 64px
- Card body: `background:rgba(255,255,255,0.04); border:1px solid rgba(123,47,190,0.30); border-radius:16px; padding:36px 44px; font-size:34px; font-weight:500; color:rgba(255,255,255,0.85); line-height:1.55`

**Botão ARRASTE (slides 1 a N-1, exceto último):**
- Texto: `← ARRASTE` (seta à ESQUERDA — NUNCA à direita)
- `color:rgba(255,255,255,0.90); background:rgba(255,255,255,0.08); border:2px solid rgba(255,255,255,0.30); border-radius:12px; padding:16px 36px; font-size:36px; font-weight:700`
- **border-radius:12px** (levemente arredondado — 100px "pílula" é PROIBIDO)

**Slide CTA — último slide (sem botão ARRASTE):**
- NUNCA usar fórmula genérica "salva e compartilha"
- Sempre dois argumentos persuasivos específicos ao tema:
  1. Por que **salvar**: utilidade futura ("você vai lembrar disso antes do próximo fechamento")
  2. Por que **compartilhar**: alguém que o leitor conhece precisa ("manda para um colega que fechou sem verificar X")
- Bloco CTA: `background:linear-gradient(135deg,#3B0764,#6B21A8); border-radius:16px; padding:36px 44px`
- Texto CTA: Montserrat 900, 38px, `color:#fff`; detalhe complementar em `color:#DDD6FE`
- Exemplo aprovado: *"Salva esse carrossel — você vai lembrar dele antes do próximo fechamento. E manda para um colega que fechou negócio sem verificar a situação de posse."*

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
- Nunca usar seta à direita da palavra no botão de arraste do carrossel ("Arraste →" é proibido — usar "← Arraste").

## Técnico (específico do squad)

- Nome da pasta de output: `YYYY-MM-DD-HHmmss-tema-slug` (data + hora + 1 a 3 palavras do tema em kebab-case).
- Estrutura de subpastas obrigatória: `Posts/` para imagens, PNGs **e** `post-content.md`; `Roteiros/` para scripts de vídeo.
- Logo embedado como base64 data URI — nunca como path relativo (o HTTP server serve só da pasta de slides).

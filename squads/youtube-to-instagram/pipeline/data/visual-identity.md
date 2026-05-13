# Visual Identity — Sucesso Imóvel

Template aprovado: **Template C — Premium Dark**

## Color Palette

- **Primary:** #7B2FBE — roxo principal; usado em bordas de cards, ícone da marca, glow superior
- **Secondary:** #A855F7 — roxo médio; usado em texto de destaque, eyebrow, tag label, footer swipe, glow inferior
- **Accent:** #D4A0FF — roxo claro; usado em gradient text de valores em destaque e segunda métrica
- **Background:** `linear-gradient(160deg, #0A0012 0%, #1A0A2E 45%, #0D0D0D 100%)` — fundo gradiente roxo-preto escuro
- **Text Primary:** #FFFFFF — texto principal, títulos, valores de destaque
- **Text Secondary:** #9B9B9B — subtítulos, labels de cards, texto de apoio
- **Text Muted:** #6B6B6B — handle @, rodapé, valores menos prioritários
- **Card Background:** rgba(255,255,255,0.04) — cards semitransparentes sobre fundo escuro
- **Card Highlighted:** rgba(123, 47, 190, 0.12) — card de destaque com leve roxo

## Typography

- **Headings (título principal):** Montserrat, weight 900, 60px mínimo para Instagram carousel
- **Body / Subtítulo:** Inter, weight 500, 34px mínimo para Instagram carousel
- **Eyebrow / Tags:** Inter, weight 700, 24px, UPPERCASE, letter-spacing 2-3px
- **Badge / Handle / Footer:** Inter, weight 700/500, 24-28px
- **Valores de Métrica:** Montserrat, weight 800, 44px
- **Mínimos absolutos:** Hero 60px, Heading 43px, Body 34px, Caption 24px (Instagram carousel 1080x1440)

## Layout

- **Viewport:** 1080 x 1440 px (Instagram Carousel 3:4 portrait)
- **Padding:** 72px em todos os lados
- **Estrutura:** Flexbox coluna — Header → Title Area → Cards → Footer
- **Z-index:** Conteúdo em z-index: 1; efeitos decorativos em posição absoluta sem z-index

## Composition Rules

- **Header:** Sempre presente. Badge "SI" roxo à esquerda + nome da marca. Tag de categoria à direita com borda roxa.
- **Accent line:** Linha fina de 3px no topo, gradiente de transparente para roxo e volta a transparente.
- **Glow effects:** Radial gradient roxo no canto superior direito (#7B2FBE44) e inferior esquerdo (#A855F722). Decorativos, pointer-events: none.
- **Eyebrow:** Texto pequeno em roxo, uppercase, acima do título. Define o tema/categoria do slide.
- **Título principal:** Montserrat 900, branco. Palavras-chave em gradient roxo (#A855F7 → #D4A0FF) via -webkit-background-clip.
- **Cards:** Fundo semitransparente com borda roxa. Card 1 com borda mais intensa (rgba 0.5). Card 3 com background roxo levemente opaco.
- **Footer:** Linha separadora sutil (rgba branco 0.08). Dot circular gradiente roxo + handle @sucessoimovel à esquerda. "ARRASTE →" em roxo à direita.

## Adaptation Rules

- **Slides de conteúdo (carrossel):** Substituir os metric cards por blocos de texto com headline + supporting text. Manter header, eyebrow, título e footer.
- **Slide de capa (cover):** Título maior (68-72px), sem cards. Subtitle mais curto. Tag à direita pode mudar conforme o tema.
- **Slide CTA:** Footer expandido com CTA em destaque. Cards substituídos por uma única caixa de chamada em roxo.
- **Post único:** Mesma estrutura, conteúdo condensado em um único slide.
- **Cores primárias sempre presentes:** Toda imagem deve ter pelo menos roxo (#7B2FBE ou #A855F7) e branco (#FFFFFF) visíveis.
- **Outras cores aceitas como acento:** Desde que roxo, preto, cinza e branco sejam as cores dominantes.
- **Nunca usar:** Fundo branco ou claro como principal neste template. Manter sempre o gradiente escuro como base.

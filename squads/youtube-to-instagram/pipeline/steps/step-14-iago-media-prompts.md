---
type: agent
agent: iago-instagram
execution: inline
inputFile: squads/youtube-to-instagram/output/{run-id}/Posts/post-content.md
outputFile: squads/youtube-to-instagram/output/{run-id}/Prompts/media-prompts.md, squads/youtube-to-instagram/output/{run-id}/Prompts/media-prompts.html
---

# Step 14: Iago Instagram — Geração de Prompts Imagen (nano-banana)

Iago cria **3 prompts para geração de posts completos no Google Imagen (nano-banana)**.

> **Nota:** estes prompts (`media-prompts.md`) são diferentes do `ai-image-prompt-post2.md` criado no step 11. Aquele gera apenas a imagem de fundo do Qua-PU2 para Diego usar no design. Estes geram posts Instagram inteiros com headline e sub-headline escritas na imagem.

Cada prompt gera uma imagem de Instagram pronta — com design, **texto em português legível** (headline + sub-headline) e identidade visual da Sucesso Imóvel embutidos na própria imagem. O texto precisa APARECER e COMUNICAR — não é apenas background visual.

## Context Loading

Antes de iniciar, Iago deve carregar:
- `squads/youtube-to-instagram/output/{run-id}/Posts/post-content.md` — Conteúdo dos posts criados
- `squads/youtube-to-instagram/output/{run-id}/v1/doc-source-analysis.md` — Análise do vídeo original
- `squads/youtube-to-instagram/_memory/memories.md` — Estilo visual aprovado
- `_opensquad/_memory/company.md` — Perfil da Sucesso Imóvel

## Identidade Visual da Sucesso Imóvel — Imagens IA

Os prompts devem instruir o Imagen a gerar imagens com **estética de consultoria jurídica premium**: séria, conservadora, autoritária. Sem elementos futuristas, neon, sci-fi ou tech.

**Paleta de cores:**
- Fundo: carvão profundo neutro (`#0D0D0F` → `#141418` → `#0A0A0C`) — gradiente sutil, sem roxo saturado
- Accent: roxo primário mudo (`#7B2FBE`) — profundo, elegante, não elétrico
- Texto principal: branco puro (`#FFFFFF`)
- Texto secundário: branco suave (`rgba(255,255,255,0.82)`)

**Tipografia:**
- Headline: fonte bold/black sem-serifa estilo Montserrat, peso 900, letras levemente condensadas, tamanho grande
- Sub-headline: fonte sem-serifa limpa estilo Inter, peso 500, tamanho médio, cor branco suave

**Elementos visuais de fundo (conservadores):**
- Texturas sutis de fundo: mármore escuro, papel envelhecido, madeira nobre, pedra arquitetônica — renderizadas em baixíssima opacidade como watermark
- Elementos iconográficos opcionais: linhas arquitetônicas geométricas, livros de direito em silhueta, balança da justiça em outline muito sutil
- Linha fina vertical à esquerda (accent line) em roxo mudo `#7B2FBE`, sem glow/brilho
- Iluminação: luz direcional discreta e quente (como luminária de escritório ou câmara judicial), sem neon

**Proibições de estilo:**
- **PROIBIDO:** orbes brilhantes/neon, gradientes elétricos violeta, efeitos sci-fi, estética futurista ou tech
- **PROIBIDO:** "glowing", "vivid neon", "electric", "cinematic orbs", "atmospheric glow", "diffused neon light"
- **PROIBIDO:** qualquer elemento que remeta a tecnologia, startup, metaverso ou ciberespaço

**Regras absolutas:**
- **SEM logo** — nenhuma marca, símbolo, ícone de empresa ou logotipo em nenhuma área da imagem
- **Somente dois textos:** headline principal + sub-headline de apoio — todos os demais elementos (badge, tag, card, botão) são proibidos
- O texto **DEVE aparecer na imagem** — é a razão de existir do post. Headline e sub-headline são parte obrigatória do prompt
- Headline: fonte bold/black estilo Montserrat 900, tamanho grande, branca com **uma palavra ou trecho em roxo mudo (#7B2FBE)**
- Sub-headline: fonte leve estilo Inter 500, tamanho médio, branco suave (rgba(255,255,255,0.82))
- Posicionamento do texto: zona central da imagem, legível, com contraste claro contra o fundo escuro

**Formato:** 1080×1350px (proporção 4:5 — feed Instagram)

---

## Instructions

Com base no conteúdo dos posts já criados, gerar 3 prompts — um por post, derivado diretamente do conteúdo e ângulo editorial de cada post correspondente.

Cada prompt descreve um **post completo do Instagram** com:
1. O **layout e design** seguindo a identidade visual da Sucesso Imóvel
2. A **headline em português** — extraída ou adaptada da headline do post correspondente — deve ser escrita LITERALMENTE no prompt para que o Imagen a renderize na imagem. Uma palavra ou trecho chave deve estar em roxo (#A855F7)
3. A **sub-headline em português** — adaptada do body text do post correspondente (1 linha, sem repetir a headline) — também escrita LITERALMENTE no prompt
4. Um **elemento visual de fundo** (composição abstrata, textura, gradiente ou fotografia desfocada) que reforce o tema do post sem competir com o texto

### Estrutura obrigatória do prompt em inglês

O prompt deve conter obrigatoriamente estas seções, nesta ordem:

```
[Dimensão e descrição do formato]
[Descrição do background: gradiente carvão neutro + textura conservadora temática (mármore, papel, pedra, madeira, silhueta arquitetônica)]
[Accent line vertical à esquerda em roxo primário mudo #7B2FBE — fina, sem glow]
[Bloco de tipografia — com as frases exatas em português]:
  - Headline: "[FRASE EXATA EM PORTUGUÊS]" — Montserrat-style, 900 weight, white, large — the word/phrase "[PALAVRA CHAVE]" in deep muted purple #7B2FBE
  - Sub-headline below: "[FRASE EXATA EM PORTUGUÊS]" — Inter-style, 500 weight, soft white rgba(255,255,255,0.82), medium size
[Regra de composição: texto centralizado/alinhado, legível, alto contraste]
[Proibições: SEM logo, SEM badge, SEM tag, SEM ícones, SEM orbes neon, SEM efeitos elétricos/futuristas — apenas headline e sub-headline]
[Mood obrigatório: "premium legal editorial", "prestigious law firm", "authoritative", "classical" — NÃO usar: "cinematic", "neon", "electric", "futuristic", "sci-fi", "glowing orbs"]
```

### Os 3 prompts obrigatórios (cada um derivado do post correspondente):

1. **01-Ter-PU1** — derivado do post `Ter-PU1` do `post-content.md` (ângulo: tema central do vídeo)
2. **02-Qua-PU2** — derivado do post `Qua-PU2` do `post-content.md` (ângulo: impacto/consequência)
3. **03-Qui-PU3** — derivado do post `Qui-PU3` do `post-content.md` (ângulo: reflexão/princípio)

### CTA fixo para os 3 posts

A legenda de **todos** os posts gerados neste step deve encerrar com este CTA fixo, sem alterações:

> Gostou do conteúdo? Deixe o seu like! É rapidinho e ajuda muito a gente na criação de mais conteúdo.

---

## Output Format

Salvar **dois arquivos** em `output/{run-id}/Prompts/`:

### 1. `media-prompts.md`

```markdown
# Prompts Imagen — {Tema}

Data: {YYYY-MM-DD}
Tema central: {tema extraído do post-content.md}
Ferramenta: Google Imagen via nano-banana
Formato alvo: 1080×1350px (feed Instagram 4:5)

---

### 01-Ter-PU1
**Post de origem:** Ter-PU1 — {título do post}
**Ângulo:** {ângulo editorial do Ter-PU1}
**Headline:** {headline em português derivada do Ter-PU1}
**Sub-headline:** {sub-headline em português derivada do body text do Ter-PU1}
**Prompt:**
{prompt em inglês — deve conter: background visual temático + accent line roxa + headline em português com palavra-chave em roxo + sub-headline em português + regras de legibilidade + proibição de logo/badge/tag}

**Legenda:**
{legenda do Ter-PU1 copiada do post-content.md}

**Hashtags:**
{hashtags do Ter-PU1}

---

### 02-Qua-PU2
**Post de origem:** Qua-PU2 — {título do post}
**Ângulo:** {ângulo editorial do Qua-PU2}
**Headline:** {headline em português derivada do Qua-PU2}
**Sub-headline:** {sub-headline em português derivada do body text do Qua-PU2}
**Prompt:**
{prompt em inglês — deve conter: background visual temático + accent line roxa + headline em português com palavra-chave em roxo + sub-headline em português + regras de legibilidade + proibição de logo/badge/tag}

**Legenda:**
{legenda do Qua-PU2 copiada do post-content.md}

**Hashtags:**
{hashtags do Qua-PU2}

---

### 03-Qui-PU3
**Post de origem:** Qui-PU3 — {título do post}
**Ângulo:** {ângulo editorial do Qui-PU3}
**Headline:** {headline em português derivada do Qui-PU3}
**Sub-headline:** {sub-headline em português derivada do body text do Qui-PU3}
**Prompt:**
{prompt em inglês — deve conter: background visual temático + accent line roxa + headline em português com palavra-chave em roxo + sub-headline em português + regras de legibilidade + proibição de logo/badge/tag}

**Legenda:**
{legenda do Qui-PU3 copiada do post-content.md}

**Hashtags:**
{hashtags do Qui-PU3}
```

### 2. `media-prompts.html`

Após salvar o Markdown, gerar um arquivo HTML auto-suficiente que apresenta os 3 prompts de forma organizada e visualmente rica. Design Premium Dark da Sucesso Imóvel.

**Estrutura do HTML:**
- Header com título "Prompts Imagen — {Tema}" e data
- Um card por prompt com: badge do ângulo (Alerta / Dado / Reflexão), headline, sub-headline, bloco de prompt em inglês (monospace, fundo escuro), **botão "Copiar prompt"** logo abaixo do bloco de prompt, legenda completa e hashtags
- Botão de cópia: ao clicar, copia o texto do prompt para a área de transferência e exibe "Copiado!" por 2 segundos com ícone de check verde, depois volta ao estado original
- Totalmente auto-suficiente: CSS inline + Google Fonts (Montserrat + Inter) + JavaScript inline apenas

Salvar em `output/{run-id}/Prompts/media-prompts.html`.

## Quality Criteria

- [ ] 3 prompts gerados: 01-Ter-PU1, 02-Qua-PU2 e 03-Qui-PU3
- [ ] Cada prompt é derivado do post correspondente (headline e body do post-content.md)
- [ ] Cada prompt contém a **headline exata em português** escrita literalmente dentro do prompt em inglês (para que o Imagen renderize o texto na imagem)
- [ ] Cada prompt contém a **sub-headline exata em português** escrita literalmente dentro do prompt em inglês
- [ ] A headline especifica que uma palavra ou trecho deve estar em roxo primário mudo #7B2FBE (não elétrico/neon)
- [ ] Nenhum prompt menciona logo, marca ou logotipo
- [ ] Apenas headline e sub-headline como texto na imagem — badge, tag, card e botão são proibidos
- [ ] Layout segue identidade visual da Sucesso Imóvel (dark background, roxo accent, sem logo)
- [ ] Legenda e hashtags incluídas para cada post, copiadas do post-content.md
- [ ] CTA de todos os posts encerra com o texto fixo: "Gostou do conteúdo? Deixe o seu like! É rapidinho e ajuda muito a gente na criação de mais conteúdo."
- [ ] Hashtags são exatamente as 6 oficiais — sem adições ou substituições
- [ ] `media-prompts.md` salvo em `output/{run-id}/Prompts/`
- [ ] `media-prompts.html` salvo em `output/{run-id}/Prompts/` — auto-suficiente, design Premium Dark

## Veto Conditions

1. Qualquer menção a logo, ícone de marca ou símbolo da empresa no prompt
2. Mais de dois elementos de texto na imagem (badge, tag, card, botão, etc.)
3. Prompts que dizem "no text", "no words", "no letters", "purely visual", "zero typography" — o texto É o produto, não pode ser proibido
4. Headline ou sub-headline em português AUSENTE do corpo do prompt em inglês (o texto deve estar escrito literalmente para que o Imagen o renderize)
5. Prompts não derivados dos posts correspondentes (Ter-PU1, Qua-PU2, Qui-PU3)
6. Dois prompts com a mesma headline
7. Sub-headline que repete a ideia da headline sem acrescentar informação
8. Legenda ou hashtags ausentes em qualquer dos 3 posts
9. Hashtags diferentes das 6 oficiais
10. `media-prompts.md` salvo fora da pasta `Prompts/`
11. `media-prompts.html` não gerado
12. Prompts com estilo futurista/neon: "glowing orbs", "electric purple", "neon", "sci-fi", "cinematic orbs", "atmospheric glow", "vivid neon", "futuristic" — a Sucesso Imóvel é consultoria jurídica, não empresa de tecnologia

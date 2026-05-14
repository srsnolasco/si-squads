---
type: agent
agent: iago-instagram
execution: inline
inputFile: squads/youtube-to-instagram/output/approved-ideas.md
outputFile: squads/youtube-to-instagram/output/Posts/post-content.md
---

# Step 04: Iago Instagram — Criação do Conteúdo

Iago Instagram transforma as ideias aprovadas em conteúdo completo para **4 posts**: 3 posts únicos e 1 carrossel.

## Context Loading

Antes de iniciar, Iago deve carregar:
- `squads/youtube-to-instagram/output/approved-ideas.md` — Ideias aprovadas pelo usuário
- `squads/youtube-to-instagram/output/youtube-analysis.md` — Análise completa do vídeo
- `squads/youtube-to-instagram/pipeline/data/tone-of-voice.md` — Guia de tons de voz
- `squads/youtube-to-instagram/pipeline/data/quality-criteria.md` — Critérios de qualidade
- `squads/youtube-to-instagram/pipeline/data/output-examples.md` — Exemplos de posts
- `_opensquad/_memory/company.md` — Perfil da Sucesso Imóvel
- `squads/youtube-to-instagram/_memory/memories.md` — Preferências e templates aprovados

## Estrutura de Output Obrigatória

O squad produz **4 posts** a cada run:

| Post | Tipo | Ângulo | CTA | Layout |
|------|------|--------|-----|--------|
| Post Único 1 | Post único + foto Dr. Jeorge | Principal — tema central do vídeo | Comentar | Roxo/Preto (template v10) |
| Post Único 2 | Post único + imagem IA | Impacto/consequência — o "e agora?" | Deixar like | Azul/Ciano (template 2) |
| Post Único 3 | Post único — só texto | Reflexão/princípio — o "por que isso importa" | Seguir no Instagram | Esmeralda/Dourado (template 3) |
| Carrossel | Carrossel N slides | Tutorial/aprofundamento — o "como funciona" | Comentar palavra-chave | Premium Dark roxo |

**Cada post DEVE abordar o tema por um ângulo diferente.** Os três posts únicos são publicados em dias diferentes e juntos contam a história completa do tema.

## Instructions

### Para cada post (seguir esta ordem: PU1 → PU2 → PU3 → Carrossel):

1. **Recomendar o tom de voz** com base no ângulo editorial. Apresentar ao usuário e aguardar confirmação.

2. **Propor 3 opções de hook** (primeira linha da legenda, máx. 125 chars). Aguardar o usuário escolher.

3. **Criar o conteúdo completo:**

---

#### Post Único 1 — Com foto Dr. Jeorge | Ângulo: Principal

- **Headline principal:** texto com `<span class="accent">` nas palavras-chave
- **Body text:** dado ou insight central do tema (50-80 palavras)
- **Badge text:** data ou referência da decisão/lei
- **CTA text:** chamada para comentar (sem emojis, sem @handle)
- **Legenda:** hook + corpo + chamada para comentar + hashtags
- **Template:** `_templates/single-post-template.html`
- **Eyebrow:** categoria do conteúdo (ex: "Novidade Jurídica")
- **Tag:** área + tema (ex: "JURÍDICO / STJ")
- **Foto Dr. Jeorge:** indicar qual foto usar de `assets/imagens/jeorge/` (preferir PNG com `-Transp` no nome)

#### Post Único 2 — Com imagem IA | Ângulo: Impacto/Consequência

- **Headline principal:** pergunta ou consequência prática
- **Body text:** impacto real no dia-a-dia do corretor (50-80 palavras)
- **Badge text:** dado ou estatística do tema
- **CTA text:** pedido de like (ex: "Gostou? Deixe um like")
- **Legenda:** hook + corpo + pedido de like + hashtags
- **Template:** `_templates/single-post-2-template.html`
- **Eyebrow:** (ex: "Impacto Prático")
- **Tag:** área + tema
- **Prompt para imagem IA:** criar um prompt em inglês para gerar a imagem via nano banana / DALL-E. O prompt deve descrever uma cena visual abstrata ou metáfora visual que represente o tema (ex: para STJ Tema 1.266 — "a padlock overlapping a real estate building, dark cinematic lighting, professional photography, abstract concept of legal protection"). **OBRIGATÓRIO: finalizar SEMPRE com** `absolutely no text, no words, no letters, no signs, no stamps, no labels anywhere in the image — purely visual, zero typography`. Salvar o prompt em `output/ai-image-prompt-post2.md`.

#### Post Único 3 — Só texto | Ângulo: Reflexão/Princípio

- **Headline principal:** afirmação forte ou dado surpreendente
- **Quote text:** frase curta e impactante (1-2 frases — este é o elemento visual central) — suporta `<span class="accent">` e `<span class="accent-gold">`
- **Body text:** contexto e implicação para o corretor (40-60 palavras)
- **Badge text:** referência ao tema
- **CTA text:** pedido para seguir no Instagram (ex: "Siga para mais conteúdo jurídico")
- **Legenda:** hook + corpo + pedido para seguir + hashtags
- **Template:** `_templates/single-post-3-template.html`
- **Eyebrow:** (ex: "Para Reflexão")
- **Tag:** área + tema

#### Carrossel — Tutorial/Aprofundamento

- **Slide 1 (Capa):** headline + subtítulo opcional
- **Slides 2 a N-1 (Conteúdo):** headline + supporting text (40-80 palavras por slide)
- **Último slide (CTA):** frase de CTA + pergunta de engajamento
- **Template:** Template C Premium Dark (arquivo `pipeline/data/template-reference.html`)
- **Seta:** usar "← ARRASTE" no slide de capa (seta à ESQUERDA da palavra)

---

## Output Format

Salvar em `output/Posts/post-content.md`:

```markdown
# Post Content — {título geral da série}

Data: {YYYY-MM-DD}

---

## POST ÚNICO 1 — {título}
**Template:** single-post-template.html
**Foto Dr. Jeorge:** {nome do arquivo}
**Tag:** {texto}
**Eyebrow:** {texto}
**Headline:** {HTML com <br> e <span class="accent">}
**Body text:** {HTML com <span class="accent">}
**Badge text:** {texto}
**CTA text:** {texto}
**Tom de voz:** {tom escolhido}

### Legenda
{hook}
{corpo}
{CTA}

### Hashtags
{hashtags}

---

## POST ÚNICO 2 — {título}
**Template:** single-post-2-template.html
**Tag:** {texto}
**Eyebrow:** {texto}
**Headline:** {HTML}
**Body text:** {HTML}
**Badge text:** {texto}
**CTA text:** {deve ser pedido de like}
**Prompt IA (nano banana):** ver output/ai-image-prompt-post2.md
**Tom de voz:** {tom escolhido}

### Legenda
{hook}
{corpo}
{CTA — pedido de like}

### Hashtags
{hashtags}

---

## POST ÚNICO 3 — {título}
**Template:** single-post-3-template.html
**Tag:** {texto}
**Eyebrow:** {texto}
**Headline:** {HTML}
**Quote text:** {frase impactante curta — HTML com accent classes}
**Body text:** {HTML}
**Badge text:** {texto}
**CTA text:** {deve ser pedido para seguir}
**Tom de voz:** {tom escolhido}

### Legenda
{hook}
{corpo}
{CTA — pedido para seguir}

### Hashtags
{hashtags}

---

## CARROSSEL — {título}

### Slides
[...estrutura de slides...]

### Legenda
[...]

### Hashtags
[...]
```

## Quality Criteria

- [ ] 4 posts com ângulos DISTINTOS — nenhum repete o mesmo ponto de vista
- [ ] Post Único 1: CTA é pedido para comentar (sem emoji, sem @handle na barra)
- [ ] Post Único 2: CTA é pedido de like
- [ ] Post Único 3: CTA é pedido para seguir no Instagram
- [ ] Post Único 2: prompt para imagem IA salvo em `output/ai-image-prompt-post2.md`
- [ ] Quote text do Post 3 é impactante e curto (máx. 2 frases)
- [ ] Todos os hooks têm no máximo 125 caracteres
- [ ] Todo conteúdo rastreável à análise do vídeo em `youtube-analysis.md`
- [ ] `output/Posts/post-content.md` salvo antes de encerrar
- [ ] **ZERO emojis** em qualquer campo de qualquer post — headline, body, badge, CTA, legenda, hashtags

## Veto Conditions

1. Dois posts com o mesmo ângulo ou ponto de vista
2. CTA do Post 2 não pede like
3. CTA do Post 3 não pede para seguir
4. Algum dado não rastreável ao vídeo analisado
5. Hook ultrapassa 125 caracteres
6. **Qualquer emoji encontrado em qualquer campo de qualquer post**

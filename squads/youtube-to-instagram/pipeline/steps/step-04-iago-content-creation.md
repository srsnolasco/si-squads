---
type: agent
agent: iago-instagram
execution: inline
inputFile: squads/youtube-to-instagram/output/approved-ideas.md
outputFile: squads/youtube-to-instagram/output/Posts/post-content.md
---

# Step 04: Iago Instagram — Criação do Conteúdo

Iago Instagram transforma as ideias aprovadas em conteúdo completo para **5 posts**: 3 posts únicos, 1 Seg-CT e 1 Sex-CCTA.

## Context Loading

Antes de iniciar, Iago deve carregar:
- `squads/youtube-to-instagram/output/{run-id}/approved-ideas.md` — Ideias aprovadas pelo usuário
- `squads/youtube-to-instagram/output/{run-id}/selected-jeorge-photo.md` — Foto do Dr. Jeorge selecionada no step 10 (**usar exatamente este arquivo no Ter-PU1**)
- `squads/youtube-to-instagram/output/{run-id}/v1/youtube-analysis.md` — Análise completa do vídeo
- `squads/youtube-to-instagram/output/{run-id}/lead-magnet-ideas.md` — Isca digital aprovada (**obrigatório para o Sex-CCTA — extrair título, descrição e palavra do CTA**)
- `squads/youtube-to-instagram/pipeline/data/tone-of-voice.md` — Guia de tons de voz
- `squads/youtube-to-instagram/pipeline/data/quality-criteria.md` — Critérios de qualidade
- `squads/youtube-to-instagram/pipeline/data/output-examples.md` — Exemplos de posts
- `squads/youtube-to-instagram/pipeline/data/hashtags.md` — Lista oficial de hashtags (**obrigatório carregar antes de escrever qualquer post**)
- `_opensquad/_memory/company.md` — Perfil da Sucesso Imóvel
- `squads/youtube-to-instagram/_memory/memories.md` — Preferências e templates aprovados

## Estrutura de Output Obrigatória

O squad produz **5 posts** a cada run:

| Post | Tipo | Ângulo | CTA | Layout |
|------|------|--------|-----|--------|
| Ter-PU1 | Post único + foto Dr. Jeorge | Principal — tema central do vídeo | Comentar | Roxo/Preto (template v10) |
| Qua-PU2 | Post único + imagem IA | Impacto/consequência — o "e agora?" | Deixar like | Azul/Ciano (template 2) |
| Qui-PU3 | Post único — só texto | Reflexão/princípio — o "por que isso importa" | Seguir no Instagram | Esmeralda/Dourado (template 3) |
| Seg-CT | Carrossel Tutorial — N slides | Tutorial/aprofundamento — o "como funciona" | Salvar o post | Premium Dark roxo |
| Sex-CCTA | Carrossel — N slides | Isca digital — incentivar download do material | Comentar [PALAVRA] | Premium Dark roxo |

**Cada post DEVE abordar o tema por um ângulo diferente.** Os três posts únicos são publicados em dias diferentes e juntos contam a história completa do tema.

## Instructions

### Para cada post (seguir esta ordem: Seg-CT → Ter-PU1 → Qua-PU2 → Qui-PU3 → Sex-CCTA):

1. **Recomendar o tom de voz** com base no ângulo editorial. Apresentar ao usuário e aguardar confirmação.

2. **Propor 3 opções de hook** (primeira linha da legenda, máx. 125 chars). Aguardar o usuário escolher.

3. **Criar o conteúdo completo:**

---

#### Ter-PU1 — Com foto Dr. Jeorge | Ângulo: Principal

- **Headline principal:** texto com `<span class="accent">` nas palavras-chave
- **Body text:** dado ou insight central do tema (50-80 palavras)
- **Badge text:** data ou referência da decisão/lei
- **CTA text:** pergunta genuína relacionada ao tema do post + convite para responder nos comentários. Estrutura obrigatória: [pergunta sobre o tema] + [direcionamento para os comentários]. A pergunta deve ser relevante ao dia a dia do corretor. O direcionamento deve ser natural — nunca pedir uma palavra-chave específica. Exemplos válidos: "Você já passou por um problema como este? Conta aqui nos comentários." / "Isso já aconteceu com algum cliente seu? Me conta nos comentários." / "Como você lida com isso nos fechamentos? Compartilha aqui embaixo." Exemplos proibidos: "Comenta CONTRATO" / "Deixa um comentário" / "Responde aqui" (sem pergunta antes).
- **Legenda:** hook + corpo + CTA (mesma estrutura: pergunta genuína + direcionamento para comentários, sem palavra-chave) + hashtags
- **Template:** `_templates/single-post-template.html`
- **Eyebrow:** categoria do conteúdo (ex: "Novidade Jurídica")
- **Tag:** área + tema (ex: "JURÍDICO / STJ")
- **Foto Dr. Jeorge:** indicar qual foto usar de `assets/imagens/jeorge/` (preferir PNG com `-Transp` no nome)

#### Qua-PU2 — Com imagem IA | Ângulo: Impacto/Consequência

- **Headline principal:** pergunta ou consequência prática
- **Body text:** impacto real no dia-a-dia do corretor — **máximo 120 caracteres** (incluindo espaços). O template Qua-PU2 renderiza o body text em fonte 39px com limite rígido de 4 linhas: texto mais longo é cortado com "..." e o seguidor não lê a frase completa. Escrever uma frase única, completa e impactante que caiba nesse limite. Contar os caracteres antes de finalizar.
- **Badge text:** dado ou estatística do tema
- **CTA text:** pedido de like (ex: "Gostou? Deixe um like")
- **Legenda:** hook + corpo + pedido de like + hashtags
- **Template:** `_templates/single-post-2-template.html`
- **Eyebrow:** (ex: "Impacto Prático")
- **Tag:** área + tema
- **Prompt para imagem IA:** criar um prompt em inglês para gerar a imagem via nano banana / DALL-E. O prompt deve descrever uma cena visual abstrata ou metáfora visual que represente o tema (ex: para STJ Tema 1.266 — "a padlock overlapping a real estate building, dark cinematic lighting, professional photography, abstract concept of legal protection"). **OBRIGATÓRIO: finalizar SEMPRE com** `absolutely no text, no words, no letters, no signs, no stamps, no labels anywhere in the image — purely visual, zero typography`. Salvar o prompt em `output/ai-image-prompt-post2.md`.

#### Qui-PU3 — Só texto | Ângulo: Reflexão/Princípio

- **Headline principal:** afirmação forte ou dado surpreendente
- **Quote text:** frase curta e impactante (1-2 frases — este é o elemento visual central) — suporta `<span class="accent">` e `<span class="accent-gold">`
- **Body text:** contexto e implicação para o corretor — **máximo 120 caracteres** (incluindo espaços). O template Qui-PU3 tem o mesmo limite rígido de 4 linhas a 39px que o Qua-PU2: texto mais longo é cortado com "...". Escrever uma frase única, completa e impactante. Contar os caracteres antes de finalizar.
- **Badge text:** referência ao tema
- **CTA text:** pedido para seguir o perfil da **Sucesso Imóvel** — deve mencionar o nome da marca e conectar o convite ao valor que o conteúdo entregou. Exemplos válidos: "Siga a Sucesso Imóvel para receber mais conteúdo jurídico como esse." / "Se esse conteúdo lhe ajudou, siga a Sucesso Imóvel para receber mais novidades!" Nunca usar um pedido genérico sem mencionar a marca (ex: "Siga para mais conteúdo" é proibido).
- **Legenda:** hook + corpo + CTA (pedido para seguir a Sucesso Imóvel, com menção ao nome da marca) + hashtags
- **Template:** `_templates/single-post-3-template.html`
- **Eyebrow:** (ex: "Para Reflexão")
- **Tag:** área + tema

#### Seg-CT — Carrossel Tutorial / Aprofundamento

- **Número de slides:** mínimo 6, máximo 10. Preferir **7 slides** sempre que o conteúdo permitir. Só ultrapassar 7 se o tema demandar slides adicionais com conteúdo próprio — nunca adicionar slides para preencher.
- **Slide 1 (Capa):** headline + subtítulo opcional
- **Slides 2 a N-1 (Conteúdo):** headline + supporting text (40-80 palavras por slide)
- **Último slide (CTA):** frase focada em pedir para o seguidor **salvar o post** — sem pedido de comentário com palavra-chave. O argumento para salvar deve ser específico ao tema (ex: "Salva esse Seg-CT para consultar antes do próximo fechamento.").
- **Template:** Template C Premium Dark (arquivo `pipeline/data/template-reference.html`)
- **Seta:** usar "← ARRASTE" no slide de capa (seta à ESQUERDA da palavra)

#### Sex-CCTA — Carrossel Isca Digital

- **Objetivo:** incentivar o seguidor a baixar a isca digital aprovada. Cada slide deve comunicar o valor prático do material e criar desejo de recebê-lo.
- **Antes de escrever:** ler `lead-magnet-ideas.md` e extrair: título da isca, descrição do conteúdo e **palavra do CTA** (usar exatamente essa palavra — não inventar outra).
- **Número de slides:** mínimo 6, máximo 10. Preferir **7 slides**. Só ultrapassar 7 se necessário.
- **Slide 1 (Capa):** headline que nomeia o material disponível (ex: "Baixe agora: [título genérico da isca]")
- **Slides 2 a N-1 (Conteúdo):** apresentar os benefícios e tópicos cobertos pela isca — o seguidor deve entender o que vai receber e por que vale a pena
- **Último slide (CTA):** "Comenta [PALAVRA] aqui embaixo e receba [referência genérica ao material]". A PALAVRA deve ser exatamente a mesma registrada em `lead-magnet-ideas.md`. Sem "link na bio". Sem "arrasta pra cima".
- **Template:** Template C Premium Dark (mesmo do Seg-CT)
- **Seta:** usar "← ARRASTE" no slide de capa

---

## Output Format

Salvar em `output/Posts/post-content.md`:

```markdown
# Post Content — {título geral da série}

Data: {YYYY-MM-DD}

---

## Ter-PU1 — {título}
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

## Qua-PU2 — {título}
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

## Qui-PU3 — {título}
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

## Seg-CT — {título}

### Slides
[...estrutura de slides...]

### Legenda
[...]

### Hashtags
[...]

---

## Sex-CCTA — {título}

**Palavra do CTA:** {PALAVRA extraída de lead-magnet-ideas.md}

### Slides
[...estrutura de slides incentivando o download da isca...]

### Legenda
[...]

### Hashtags
[...]
```

## Quality Criteria

- [ ] 5 posts com ângulos DISTINTOS — nenhum repete o mesmo ponto de vista
- [ ] Ter-PU1: CTA é pergunta genuína sobre o tema + direcionamento para comentários — sem palavra-chave, sem emoji
- [ ] Seg-CT: CTA do último slide pede apenas para salvar o post — sem pedido de comentário com palavra-chave
- [ ] Qua-PU2: CTA é pedido de like
- [ ] Qui-PU3: CTA é pedido para seguir no Instagram mencionando a Sucesso Imóvel pelo nome
- [ ] Sex-CCTA: CTA usa "Comenta [PALAVRA]" — PALAVRA idêntica à registrada em `lead-magnet-ideas.md`
- [ ] Sex-CCTA: sem "link na bio" ou "arrasta pra cima" no CTA
- [ ] Qua-PU2: prompt para imagem IA salvo em `output/ai-image-prompt-post2.md`
- [ ] Quote text do Qui-PU3 é impactante e curto (máx. 2 frases)
- [ ] Todos os hooks têm no máximo 125 caracteres
- [ ] Body text do Qua-PU2 tem no máximo 120 caracteres (contados) — frase completa, sem corte
- [ ] Body text do Qui-PU3 tem no máximo 120 caracteres (contados) — frase completa, sem corte
- [ ] Todo conteúdo rastreável à análise do vídeo em `youtube-analysis.md`
- [ ] `output/Posts/post-content.md` salvo antes de encerrar
- [ ] Hashtags de todos os posts são exatamente as listadas em `pipeline/data/hashtags.md` — sem adicionar ou remover
- [ ] **ZERO emojis** em qualquer campo de qualquer post — headline, body, badge, CTA, legenda, hashtags

## Veto Conditions

1. Dois posts com o mesmo ângulo ou ponto de vista
2. CTA do Ter-PU1 não tem pergunta genuína, ou tem palavra-chave específica, ou direciona sem fazer a pergunta antes
3. CTA do Seg-CT pede comentário com palavra-chave — deve focar apenas em salvar o post
4. CTA do Qua-PU2 não pede like
5. CTA do Qui-PU3 não pede para seguir mencionando a Sucesso Imóvel pelo nome
6. CTA do Sex-CCTA usa palavra diferente da registrada em `lead-magnet-ideas.md`
7. CTA do Sex-CCTA menciona "link na bio" ou "arrasta pra cima"
8. Algum dado não rastreável ao vídeo analisado
9. Hook ultrapassa 125 caracteres
10. Body text do Qua-PU2 ou Qui-PU3 ultrapassa 120 caracteres
11. Hashtags diferentes das listadas em `pipeline/data/hashtags.md`
12. **Qualquer emoji encontrado em qualquer campo de qualquer post**

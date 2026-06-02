---
type: agent
agent: iago-instagram
execution: inline
inputFile: squads/youtube-to-instagram/output/{run-id}/Posts/post-content.md
outputFile: squads/youtube-to-instagram/output/{run-id}/Prompts/media-prompts.md
---

# Step 14: Iago Instagram — Geração de Prompts Imagen (nano-banana)

Iago cria **3 prompts para geração de posts completos no Google Imagen (nano-banana)**.

Cada prompt gera uma imagem de Instagram pronta — com design, texto em português e identidade visual da Sucesso Imóvel embutidos na própria imagem.

## Context Loading

Antes de iniciar, Iago deve carregar:
- `squads/youtube-to-instagram/output/{run-id}/Posts/post-content.md` — Conteúdo dos posts criados
- `squads/youtube-to-instagram/output/{run-id}/v1/youtube-analysis.md` — Análise do vídeo original
- `squads/youtube-to-instagram/_memory/memories.md` — Estilo visual aprovado
- `_opensquad/_memory/company.md` — Perfil da Sucesso Imóvel

## Identidade Visual da Sucesso Imóvel

Os prompts devem instruir o Imagen a gerar imagens que sigam rigorosamente este padrão visual:

**Paleta de cores:**
- Fundo: gradiente escuro de preto profundo para roxo escuro (`#0C0018` → `#1A0A2E` → `#0A0A0A`)
- Destaque / accent: roxo vibrante (`#A855F7`)
- Texto principal: branco puro (`#FFFFFF`)
- Texto secundário: branco suave (`rgba(255,255,255,0.85)`)

**Tipografia:**
- Headline: fonte bold/black sem-serifa estilo Montserrat, peso 900, letras levemente condensadas, tamanho grande
- Sub-headline: fonte sem-serifa limpa estilo Inter, peso 500, tamanho médio, cor branco suave

**Elementos visuais recorrentes:**
- Linha de destaque vertical à esquerda (accent line) em roxo
- Orbes/brilhos atmosféricos desfocados no fundo para profundidade
- Uma palavra ou trecho da headline em roxo vibrante (#A855F7) como destaque

**Regras absolutas:**
- **SEM logo** — nenhuma marca, símbolo, ícone de empresa ou logotipo em nenhuma área da imagem
- **Somente dois textos:** headline principal + sub-headline de apoio
- Nenhum badge, tag, card, botão ou elemento de texto adicional

**Formato:** 1080×1350px (proporção 4:5 — feed Instagram)

---

## Instructions

Com base no **tema central** e nos **3 ângulos editoriais** extraídos do post-content.md, criar 3 prompts — um por ângulo.

Cada prompt descreve um **post completo do Instagram** com:
1. O **layout e design** seguindo a identidade visual da Sucesso Imóvel
2. A **headline** em português — frase de impacto, bold, com uma palavra ou trecho em roxo
3. A **sub-headline** em português — frase de apoio que complementa a headline (1 linha, sem repetir a headline)
4. Um **elemento visual de fundo** (composição abstrata, textura, gradiente ou fotografia desfocada) que reforce o tema sem competir com o texto

### Os 3 ângulos obrigatórios (derivados do post-content.md):

1. **Alerta / Risco** — o problema principal: o que pode dar errado
2. **Dado / Evidência** — a consequência técnica ou jurídica
3. **Reflexão / Princípio** — a provocação que o corretor deve internalizar

### CTA fixo para os 3 posts

A legenda de **todos** os posts gerados neste step deve encerrar com este CTA fixo, sem alterações:

> Gostou do conteúdo? Deixe o seu like! É rapidinho e ajuda muito a gente na criação de mais conteúdo ❤️

---

## Output Format

Salvar em `output/{run-id}/Prompts/media-prompts.md`:

```markdown
# Prompts Imagen — {Tema}

Data: {YYYY-MM-DD}
Tema central: {tema extraído do post-content.md}
Ferramenta: Google Imagen via nano-banana
Formato alvo: 1080×1350px (feed Instagram 4:5)

---

### Post 1 — Alerta / Risco
**Ângulo:** {descrição do ângulo}
**Headline:** {headline exata em português}
**Sub-headline:** {sub-headline exata em português}
**Prompt:**
{prompt em inglês descrevendo o post completo}

**Legenda:**
{legenda completa — hook + corpo + CTA — copiada do post-content.md correspondente}

**Hashtags:**
{hashtags copiadas do post-content.md correspondente}

---

### Post 2 — Dado / Evidência
**Ângulo:** {descrição do ângulo}
**Headline:** {headline exata em português}
**Sub-headline:** {sub-headline exata em português}
**Prompt:**
{prompt em inglês descrevendo o post completo}

**Legenda:**
{legenda completa — hook + corpo + CTA — copiada do post-content.md correspondente}

**Hashtags:**
{hashtags copiadas do post-content.md correspondente}

---

### Post 3 — Reflexão / Princípio
**Ângulo:** {descrição do ângulo}
**Headline:** {headline exata em português}
**Sub-headline:** {sub-headline exata em português}
**Prompt:**
{prompt em inglês descrevendo o post completo}

**Legenda:**
{legenda completa — hook + corpo + CTA — copiada do post-content.md correspondente}

**Hashtags:**
{hashtags copiadas do post-content.md correspondente}
```

## Quality Criteria

- [ ] 3 prompts com ângulos editoriais distintos
- [ ] Cada prompt tem headline + sub-headline em português especificados
- [ ] Nenhum prompt menciona logo, marca ou logotipo
- [ ] Apenas headline e sub-headline como texto na imagem — nenhum elemento adicional
- [ ] Layout segue identidade visual da Sucesso Imóvel (dark background, roxo accent, sem logo)
- [ ] Legenda e hashtags incluídas para cada post, copiadas do post-content.md
- [ ] CTA de todos os posts encerra com o texto fixo: "Gostou do conteúdo? Deixe o seu like! É rapidinho e ajuda muito a gente na criação de mais conteúdo ❤️"
- [ ] Hashtags são exatamente as 6 oficiais — sem adições ou substituições
- [ ] Arquivo salvo em `output/{run-id}/Prompts/media-prompts.md`

## Veto Conditions

1. Qualquer menção a logo, ícone de marca ou símbolo da empresa no prompt
2. Mais de dois elementos de texto na imagem (badge, tag, card, botão, etc.)
3. Dois prompts com o mesmo ângulo editorial ou a mesma headline
4. Sub-headline que repete a ideia da headline sem acrescentar informação
5. Legenda ou hashtags ausentes em qualquer dos 3 posts
6. Hashtags diferentes das 6 oficiais
7. Arquivo salvo fora da pasta `Prompts/`

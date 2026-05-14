---
type: agent
agent: iago-instagram
execution: inline
inputFile: squads/youtube-to-instagram/output/Posts/post-content.md
outputFile: squads/youtube-to-instagram/output/{run-id}/Roteiros/
---

# Step 04b: Iago Instagram — Criação dos Roteiros

Iago cria os roteiros de vídeo com base no conteúdo aprovado no step 04: um roteiro para YouTube e cinco roteiros para Reels/Shorts.

## Context Loading

Antes de iniciar, Iago deve carregar:
- `squads/youtube-to-instagram/output/{run-id}/Posts/post-content.md` — Conteúdo dos posts já criados
- `squads/youtube-to-instagram/output/{run-id}/v1/youtube-analysis.md` — Análise do vídeo original
- `_opensquad/_memory/company.md` — Perfil da Sucesso Imóvel

## Estrutura de Output

Dois arquivos salvos em `output/{run-id}/Roteiros/`:
- `roteiro-youtube-{slug}.md` — Roteiro completo para YouTube
- `roteiros-reels-{slug}.md` — 5 roteiros para Reels/Shorts

## Instructions

### Tarefa 1: Roteiro YouTube

**Diretrizes:**
- Duração: até 20 minutos (sem mínimo — incluir tudo que for pertinente)
- Tom: didático, direto, com exemplos práticos do cotidiano do público-alvo
- Estrutura obrigatória:
  1. **Abertura/Hook** — pergunta ou afirmação contraintuitiva relacionada ao tema (1–2 min)
  2. **Conceito central** — explicação do tema base (2–4 min)
  3. **Aprofundamento** — subtópicos, tipos, modalidades (3–5 min)
  4. **Efeitos ou Consequências** — os impactos práticos do tema (4–6 min)
  5. **Situações reais** — 2 a 3 cenários do dia a dia do público-alvo (3–5 min)
  6. **Encerramento + CTA** — síntese + chamada para like/inscrição/salvar (1–2 min)
- Incluir ao final: referências legais usadas + descrição completa para YouTube com capítulos

**Formato de cada seção:**
```
**[CÂMERA — indicação de ação/ângulo]**
**[BLOCO X — Nome do Bloco (mm:ss – mm:ss)]**
[texto do roteiro]
```

### Tarefa 2: Roteiros Reels

**Diretrizes:**
- 5 roteiros distintos — cada um com ângulo diferente derivado do tema
- Duração: ~60 segundos cada (~130 palavras/minuto)
- Estrutura obrigatória de cada Reel:
  - **Hook (0:00–0:05):** frase de impacto — afirmação contraintuitiva, situação real ou dado surpreendente. Deve parar o scroll em 3 segundos.
  - **Desenvolvimento (0:05–0:48):** o argumento central — direto, sem rodeios, com exemplo prático
  - **CTA (0:48–0:60):** micro-chamada — salvar, comentar, seguir ou compartilhar (variar entre os 5)

**Os 5 ângulos obrigatórios:**
1. O conceito central do tema (definição, base jurídica)
2. O risco mais grave para o público-alvo (o que pode dar errado)
3. A situação mais comum de problema real (caso específico)
4. O detalhe que ninguém verifica (ponto técnico ignorado)
5. O cenário de nicho (variação menos óbvia do tema)

**Formato de cada Reel:**
```
## REEL N — Título

**Ângulo:** [descrição do ângulo]
**Hook:** [frase de abertura]
**Duração estimada:** ~60 segundos

---

**[CÂMERA — DR. JEORGE]**

**[HOOK — 0:00–0:05]**
[texto]

**[DESENVOLVIMENTO — 0:05–0:48]**
[texto]

**[CTA — 0:48–0:60]**
[texto]

---

**LEGENDA SUGERIDA:** [texto pronto para Instagram]
**HASHTAGS:** [10 hashtags]
```

Ao final do arquivo, incluir tabela-resumo com os 5 Reels e sequência de publicação sugerida (dias entre posts).

## Output Format

Dois arquivos em `output/{run-id}/Roteiros/`:

**Arquivo 1:** `roteiro-youtube-{slug}.md`
```markdown
# Roteiro YouTube — {Título}

**Duração estimada:** X a Y minutos
**Público-alvo:** {público}
**Referência legal:** {leis/artigos}
**Tom:** {tom}

---

[estrutura do roteiro]

---

## REFERÊNCIAS LEGAIS
[lista de artigos citados]

## DESCRIÇÃO DO VÍDEO (YouTube)
[descrição completa com capítulos]
```

**Arquivo 2:** `roteiros-reels-{slug}.md`
```markdown
# Roteiros Reels — {Tema}

**Duração:** ~60 segundos cada
[5 roteiros estruturados]

## RESUMO DOS 5 REELS
[tabela-resumo + sequência de publicação]
```

## Quality Criteria

- [ ] Roteiro YouTube: cobre todos os subtópicos relevantes do tema, sem exceder 20 min
- [ ] Roteiro YouTube: inclui referências legais e descrição com capítulos
- [ ] 5 Reels com ângulos distintos — nenhum repete o mesmo ponto de vista
- [ ] Cada Reel tem hook nos primeiros 5 segundos
- [ ] Cada Reel tem CTA diferenciado (variar entre salvar / comentar / seguir / compartilhar)
- [ ] Legenda e hashtags prontos para cada Reel
- [ ] Ambos os arquivos salvos em `output/{run-id}/Roteiros/`
- [ ] **ZERO emojis** em qualquer parte dos roteiros — texto do script, legendas, hashtags

## Veto Conditions

1. Roteiro YouTube sem hook na abertura
2. Dois Reels com o mesmo ângulo ou hook similar
3. Algum dado não rastreável ao vídeo analisado ou ao Código Civil
4. Arquivos salvos fora da pasta `Roteiros/`
5. Roteiro sem referências legais citadas
6. **Qualquer emoji encontrado em qualquer parte dos roteiros**

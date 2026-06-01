---
type: agent
agent: renata-revisao
execution: inline
inputFile: squads/youtube-to-instagram/output/Posts/post-content.md
outputFile: squads/youtube-to-instagram/output/review.md
on_reject: 4
---

# Step 07: Renata Revisão — Quality Review

Renata Revisão avalia o conteúdo textual e as imagens renderizadas contra os critérios de qualidade definidos, emitindo um veredito estruturado.

## Context Loading

Antes de iniciar, Renata deve carregar:
- `squads/youtube-to-instagram/output/Posts/post-content.md` — Texto completo dos slides, legenda e hashtags
- `squads/youtube-to-instagram/output/Posts/` — PNGs renderizados (verificação visual)
- `squads/youtube-to-instagram/pipeline/data/quality-criteria.md` — Critérios e thresholds de avaliação
- `squads/youtube-to-instagram/output/youtube-analysis.md` — Análise do vídeo (fonte de verdade para verificar aderência)

## Instructions

### Processo de Review

1. Ler `post-content.md` na íntegra — todos os slides, a legenda completa e as hashtags.
2. Ler os PNGs em `output/Posts/` para verificar qualidade visual das imagens.
3. Ler `pipeline/data/quality-criteria.md` para os critérios de avaliação e thresholds.
4. Avaliar cada critério individualmente com score 1-10 e justificativa de ao menos uma frase.
5. Verificar hard rejection triggers:
   - Dado inventado (não rastreável ao vídeo) → REJEITAR imediatamente
   - CTA ausente ou genérico no último slide → REJEITAR imediatamente
6. Contar palavras de cada slide (headline + supporting text combinados):
   - Slides < 40 palavras → REJEITAR
   - Slides > 80 palavras → sinalizar como Suggestion (não-bloqueante)
7. Calcular média geral. Aplicar regra de decisão:
   - >= 7.0 + nenhum score < 4 → APROVAR
   - >= 7.0 + algum score entre 4-6 → APROVAR CONDICIONAL
   - < 7.0 → REJEITAR
8. Redigir o review estruturado com tabela de scores, feedback detalhado e veredito final.
9. Salvar em `output/review.md`.

### Critérios Avaliados

| Critério | O que verificar |
|----------|-----------------|
| Hook da legenda (125 chars) | Impacto, contagem de caracteres, especificidade |
| Qualidade dos slides | Legibilidade visual, contraste, layout sem clipping |
| Contagem de palavras | Todos os slides entre 40-80 palavras |
| Tom e voz da marca | Consultivo B2B, sem linguagem ao consumidor final |
| CTA e engajamento | CTA específico, pergunta de engajamento presente |
| Aderência ao vídeo | Todo dado rastreável ao vídeo analisado |
| Identidade visual | Template C Premium Dark consistente, accent keywords em roxo |
| Hashtags | 10-15 tags, mix relevante, #sucessoimovel presente |

### Regra de Escalada

Se este for o **3º ciclo de revisão** no mesmo conteúdo sem aprovação:
- Não rejeitar novamente automaticamente
- Apresentar ao usuário o histórico de ciclos com os principais problemas recorrentes
- Perguntar se quer continuar iterando ou descartar o post e escolher outra ideia

## Output Format

```markdown
==============================
 REVIEW VEREDITO: {APROVAR / REJEITAR / APROVAR CONDICIONAL}
==============================

Conteúdo: {titulo_do_post}
Tipo: {Seg-CT X slides / Post único}
Revisão: {N} de 3
Data: {YYYY-MM-DD}

------------------------------
 TABELA DE SCORES
------------------------------
| Critério                    | Score | Resumo                          |
|-----------------------------|-------|---------------------------------|
| Hook da legenda (125 chars) | X/10  | {justificativa_breve}           |
| Qualidade dos slides        | X/10  | {justificativa_breve}           |
| Contagem de palavras        | X/10  | {justificativa_breve}           |
| Tom e voz da marca          | X/10  | {justificativa_breve}           |
| CTA e engajamento           | X/10  | {justificativa_breve}           |
| Aderência ao vídeo          | X/10  | {justificativa_breve}           |
| Identidade visual           | X/10  | {justificativa_breve}           |
| Hashtags                    | X/10  | {justificativa_breve}           |
------------------------------
 MÉDIA GERAL: X.X/10
------------------------------

FEEDBACK DETALHADO:

Strength: {o que funcionou — específico}

{Required change: ou Suggestion (não-bloqueante):} {feedback_com_localização_e_correção}

VEREDITO: {APROVAR / REJEITAR / APROVAR CONDICIONAL} — {justificativa_de_uma_linha}
```

## Quality Criteria

- [ ] Todos os critérios foram avaliados e têm score com justificativa
- [ ] Contagem de palavras de cada slide verificada explicitamente
- [ ] Hard rejection triggers verificados (dado inventado, CTA ausente, slide < 40 palavras)
- [ ] Pelo menos um "Strength:" presente no feedback
- [ ] Required changes e Suggestions não-bloqueantes estão claramente separados
- [ ] Veredito final é inequívoco e justificado em uma linha
- [ ] `output/review.md` salvo antes de encerrar

## Veto Conditions

Rejeitar e refazer se QUALQUER condição for verdadeira:
1. O review emite APROVAR mas algum critério tem score < 4 (contradição com hard rejection trigger)
2. O review não tem nenhum "Strength:" — ausência de ponto positivo é sinal de review incompleto

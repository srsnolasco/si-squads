---
task: "Review"
order: 1
input: |
  - post_content: Texto dos slides, legenda e hashtags (post-content.md)
  - slide_pngs: Imagens renderizadas em output/slides/
  - quality_criteria: Critérios de avaliação (quality-criteria.md)
output: |
  - review_report: Veredito estruturado com scores, feedback por critério e required changes
---

# Review

Avalia o conteúdo textual e as imagens renderizadas contra os critérios de quality-criteria.md. Emite veredito APROVAR / REJEITAR / APROVAR CONDICIONAL com scores individuais, feedback específico e acionável para cada critério.

## Process

1. Ler `post-content.md` na íntegra — todos os slides, a legenda completa e as hashtags.
2. Ler os PNGs em `output/slides/` para verificar qualidade visual das imagens.
3. Ler `pipeline/data/quality-criteria.md` para os critérios de avaliação e thresholds.
4. Avaliar cada critério individualmente com score 1-10 e justificativa de ao menos uma frase.
5. Verificar hard rejection triggers: dado inventado (não rastreável ao vídeo) ou CTA ausente = REJEITAR imediatamente.
6. Contar palavras de cada slide (headline + supporting text combinados). Slides < 40 palavras = REJEITAR.
7. Calcular média geral. Aplicar regra de decisão: >= 7 + nenhum score < 4 = APROVAR; >= 7 + algum score 4-6 = APROVAR CONDICIONAL; < 7 = REJEITAR.
8. Redigir o review estruturado com: tabela de scores, feedback por critério, required changes (se houver), sugestões não-bloqueantes, e veredito final.
9. Salvar em `output/review.md`.

## Output Format

```markdown
==============================
 REVIEW VEREDITO: {APROVAR / REJEITAR / APROVAR CONDICIONAL}
==============================

Conteúdo: {titulo_do_post}
Tipo: {Carrossel X slides / Post único}
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

## Output Example

```markdown
==============================
 REVIEW VEREDITO: APROVAR
==============================

Conteúdo: 4 cláusulas que corretores esquecem — e que podem custar a comissão
Tipo: Carrossel 7 slides
Revisão: 1 de 3
Data: 2026-05-13

------------------------------
 TABELA DE SCORES
------------------------------
| Critério                    | Score | Resumo                                                          |
|-----------------------------|-------|-----------------------------------------------------------------|
| Hook da legenda (125 chars) | 9/10  | "Você fecha o contrato. O cliente some." — 45 chars, impacto alto |
| Qualidade dos slides        | 8/10  | Slides 2-5 com 50-65 palavras; slide 6 no limite inferior (42) |
| Contagem de palavras        | 9/10  | Todos acima de 40 palavras; nenhum acima de 80                  |
| Tom e voz da marca          | 9/10  | Consultivo, B2B, parceiro do corretor — sem linguagem ao consumidor |
| CTA e engajamento           | 8/10  | "Comenta CONTRATO" específico; pergunta de engajamento presente |
| Aderência ao vídeo          | 9/10  | Todas as 4 cláusulas rastreáveis ao vídeo analisado             |
| Identidade visual           | 8/10  | Template C Premium Dark consistente; accent line presente       |
| Hashtags                    | 8/10  | 12 hashtags, bom mix; #sucessoimovel presente                   |
------------------------------
 MÉDIA GERAL: 8.5/10
------------------------------

FEEDBACK DETALHADO:

Strength: O hook da legenda ("Você fecha o contrato. O cliente some.") é um dos mais fortes do squad — two-sentence narrative que cria empatia imediata e urgência sem ser alarmista.

Strength: A cláusula 4 (slide 5) sobre responsabilidade solidária é o ponto mais diferenciado do post — informação que o corretor raramente sabe e que agrega valor real.

Suggestion (não-bloqueante): Slide 6 (síntese) tem 42 palavras — dentro do mínimo de 40, mas próximo do limite. Uma linha adicional de contexto elevaria o valor entregue sem comprometer a legibilidade.

Suggestion (não-bloqueante): A tag "Jurídico" no header poderia ser mais específica — "Contratos" reflete melhor o conteúdo e aumenta o contexto visual ao primeiro olhar.

VEREDITO: APROVAR — Conteúdo atende todos os critérios de qualidade. Sugestões não-bloqueantes incluídas para iteração futura.
```

## Quality Criteria

- [ ] Todos os critérios de quality-criteria.md foram avaliados e têm score
- [ ] Todo score tem justificativa escrita na mesma linha ou imediatamente após
- [ ] Contagem de palavras de cada slide foi verificada explicitamente
- [ ] Dados não rastreáveis ao vídeo foram identificados (se houver)
- [ ] Hard rejection triggers verificados (dado inventado, CTA ausente, slide < 40 palavras)
- [ ] Pelo menos um "Strength:" presente no feedback
- [ ] Required changes e Suggestions não-bloqueantes estão claramente separados
- [ ] Veredito final é inequívoco e justificado em uma linha

## Veto Conditions

Rejeitar e refazer se QUALQUER condição for verdadeira:
1. O review emite APROVAR mas algum critério tem score < 4 (contradição com hard rejection trigger)
2. O review não tem nenhum "Strength:" — ausência de ponto positivo é sinal de review incompleto

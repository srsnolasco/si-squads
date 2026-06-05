---
type: agent
agent: yago-video
execution: subagent
inputFile: squads/youtube-to-instagram/output/{run-id}/v1/doc-source-analysis.md
outputFile: squads/youtube-to-instagram/output/{run-id}/post-ideas.md
model_tier: powerful
---

# Step 09: Yago Vídeo — Geração de Ideias de Posts

Yago Vídeo lê o relatório de análise do vídeo e gera exatamente 5 ideias de posts — uma por tipo de post do squad.

## Context Loading

Antes de iniciar, Yago deve carregar:
- `squads/youtube-to-instagram/output/{run-id}/v1/doc-source-analysis.md` — Relatório completo da análise do vídeo
- `squads/youtube-to-instagram/output/{run-id}/lead-magnet-ideas.md` — Isca digital aprovada (para extrair a palavra do CTA do Sex-CCTA)
- `squads/youtube-to-instagram/pipeline/data/domain-framework.md` — Classificação de conteúdo e design
- `_opensquad/_memory/company.md` — Perfil da Sucesso Imóvel

## Instructions

Com base no relatório de análise, gerar exatamente **5 ideias de posts** — uma por tipo, na ordem abaixo. O ângulo editorial e o hook de cada ideia devem ser derivados dos insights e trechos identificados na análise.

| Post | Formato | Ângulo | CTA |
|------|---------|--------|-----|
| Seg-CT | Carrossel Tutorial — preferir 7 slides | Tutorial/aprofundamento — o "como funciona" | Salvar o post |
| Ter-PU1 | Post único + foto Dr. Jeorge | Principal — tema central do vídeo | Pergunta genuína + comentários |
| Qua-PU2 | Post único + imagem IA | Impacto/consequência — o "e agora?" | Like |
| Qui-PU3 | Post único — só texto | Reflexão/princípio — o "por que isso importa" | Seguir a Sucesso Imóvel |
| Sex-CCTA | Carrossel — preferir 7 slides | Isca digital — incentivar o seguidor a baixar o material | Comentar [PALAVRA] — extrair de `lead-magnet-ideas.md` |

**Regra do Sex-CCTA:** a palavra do CTA deve ser extraída do campo `Palavra do CTA` da isca digital aprovada em `lead-magnet-ideas.md`. Não inventar uma palavra nova — usar exatamente a mesma.

Para cada ideia, definir:
- **Título da ideia**: uma linha que resume o post proposto
- **Ângulo editorial**: tom e abordagem específicos ao tipo de post
- **Hook proposto**: primeira frase ou manchete que captura atenção (máx. 125 chars)
- **Conceito visual**: sugestão de composição e destaque visual
- **Por que funciona**: justificativa baseada nos insights da análise do vídeo

Salvar as ideias em `output/{run-id}/post-ideas.md`.

## Output Format

```markdown
# Ideias de Post — {título do vídeo}

Baseado em: output/{run-id}/v1/doc-source-analysis.md
Data: {YYYY-MM-DD}

---

## Seg-CT — {título da ideia}

**Formato:** Carrossel Tutorial — 7 slides (preferencial)
**Ângulo:** {tutorial/aprofundamento — o "como funciona"}
**Hook:** "{primeira frase ou manchete — máx. 125 chars}"
**Conceito visual:** {descrição do layout e destaque — Template C Premium Dark}
**Por que funciona:** {justificativa baseada na análise}

---

## Ter-PU1 — {título da ideia}

**Formato:** Post único + foto Dr. Jeorge
**Ângulo:** {tema central do vídeo}
**Hook:** "{primeira frase ou manchete — máx. 125 chars}"
**Conceito visual:** {descrição — template roxo/preto}
**Por que funciona:** {justificativa baseada na análise}

---

## Qua-PU2 — {título da ideia}

**Formato:** Post único + imagem IA
**Ângulo:** {impacto/consequência — o "e agora?"}
**Hook:** "{primeira frase ou manchete — máx. 125 chars}"
**Conceito visual:** {descrição — template carvão/roxo claro}
**Por que funciona:** {justificativa baseada na análise}

---

## Qui-PU3 — {título da ideia}

**Formato:** Post único — só texto
**Ângulo:** {reflexão/princípio — o "por que isso importa"}
**Hook:** "{primeira frase ou manchete — máx. 125 chars}"
**Conceito visual:** {descrição — template branco/lavanda}
**Por que funciona:** {justificativa baseada na análise}

---

## Sex-CCTA — {título da ideia}

**Formato:** Carrossel — 7 slides (preferencial) — mesmo estilo e design do Seg-CT (Template C Premium Dark)
**Ângulo:** Isca digital — incentivar o seguidor a baixar o material aprovado
**CTA:** Comentar {PALAVRA} — extraída do campo `Palavra do CTA` de `lead-magnet-ideas.md`
**Hook:** "{primeira frase ou manchete — máx. 125 chars}"
**Conceito visual:** {descrição — Template C Premium Dark, accent roxo, slides destacando o valor da isca}
**Por que funciona:** {justificativa — conexão entre o tema da semana e o valor da isca digital}
```

## Quality Criteria

- [ ] Exatamente 5 ideias — uma por tipo de post (Seg-CT, Ter-PU1, Qua-PU2, Qui-PU3, Sex-CCTA)
- [ ] Cada ideia tem: título, ângulo, hook, conceito visual e justificativa
- [ ] Hooks específicos, rastreáveis ao conteúdo do vídeo e com máx. 125 chars
- [ ] Seg-CT e Sex-CCTA especificam 7 slides como preferencial
- [ ] Conceitos visuais referenciam os templates corretos por tipo de post
- [ ] Cada ideia aborda o tema por um ângulo diferente — nenhum repete o mesmo ponto de vista
- [ ] Palavra do CTA do Sex-CCTA extraída de `lead-magnet-ideas.md` — não inventada
- [ ] `output/{run-id}/post-ideas.md` salvo antes de encerrar

## Veto Conditions

1. Hook ou dado não rastreável ao relatório de análise — dado inventado é recusa automática
2. Número de ideias diferente de 5
3. Algum tipo de post ausente (Seg-CT, Ter-PU1, Qua-PU2, Qui-PU3 ou Sex-CCTA)
4. Hook ultrapassa 125 caracteres
5. Dois posts com o mesmo ângulo editorial
6. Palavra do CTA do Sex-CCTA diferente da registrada em `lead-magnet-ideas.md`

---
task: "Generate Ideas"
order: 2
input: |
  - video_analysis: Resultado da tarefa analyze-youtube (tópicos, insights, dados)
  - company_context: Perfil da Sucesso Imóvel (tom, público, proposta de valor)
output: |
  - ideas: Lista de 3-5 ideias de posts com formato, ângulo, conceito visual e origem
---

# Generate Ideas

Com base na análise do vídeo, gera 3 a 5 ideias de posts para o Instagram da Sucesso Imóvel. Cada ideia especifica o formato (carrossel ou post único), o ângulo editorial, o conceito visual e o trecho do vídeo que a originou.

## Process

1. Revisar os tópicos e insights da análise do vídeo.
2. Para cada tópico relevante, avaliar: qual formato serve melhor ao conteúdo? (lista → Listicle; processo → Tutorial; mito → Mito vs Realidade; dado único → Post único; tese → Editorial)
3. Definir o ângulo editorial para cada ideia: Autoridade Consultiva, Alerta e Urgência, Educativo Direto, Dados e Evidências, Provocativo Inteligente, ou Storytelling (ver tone-of-voice.md).
4. Descrever o conceito visual em uma linha (o que o designer vai criar).
5. Ordenar as ideias do maior para o menor potencial de engajamento (saves + shares estimados).
6. Selecionar as 3-5 melhores. Descartar ideias redundantes ou sem potencial para o público B2B.
7. Salvar o resultado em post-ideas.md.

## Output Format

```markdown
# Ideias de Posts — {titulo_do_video}

**Fonte:** {url}
**Analisado por:** Yago Vídeo

---

## Ideia 1 — {titulo_da_ideia} ⭐ (maior potencial)

**Formato:** Carrossel / Post único
**Estrutura:** Listicle / Tutorial / Editorial / Mito vs Realidade / Problema→Solução / Single Image
**Ângulo:** {nome_do_tom}
**Conceito visual:** {descricao_em_uma_linha}
**Origem no vídeo:** {qual_topico_ou_trecho_gerou_esta_ideia}

---

## Ideia 2 — {titulo_da_ideia}
...

---

## Ideia N — {titulo_da_ideia}
...
```

## Output Example

```markdown
# Ideias de Posts — Os erros mais comuns em contratos de compra e venda

**Fonte:** https://youtube.com/watch?v=abc123
**Analisado por:** Yago Vídeo

---

## Ideia 1 — 4 cláusulas que corretores esquecem — e que podem custar a comissão ⭐

**Formato:** Carrossel
**Estrutura:** Listicle (7-8 slides)
**Ângulo:** Alerta e Urgência
**Conceito visual:** Cards numerados com cada cláusula em título grande e consequência em texto de apoio; paleta Premium Dark
**Origem no vídeo:** Tópicos 1, 2, 3 e 4 — Dr. Ricardo Alves lista os 4 erros mais comuns em contratos

---

## Ideia 2 — Quem paga o ITBI? A resposta que todo corretor precisa dar com segurança

**Formato:** Post único
**Estrutura:** Single Image (pergunta + resposta em destaque)
**Ângulo:** Educativo Direto
**Conceito visual:** Pergunta em grande, resposta destacada em roxo, rodapé com @sucessoimovel
**Origem no vídeo:** Tópico 2 — responsabilidade pelo ITBI discutida pelo Dr. Alves

---

## Ideia 3 — Procuração geral não serve para venda de imóvel (e o cartório vai te barrar)

**Formato:** Carrossel
**Estrutura:** Problema → Solução (6 slides)
**Ângulo:** Autoridade Consultiva
**Conceito visual:** Slide 1 com o "erro" em destaque vermelho/roxo; slides seguintes com a solução em branco
**Origem no vídeo:** Tópico 3 — vício de procuração sem poderes específicos

---

## Ideia 4 — Contratos sem cláusula de penalidade: o corretor que não protege o cliente perde o cliente

**Formato:** Carrossel
**Estrutura:** Antes e Depois (6 slides)
**Ângulo:** Provocativo Inteligente
**Conceito visual:** Antes (problema) em tons escuros; Depois (solução) com destaque roxo
**Origem no vídeo:** Tópico 4 — prazo de entrega sem penalidade por atraso
```

## Quality Criteria

- [ ] Entre 3 e 5 ideias entregues
- [ ] Cada ideia tem: título, formato, estrutura, ângulo, conceito visual e origem no vídeo
- [ ] Pelo menos uma ideia de carrossel e uma de post único
- [ ] Todas as ideias derivam de tópicos identificados na análise do vídeo
- [ ] Ideias ordenadas do maior para o menor potencial de engajamento
- [ ] Nenhuma ideia é genérica — todas são específicas ao conteúdo do vídeo

## Veto Conditions

Rejeitar e refazer se QUALQUER condição for verdadeira:
1. Alguma ideia não tem origem rastreável no vídeo analisado
2. Todas as ideias são do mesmo formato (ex: só carrosséis) — deve haver diversidade

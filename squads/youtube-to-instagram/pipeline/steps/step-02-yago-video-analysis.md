---
type: agent
agent: yago-video
execution: subagent
inputFile: squads/youtube-to-instagram/output/youtube-focus.md
outputFile: squads/youtube-to-instagram/output/post-ideas.md
model_tier: powerful
run_id_slug: true
---

# Step 03: Yago Vídeo — Análise do Conteúdo

Yago Vídeo analisa o conteúdo do vídeo (YouTube ou local transcrito) e gera ideias de posts para o Instagram.

## Context Loading

Antes de iniciar, Yago deve carregar:
- `squads/youtube-to-instagram/output/youtube-focus.md` — fonte do vídeo e foco informados pelo usuário
- `squads/youtube-to-instagram/output/video-transcript.md` — transcrição (se fonte local) ou marcador "none" (se YouTube)
- `squads/youtube-to-instagram/pipeline/data/research-brief.md` — Framework de análise YouTube→Instagram
- `squads/youtube-to-instagram/pipeline/data/domain-framework.md` — Classificação de conteúdo e design
- `_opensquad/_memory/company.md` — Perfil da Sucesso Imóvel para contextualizar a análise

## Instructions

### Tarefa 1: Analisar o Vídeo

1. Ler `output/youtube-focus.md` para verificar `source_type` (youtube ou local) e o foco informado.

**Se `source_type: youtube`:**
2. Usar `web_fetch` na URL do YouTube para obter: título, descrição, canal, duração, data de publicação.
3. Identificar os principais tópicos abordados no vídeo.

**Se `source_type: local`:**
2. Ler `output/video-transcript.md` para obter a transcrição completa do vídeo.
3. O título do vídeo será o `file_name` sem extensão (formatar de forma legível, ex: "minha-aula.mp4" → "Minha Aula").
4. Identificar os principais tópicos abordados com base na transcrição.

**Ambos os casos:**
4. Extrair insights, dados, estatísticas ou afirmações relevantes para corretores e o mercado imobiliário.
5. Mapear os pontos de maior valor educacional ou de autoridade para a audiência-alvo.
6. Salvar a análise completa em `output/youtube-analysis.md`.

### Tarefa 2: Gerar Ideias de Posts

1. Com base na análise, gerar entre 3 e 5 ideias de posts para o Instagram da Sucesso Imóvel.
2. Para cada ideia, definir:
   - **Título da ideia**: uma linha que resume o post proposto
   - **Formato**: Carrossel (N slides) ou Post único
   - **Ângulo editorial**: tom e abordagem (educativo, alerta, dados, storytelling, etc.)
   - **Hook proposto**: primeira frase ou manchete que captura atenção
   - **Conceito visual**: sugestão de template/composição e destaque visual
   - **Por que funciona**: justificativa baseada na audiência e no conteúdo do vídeo
3. Ordenar as ideias do maior para o menor potencial de engajamento.
4. Salvar as ideias em `output/post-ideas.md`.

## Output Format

```markdown
# Ideias de Post — {título do vídeo}

Vídeo analisado: {URL}
Canal: {nome do canal}
Data: {data de análise}

---

## Ideia 1: {título da ideia}

**Formato:** {Carrossel N slides / Post único}
**Ângulo:** {tom editorial}
**Hook:** "{primeira frase ou manchete}"
**Conceito visual:** {descrição do layout e destaque}
**Por que funciona:** {justificativa 1-2 frases}

---

## Ideia 2: {título da ideia}
[...]
```

## Output Example

```markdown
# Ideias de Post — 4 Cláusulas que Corretores Esquecem no Contrato

Vídeo analisado: https://www.youtube.com/watch?v=abc123
Canal: Sucesso Imóvel
Data: 2026-05-12

---

## Ideia 1: As 4 cláusulas que podem custar sua comissão

**Formato:** Carrossel 7 slides
**Ângulo:** Alerta e Urgência — corretor como protagonista que precisa se proteger
**Hook:** "Você fecha o contrato. O cliente some."
**Conceito visual:** Template C Premium Dark; cada slide destaca uma cláusula com número em roxo e texto de alerta em branco
**Por que funciona:** O medo de perder comissão é o gatilho mais forte para corretores — o vídeo lista problemas reais e rastreáveis

---

## Ideia 2: Cláusula de arrependimento — o que nenhum corretor te contou

**Formato:** Post único
**Ângulo:** Educativo Direto — desmistificar um conceito jurídico complexo
**Hook:** "Seu cliente pode desistir a qualquer momento. Sem multa. Você sabia?"
**Conceito visual:** Template C com card translúcido roxo central; estatística em destaque no centro
**Por que funciona:** Um único conceito bem explicado gera mais salvamentos do que um carrossel incompleto

---

## Ideia 3: Checklist de contrato para corretor imobiliário

**Formato:** Carrossel 5 slides
**Ângulo:** Autoridade Consultiva — Sucesso Imóvel como guia especializado
**Hook:** "Antes de assinar qualquer contrato, o seu cliente precisa ter isso."
**Conceito visual:** Template C; slides com ícones de check em roxo e texto descritivo limpo
**Por que funciona:** Checklists têm altíssima taxa de salvamento no Instagram — conteúdo de referência que o corretor guarda
```

## Quality Criteria

- [ ] Análise do vídeo inclui título, canal, tópicos principais e insights extraídos
- [ ] Entre 3 e 5 ideias geradas, ordenadas por potencial de engajamento
- [ ] Cada ideia tem: título, formato, ângulo, hook, conceito visual e justificativa
- [ ] Hooks são específicos (não genéricos) e rastreáveis ao conteúdo do vídeo
- [ ] Ideias são diversificadas em formato (ao menos uma carrossel e uma post único, se viável)
- [ ] Conceitos visuais fazem referência ao Template C Premium Dark
- [ ] `output/post-ideas.md` salvo antes de encerrar

## Veto Conditions

Rejeitar e refazer se QUALQUER condição for verdadeira:
1. Algum hook ou dado não é rastreável ao vídeo analisado — dado inventado é recusa automática
2. Todas as ideias têm o mesmo formato (todas carrossel ou todas post único)
3. Menos de 3 ideias geradas

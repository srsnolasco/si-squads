---
type: agent
agent: iago-instagram
execution: inline
inputFile: squads/youtube-to-instagram/output/{run-id}/Posts/post-content.md
outputFile: squads/youtube-to-instagram/output/{run-id}/Stories/
---

# Step: Iago Instagram — Roteiros de Stories Diários

Iago cria os roteiros de Stories para todos os dias da semana. Cada story tem horário definido, tipo editorial, texto sugerido, sticker obrigatório e CTA. O conteúdo de cada story referencia o post e o reel do dia correspondente.

## Context Loading

Antes de iniciar, Iago deve carregar:
- `squads/youtube-to-instagram/output/{run-id}/Posts/post-content.md` — Conteúdo dos 5 posts (referência para stories de Seg a Sex)
- `squads/youtube-to-instagram/output/{run-id}/Roteiros/` — Roteiros dos 6 Reels Virais (referência para teaser de cada dia)
- `squads/youtube-to-instagram/output/{run-id}/lead-magnet-ideas.md` — Isca digital aprovada (referência para stories de Sex)
- `_opensquad/_memory/company.md` — Perfil da Sucesso Imóvel

## Estrutura de Output

Oito arquivos salvos em `output/{run-id}/Stories/`:
- `stories-01-dom-{slug}.md` — Domingo: 2 stories (17:00 e 21:00)
- `stories-02-seg-{slug}.md` — Segunda: 5 stories (07:30, 11:00, 15:00, 19:00 e 22:00)
- `stories-03-ter-{slug}.md` — Terça: 5 stories (07:30, 11:00, 15:00, 19:00 e 22:00)
- `stories-04-qua-{slug}.md` — Quarta: 5 stories (07:30, 11:00, 15:00, 19:00 e 22:00)
- `stories-05-qui-{slug}.md` — Quinta: 5 stories (07:30, 11:00, 15:00, 19:00 e 22:00)
- `stories-06-sex-{slug}.md` — Sexta: 5 stories (07:30, 11:00, 15:00, 19:00 e 22:00)
- `stories-07-sab-{slug}.md` — Sábado: 3 stories (11:00, 15:00 e 19:00)
- `stories-semana-{slug}.html` — HTML visual agrupando todos os stories da semana

---

## Estrutura de cada story

Cada story deve ter obrigatoriamente:
- **Horário:** quando publicar
- **Tipo:** categoria editorial
- **Texto:** o que escrever/falar no story (direto, curto, sem enrolação)
- **Sticker obrigatório:** qual sticker usar e como configurar
- **CTA:** ação esperada do seguidor
- **Erro fatal:** o que nunca fazer neste story

---

## Padrão Seg–Sex (Bloco 1)

Aplicar este padrão para Segunda, Terça, Quarta, Quinta e Sexta. O conteúdo de cada story deve referenciar o post e o reel publicados naquele dia específico.

| Horário | Tipo | Objetivo | Duração | Sticker Obrigatório | CTA Direcionado | Erro Fatal |
|---------|------|----------|---------|---------------------|-----------------|------------|
| 07:30 | TEASER | Levar view pro Reel do dia | 5-10s | Enquete "Vi / Vendo agora" | Micro-compromisso 1 clique — leva pro Reel | Mostrar conteúdo do Reel. Só teaser |
| 11:00 | EDUCAÇÃO | Dar micro-vitória útil | 10-15s | Salvar + Caixinha | "Salva pra usar depois" ou "Qual sua trava?" | Aula de 60s. Ninguém segura |
| 15:00 | BASTIDOR | Humanizar + gerar DM | 10-15s | Hora + Localização | Pergunta pessoal: "Quantas horas você dedica a X?" | Bastidor fake/estoque |
| 19:00 | PROVA | Quebrar objeção | 10-15s | Caixinha "Quer igual?" | Auto-identificação: "Escreve EU" | Print sem autorização |
| 22:00 | CTA | Fechar para ação | 10-15s | Link + Contador + Enquete | Regra 3U: Prazo + Vagas + Perda | CTA genérico "link na bio" |

**Regras do Bloco 1:**
- O story de **07:30** teaser o Reel do dia — nunca entrega o conteúdo, apenas cria curiosidade para assistir
- O story de **11:00** entrega um insight prático extraído do post do dia — máximo 2 frases
- O story de **15:00** mostra bastidor real — nada encenado ou de estoque
- O story de **19:00** usa print real de resultado ou comentário de seguidor — nunca sem autorização
- O story de **22:00** aplica a Regra 3U: mencionar prazo, vagas ou perda concreta — nunca CTA genérico

**Sexta-feira:** o story de 22:00 deve reforçar a isca digital — usar a mesma palavra do CTA registrada em `lead-magnet-ideas.md`.

---

## Padrão Sábado (Bloco 2)

| Horário | Tipo | Conteúdo | Sticker | Motivo |
|---------|------|----------|---------|--------|
| 11:00 | TEASER | "Postei o resumo da semana" + seta para o Vídeo Feed (12:00) | Enquete "Já viu?" | Leva para o Vídeo de Fechamento |
| 15:00 | BASTIDOR | "Sábado de gravação. Preparando a semana que vem" | Hora + Quiz leve | Mostra trabalho. Não vende |
| 19:00 | PROVA LEVE | Print de comentário do vídeo: "Me ajudou muito" | Link bio + "Último dia" | Social proof sem forçar |

**Regras do Sábado:**
- O story de 11:00 direciona para o vídeo de fechamento da semana publicado no feed às 12:00
- O story de 15:00 é 100% bastidor — sem qualquer venda ou CTA direto
- O story de 19:00 usa apenas prints com autorização do seguidor

---

## Padrão Domingo (Bloco 3)

| Horário | Tipo | Conteúdo | Sticker | Motivo |
|---------|------|----------|---------|--------|
| 17:00 | TEASER REELS | "20h posto o que vai bombar semana que vem" | Contagem regressiva para 20h | Cria antecipação — +40% de views no Reel |
| 21:00 | PROVA + ANTECIPAÇÃO | "Semana passada X corretores. Semana que vem pode ser você" | Caixinha "Quer entrar?" | Domingo à noite = ansiedade. Sucesso Imóvel é a solução |

**Regras do Domingo:**
- O story de 17:00 usa contagem regressiva para o horário exato de publicação do Reel — gera antecipação real
- O story de 21:00 usa número específico obrigatório (ex: "23 corretores") — nunca "vários" ou "muitos"
- Nenhum story de domingo entrega conteúdo — ambos criam expectativa para a semana

---

## Output Format

### Arquivos Markdown (7 — um por dia)

```markdown
# Stories — {Dia da Semana} — {título do tema}

Data de publicação: {YYYY-MM-DD}
Dia: {Domingo / Segunda / ... / Sábado}
Post do dia: {nome do post referenciado — ex: Ter-PU1}
Reel do dia: {nome do reel referenciado — ex: 03-ter}

---

## Story 1 — {HH:MM} — {TIPO}

**Horário:** {HH:MM}
**Tipo:** {TEASER / EDUCAÇÃO / BASTIDOR / PROVA / CTA / etc.}
**Duração:** {5-10s / 10-15s}
**Texto:** {o que escrever ou falar — direto, sem enrolação}
**Sticker:** {qual sticker usar e como configurar}
**CTA:** {ação esperada do seguidor}
**Erro fatal:** {o que nunca fazer}

---

## Story 2 — {HH:MM} — {TIPO}
[...]
```

### HTML Unificado (`stories-semana-{slug}.html`)

Após gerar os 7 arquivos Markdown, gerar um único HTML auto-suficiente com todos os stories da semana. Design Premium Dark da Sucesso Imóvel.

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <title>Stories da Semana — {TÍTULO} | Sucesso Imóvel</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@700;800;900&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: 'Inter', sans-serif;
      background: linear-gradient(160deg, #0A0012 0%, #1A0A2E 45%, #0D0D0D 100%);
      min-height: 100vh; color: #FFFFFF; padding: 48px 24px;
    }
    .page-header {
      max-width: 1100px; margin: 0 auto 48px;
      padding-bottom: 28px; border-bottom: 1px solid rgba(255,255,255,0.08);
    }
    .page-header h1 { font-family: 'Montserrat', sans-serif; font-size: 24px; font-weight: 800; }
    .page-header .meta { font-size: 13px; color: rgba(255,255,255,0.4); margin-top: 6px; }
    .week-grid {
      max-width: 1100px; margin: 0 auto;
      display: grid; grid-template-columns: repeat(7, 1fr); gap: 16px;
    }
    .day-col { display: flex; flex-direction: column; gap: 12px; }
    .day-header {
      font-family: 'Montserrat', sans-serif; font-size: 11px; font-weight: 800;
      color: #A855F7; text-transform: uppercase; letter-spacing: 2px;
      padding-bottom: 8px; border-bottom: 2px solid rgba(168,85,247,0.3);
      margin-bottom: 4px;
    }
    .story-card {
      background: rgba(255,255,255,0.04); border: 1px solid rgba(255,255,255,0.07);
      border-radius: 12px; padding: 14px; display: flex; flex-direction: column; gap: 8px;
    }
    .story-time {
      font-size: 11px; font-weight: 700; color: #A855F7; font-family: 'Montserrat', sans-serif;
    }
    .story-type {
      display: inline-block; font-size: 9px; font-weight: 700;
      text-transform: uppercase; letter-spacing: 1px;
      padding: 2px 8px; border-radius: 100px;
      background: rgba(168,85,247,0.15); color: rgba(168,85,247,0.9);
    }
    .story-type.teaser    { background: rgba(251,191,36,0.12); color: rgba(251,191,36,0.9); }
    .story-type.educacao  { background: rgba(52,211,153,0.12); color: rgba(52,211,153,0.9); }
    .story-type.bastidor  { background: rgba(96,165,250,0.12); color: rgba(96,165,250,0.9); }
    .story-type.prova     { background: rgba(244,114,182,0.12); color: rgba(244,114,182,0.9); }
    .story-type.cta       { background: rgba(168,85,247,0.18); color: #A855F7; }
    .story-text { font-size: 12px; line-height: 1.6; color: rgba(255,255,255,0.82); }
    .story-sticker {
      font-size: 11px; color: rgba(255,255,255,0.45);
      border-top: 1px solid rgba(255,255,255,0.06); padding-top: 8px; margin-top: 4px;
    }
    .story-cta {
      font-size: 11px; font-weight: 600; color: rgba(168,85,247,0.8);
    }
    .story-error {
      font-size: 10px; color: rgba(239,68,68,0.7); font-style: italic;
    }
  </style>
</head>
<body>

  <div class="page-header">
    <div class="meta">Stories da Semana · Sucesso Imóvel</div>
    <h1>{TÍTULO DO TEMA}</h1>
    <div class="meta">Semana de {DATA DE INÍCIO} a {DATA DE FIM}</div>
  </div>

  <div class="week-grid">

    {PARA CADA DIA (Dom, Seg, Ter, Qua, Qui, Sex, Sáb):
    <div class="day-col">
      <div class="day-header">{ABREVIAÇÃO DO DIA} · {DATA}</div>

      {PARA CADA STORY DO DIA:
      <div class="story-card">
        <div style="display:flex; align-items:center; gap:8px;">
          <span class="story-time">{HH:MM}</span>
          <span class="story-type {tipo-css}">{TIPO}</span>
        </div>
        <div class="story-text">{TEXTO DO STORY}</div>
        <div class="story-sticker">Sticker: {STICKER}</div>
        <div class="story-cta">CTA: {CTA}</div>
        <div class="story-error">Erro fatal: {ERRO FATAL}</div>
      </div>
      }

    </div>
    }

  </div>

</body>
</html>
```

**Classes de cor por tipo:** `teaser` (amarelo), `educacao` (verde), `bastidor` (azul), `prova` (rosa), `cta` (roxo).

Salvar em `output/{run-id}/Stories/stories-semana-{slug}.html`.

## Quality Criteria

- [ ] 7 arquivos gerados — um por dia da semana
- [ ] Dom: 2 stories (17:00 e 21:00)
- [ ] Seg a Sex: 5 stories por dia (07:30, 11:00, 15:00, 19:00 e 22:00)
- [ ] Sáb: 3 stories (11:00, 15:00 e 19:00)
- [ ] Cada story tem: horário, tipo, texto, sticker, CTA e erro fatal
- [ ] Stories de 07:30 (Seg-Sex) são teasers do reel do dia — nunca entregam o conteúdo
- [ ] Story de Dom 21:00 tem número específico — nunca "vários" ou "muitos"
- [ ] Story de Sex 22:00 referencia a isca digital com a palavra do CTA de `lead-magnet-ideas.md`
- [ ] Stories de Sáb 15:00 e Dom sem qualquer venda ou CTA direto
- [ ] Nenhum print de terceiro sem indicação de autorização
- [ ] `stories-semana-{slug}.html` gerado com todos os dias e stories em layout semanal
- [ ] HTML com cores corretas por tipo de story (teaser=amarelo, educação=verde, bastidor=azul, prova=rosa, cta=roxo)
- [ ] Todos os arquivos salvos em `output/{run-id}/Stories/`

## Veto Conditions

1. Número de stories por dia diferente do definido (Dom: 2, Seg-Sex: 5, Sáb: 3)
2. Story de 07:30 entrega conteúdo do reel — deve ser apenas teaser
3. Story de Dom 21:00 sem número específico ("vários corretores" é proibido)
4. Story de Sex 22:00 sem referência à isca digital
5. Story de bastidor com conteúdo encenado ou de estoque
6. Print de terceiro sem indicação de autorização
7. CTA de 22:00 genérico sem aplicar Regra 3U (prazo, vagas ou perda)
8. HTML unificado ausente ou com dias/stories faltando
9. Arquivos salvos fora da pasta `Stories/`

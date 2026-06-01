---
type: agent
agent: yago-video
execution: subagent
inputFile: squads/youtube-to-instagram/output/youtube-focus.md
outputFile: squads/youtube-to-instagram/output/{run-id}/v1/youtube-analysis.md
model_tier: powerful
run_id_slug: true
---

# Step 03: Yago Vídeo — Análise do Conteúdo

Yago Vídeo analisa o conteúdo do vídeo (YouTube ou local transcrito) e produz um relatório completo em dois formatos: Markdown (`youtube-analysis.md`) e HTML visual (`youtube-analysis.html`).

## Context Loading

Antes de iniciar, Yago deve carregar:
- `squads/youtube-to-instagram/output/youtube-focus.md` — fonte do vídeo e foco informados pelo usuário
- `squads/youtube-to-instagram/output/video-transcript.md` — transcrição (se fonte local) ou marcador "none" (se YouTube)
- `squads/youtube-to-instagram/pipeline/data/research-brief.md` — Framework de análise YouTube→Instagram
- `squads/youtube-to-instagram/pipeline/data/domain-framework.md` — Classificação de conteúdo e design
- `_opensquad/_memory/company.md` — Perfil da Sucesso Imóvel para contextualizar a análise

## Instructions

### Analisar o Vídeo

1. Ler `output/youtube-focus.md` para verificar `source_type` (youtube ou local) e o foco informado.

**Se `source_type: youtube`:**
2. Usar `web_fetch` na URL do YouTube para obter: título, descrição, canal, duração, data de publicação.
3. Identificar os principais tópicos abordados no vídeo.

**Se `source_type: local`:**
2. Ler `output/video-transcript.md` para obter a transcrição completa do vídeo.
3. O título do vídeo será o `file_name` sem extensão (formatar de forma legível, ex: "minha-aula.mp4" → "Minha Aula").
4. Identificar os principais tópicos abordados com base na transcrição.

**Ambos os casos — produzir relatório completo com as seguintes seções:**

#### 1. Informações Básicas
Título, canal, duração, data de publicação, URL ou nome do arquivo.

#### 2. Tópicos Principais
Lista dos tópicos abordados no vídeo, com descrição de cada um e dados/afirmações rastreáveis.

#### 3. Pontos Positivos
O que o vídeo faz bem — clareza didática, exemplos práticos, autoridade demonstrada, linguagem adequada ao público, estrutura, ritmo, casos reais citados.

#### 4. Pontos Negativos / Lacunas
O que poderia ser melhor — tópicos superficiais, ausência de exemplos práticos, linguagem excessivamente técnica, falta de dados concretos, estrutura confusa, oportunidades não exploradas.

#### 5. Análise do Hook
Como o vídeo abre. O hook é eficaz para parar o scroll? Gera curiosidade ou incômodo imediato? Qual é a frase de abertura exata? Avaliação de 1-10 com justificativa.

#### 6. Insights-Chave para Corretores
Os 3 a 5 insights mais valiosos do vídeo para o público de corretores e imobiliárias — específicos, acionáveis e rastreáveis ao conteúdo.

#### 7. Melhores Trechos para Reaproveitamento
Citações ou momentos do vídeo com maior potencial de virar post, slide ou hook no Instagram. Indicar o trecho exato e por que funciona.

#### 8. Sugestões de Melhoria para o Vídeo
2 a 4 sugestões concretas para melhorar o próprio vídeo (estrutura, exemplos, dados, linguagem) — direcionadas ao Dr. Jeorge ou à equipe de produção.

#### 9. Fit com a Audiência da Sucesso Imóvel
Avaliação de aderência do conteúdo ao público-alvo (corretores e imobiliárias). O tema é relevante? A linguagem é adequada? O vídeo gera segurança jurídica ou apenas informação genérica?

Salvar o relatório completo em `output/{run-id}/v1/youtube-analysis.md`.

### Gerar HTML do Relatório

Após salvar o Markdown, gerar `output/{run-id}/v1/youtube-analysis.html` — documento HTML auto-suficiente com a identidade visual da Sucesso Imóvel (Premium Dark), apresentando todas as 8 seções do relatório de forma organizada e visualmente rica.

**Design:** fundo escuro (`#0A0012` → `#1A0A2E`), accent roxo (`#A855F7`), tipografia Montserrat + Inter via Google Fonts.

**Estrutura do HTML:**

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <title>Análise do Vídeo — {TÍTULO} | Sucesso Imóvel</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@700;800;900&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: 'Inter', sans-serif;
      background: linear-gradient(160deg, #0A0012 0%, #1A0A2E 45%, #0D0D0D 100%);
      min-height: 100vh; color: #FFFFFF; padding: 48px 24px;
    }
    .page-header {
      max-width: 960px; margin: 0 auto 48px;
      padding-bottom: 32px; border-bottom: 1px solid rgba(255,255,255,0.08);
    }
    .page-header h1 { font-family: 'Montserrat', sans-serif; font-size: 28px; font-weight: 800; }
    .page-header .meta { font-size: 14px; color: rgba(255,255,255,0.5); margin-top: 8px; }
    .accent { color: #A855F7; }
    .section-card {
      max-width: 960px; margin: 0 auto 24px;
      background: rgba(255,255,255,0.04);
      border: 1px solid rgba(168,85,247,0.15);
      border-radius: 16px; padding: 32px;
    }
    .section-title {
      font-family: 'Montserrat', sans-serif; font-size: 13px; font-weight: 700;
      color: #A855F7; text-transform: uppercase; letter-spacing: 1.5px;
      margin-bottom: 20px;
    }
    .section-body { font-size: 15px; line-height: 1.7; color: rgba(255,255,255,0.85); }
    .section-body ul { padding-left: 20px; }
    .section-body li { margin-bottom: 8px; }
    .hook-box {
      background: rgba(168,85,247,0.08); border-left: 3px solid #A855F7;
      border-radius: 8px; padding: 16px 20px; margin-bottom: 16px;
      font-style: italic; font-size: 16px;
    }
    .score-badge {
      display: inline-block; background: #A855F7;
      color: #fff; font-weight: 700; font-size: 13px;
      border-radius: 100px; padding: 4px 14px; margin-left: 12px;
    }
    .insight-item {
      background: rgba(255,255,255,0.03); border-radius: 10px;
      padding: 14px 18px; margin-bottom: 10px;
      border-left: 3px solid rgba(168,85,247,0.4);
    }
    .tag {
      display: inline-block; font-size: 11px; font-weight: 600;
      padding: 3px 10px; border-radius: 100px; margin-right: 6px;
      background: rgba(168,85,247,0.15); color: #A855F7;
    }
    .fit-bar {
      height: 6px; border-radius: 100px;
      background: linear-gradient(90deg, #7B2FBE, #A855F7);
      margin-top: 12px;
    }
  </style>
</head>
<body>

  <div class="page-header">
    <div>
      <div class="section-title">Relatório de Análise</div>
      <h1>{TÍTULO DO VÍDEO}</h1>
      <div class="meta">{CANAL} · {DURAÇÃO} · {DATA DE PUBLICAÇÃO} · Analisado em {DATA DA ANÁLISE}</div>
    </div>
  </div>

  <!-- Seção 1: Tópicos Principais -->
  <div class="section-card">
    <div class="section-title">1. Tópicos Principais</div>
    <div class="section-body">
      <ul>
        {LISTA DE TÓPICOS — <li> para cada tópico com descrição}
      </ul>
    </div>
  </div>

  <!-- Seção 2: Pontos Positivos -->
  <div class="section-card">
    <div class="section-title">2. Pontos Positivos</div>
    <div class="section-body">
      <ul>
        {LISTA DE PONTOS POSITIVOS COM JUSTIFICATIVA}
      </ul>
    </div>
  </div>

  <!-- Seção 3: Pontos Negativos / Lacunas -->
  <div class="section-card">
    <div class="section-title">3. Pontos Negativos / Lacunas</div>
    <div class="section-body">
      <ul>
        {LISTA DE PONTOS NEGATIVOS COM JUSTIFICATIVA}
      </ul>
    </div>
  </div>

  <!-- Seção 4: Análise do Hook -->
  <div class="section-card">
    <div class="section-title">4. Análise do Hook</div>
    <div class="section-body">
      <div class="hook-box">"{FRASE DE ABERTURA EXATA}"</div>
      <p>
        <strong>Avaliação:</strong>
        <span class="score-badge">{N}/10</span>
      </p>
      <p style="margin-top:12px;">{JUSTIFICATIVA}</p>
    </div>
  </div>

  <!-- Seção 5: Insights-Chave para Corretores -->
  <div class="section-card">
    <div class="section-title">5. Insights-Chave para Corretores</div>
    <div class="section-body">
      {PARA CADA INSIGHT: <div class="insight-item">{texto do insight}</div>}
    </div>
  </div>

  <!-- Seção 6: Melhores Trechos para Reaproveitamento -->
  <div class="section-card">
    <div class="section-title">6. Melhores Trechos para Reaproveitamento</div>
    <div class="section-body">
      {PARA CADA TRECHO:
        <div class="hook-box">"{citação exata}"</div>
        <p><strong>Por que funciona:</strong> {justificativa}</p>
      }
    </div>
  </div>

  <!-- Seção 7: Sugestões de Melhoria -->
  <div class="section-card">
    <div class="section-title">7. Sugestões de Melhoria para o Vídeo</div>
    <div class="section-body">
      <ul>
        {LISTA DE SUGESTÕES}
      </ul>
    </div>
  </div>

  <!-- Seção 8: Fit com a Audiência -->
  <div class="section-card">
    <div class="section-title">8. Fit com a Audiência da Sucesso Imóvel</div>
    <div class="section-body">
      <p>{AVALIAÇÃO DE ADERÊNCIA}</p>
      <div class="fit-bar" style="width: {PERCENTUAL DE FIT}%;"></div>
    </div>
  </div>

</body>
</html>
```

O HTML deve ser auto-suficiente — sem dependências externas além do Google Fonts. Salvar em `output/{run-id}/v1/youtube-analysis.html`.

## Output Format

```markdown
# Análise do Vídeo — {título do vídeo}

**Canal:** {canal}
**Duração:** {duração}
**Data:** {data de publicação}
**Fonte:** {URL ou nome do arquivo}
**Data da análise:** {YYYY-MM-DD}

---

## 1. Tópicos Principais

{lista com descrição de cada tópico e dados rastreáveis}

---

## 2. Pontos Positivos

{lista com justificativa para cada ponto}

---

## 3. Pontos Negativos / Lacunas

{lista com justificativa para cada ponto}

---

## 4. Análise do Hook

**Frase de abertura:** "{trecho exato}"
**Avaliação:** {N}/10
**Justificativa:** {1-2 frases}

---

## 5. Insights-Chave para Corretores

1. {insight específico e acionável}
2. {insight específico e acionável}
3. {insight específico e acionável}
[...]

---

## 6. Melhores Trechos para Reaproveitamento

**Trecho 1:** "{citação exata}"
**Por que funciona:** {justificativa}

[...]

---

## 7. Sugestões de Melhoria para o Vídeo

1. {sugestão concreta}
2. {sugestão concreta}
[...]

---

## 8. Fit com a Audiência da Sucesso Imóvel

{avaliação de aderência — linguagem, relevância, geração de segurança jurídica}
```

## Quality Criteria

- [ ] Todas as 8 seções presentes e preenchidas no Markdown
- [ ] Tópicos principais com dados rastreáveis ao vídeo
- [ ] Pontos positivos e negativos com justificativa específica — sem generalidades
- [ ] Hook avaliado com nota e justificativa
- [ ] Mínimo de 3 insights-chave para corretores
- [ ] Mínimo de 2 trechos para reaproveitamento com citação exata
- [ ] Mínimo de 2 sugestões de melhoria concretas
- [ ] `output/{run-id}/v1/youtube-analysis.md` salvo
- [ ] `output/{run-id}/v1/youtube-analysis.html` gerado com design Premium Dark
- [ ] HTML auto-suficiente — todas as 8 seções presentes no HTML

## Veto Conditions

1. Dado ou trecho não rastreável ao vídeo analisado — dado inventado é recusa automática
2. Qualquer das 8 seções ausente ou em branco (Markdown ou HTML)
3. Pontos positivos/negativos sem justificativa específica ("o vídeo é bom" não é justificativa)
4. HTML com layout quebrado ou seções faltando
5. Arquivos salvos fora de `output/{run-id}/v1/`

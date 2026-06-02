---
type: agent
agent: iago-instagram
execution: inline
inputFile: squads/youtube-to-instagram/output/{run-id}/v1/youtube-analysis.md
outputFile: squads/youtube-to-instagram/output/{run-id}/Roteiros/
---

# Step 08: Iago Instagram — Criação dos Roteiros

Iago cria o roteiro de vídeo para YouTube com base no relatório de análise gerado no step 3. O roteiro deve incorporar as melhorias identificadas na análise — não é uma transcrição do vídeo original, mas uma versão aprimorada dele.

## Context Loading

Antes de iniciar, Iago deve carregar:
- `squads/youtube-to-instagram/output/{run-id}/v1/youtube-analysis.md` — Relatório completo da análise do vídeo (**fonte principal**)
- `_opensquad/_memory/company.md` — Perfil da Sucesso Imóvel

## Estrutura de Output

Um arquivo salvo em `output/{run-id}/Roteiros/`:
- `roteiro-youtube-{slug}.md` — Roteiro completo para YouTube

## Instructions

### Roteiro YouTube

**Antes de escrever, ler obrigatoriamente do relatório `youtube-analysis.md`:**
- **Seção 3 — Pontos Negativos / Lacunas:** cada ponto negativo identificado deve ser corrigido ou suprimido no roteiro
- **Seção 7 — Sugestões de Melhoria:** aplicar todas as sugestões como diretrizes de escrita
- **Seção 5 — Insights-Chave para Corretores:** usar como base para o desenvolvimento do conteúdo
- **Seção 6 — Melhores Trechos para Reaproveitamento:** aproveitar os trechos indicados e aprimorá-los onde necessário
- **Seção 4 — Análise do Hook:** se a nota for inferior a 7, criar um hook mais forte para a abertura do roteiro

O roteiro é uma versão **aprimorada** do vídeo original — não uma transcrição. Deve manter o tema e os pontos fortes, corrigir as lacunas e incorporar todas as melhorias identificadas.

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

## Output Format

Dois arquivos em `output/{run-id}/Roteiros/`:

**Arquivo 1:** `roteiro-youtube-{slug}.md`
```markdown
# Roteiro YouTube — {Título}

**Duração estimada:** X a Y minutos
**Público-alvo:** {público}
**Referência legal:** {leis/artigos}
**Tom:** {tom}

## Melhorias Aplicadas
{lista das melhorias da análise incorporadas neste roteiro — uma linha por melhoria}

---

[estrutura do roteiro]

---

## REFERÊNCIAS LEGAIS
[lista de artigos citados]

## DESCRIÇÃO DO VÍDEO (YouTube)
[descrição completa com capítulos]
```

**Arquivo 2:** `roteiro-youtube-{slug}.html`

HTML auto-suficiente com a identidade visual da Sucesso Imóvel (Premium Dark). Design: fundo escuro (`#0A0012` → `#1A0A2E`), accent roxo (`#A855F7`), tipografia Montserrat + Inter via Google Fonts.

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <title>Roteiro YouTube — {TÍTULO} | Sucesso Imóvel</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@700;800;900&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: 'Inter', sans-serif;
      background: linear-gradient(160deg, #0A0012 0%, #1A0A2E 45%, #0D0D0D 100%);
      min-height: 100vh; color: #FFFFFF; padding: 48px 24px;
    }
    .page-header {
      max-width: 900px; margin: 0 auto 48px;
      padding-bottom: 32px; border-bottom: 1px solid rgba(255,255,255,0.08);
    }
    .page-header h1 { font-family: 'Montserrat', sans-serif; font-size: 26px; font-weight: 800; }
    .page-header .meta { font-size: 13px; color: rgba(255,255,255,0.45); margin-top: 8px; }
    .accent { color: #A855F7; }
    .melhorias {
      max-width: 900px; margin: 0 auto 32px;
      background: rgba(168,85,247,0.07); border: 1px solid rgba(168,85,247,0.2);
      border-radius: 12px; padding: 24px 28px;
    }
    .melhorias-title {
      font-size: 11px; font-weight: 700; color: #A855F7;
      text-transform: uppercase; letter-spacing: 1.5px; margin-bottom: 12px;
    }
    .melhorias ul { padding-left: 18px; }
    .melhorias li { font-size: 14px; color: rgba(255,255,255,0.75); margin-bottom: 6px; }
    .bloco {
      max-width: 900px; margin: 0 auto 20px;
      background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07);
      border-radius: 14px; overflow: hidden;
    }
    .bloco-header {
      background: rgba(168,85,247,0.1); padding: 14px 24px;
      display: flex; align-items: center; gap: 14px;
      border-bottom: 1px solid rgba(168,85,247,0.15);
    }
    .bloco-num {
      background: #A855F7; color: #fff; font-family: 'Montserrat', sans-serif;
      font-size: 12px; font-weight: 800; border-radius: 100px;
      padding: 4px 12px; white-space: nowrap;
    }
    .bloco-name { font-family: 'Montserrat', sans-serif; font-size: 14px; font-weight: 700; }
    .bloco-duration { font-size: 12px; color: rgba(255,255,255,0.4); margin-left: auto; }
    .bloco-camera {
      padding: 10px 24px; font-size: 11px; font-weight: 600;
      color: rgba(168,85,247,0.7); text-transform: uppercase; letter-spacing: 1px;
      border-bottom: 1px solid rgba(255,255,255,0.04);
    }
    .bloco-body { padding: 20px 24px; font-size: 15px; line-height: 1.75; color: rgba(255,255,255,0.82); }
    .referencias {
      max-width: 900px; margin: 32px auto 20px;
      background: rgba(255,255,255,0.03); border-radius: 14px; padding: 24px 28px;
    }
    .referencias-title {
      font-size: 11px; font-weight: 700; color: rgba(255,255,255,0.4);
      text-transform: uppercase; letter-spacing: 1.5px; margin-bottom: 14px;
    }
    .referencias ul { padding-left: 18px; }
    .referencias li { font-size: 14px; color: rgba(255,255,255,0.65); margin-bottom: 6px; }
    .descricao {
      max-width: 900px; margin: 0 auto 48px;
      background: rgba(255,255,255,0.03); border-radius: 14px; padding: 24px 28px;
    }
    .descricao pre {
      font-family: 'Inter', monospace; font-size: 13px;
      color: rgba(255,255,255,0.65); white-space: pre-wrap; line-height: 1.7;
    }
  </style>
</head>
<body>

  <div class="page-header">
    <div class="meta">Roteiro YouTube · Sucesso Imóvel</div>
    <h1>{TÍTULO DO VÍDEO}</h1>
    <div class="meta">{PÚBLICO-ALVO} · {DURAÇÃO ESTIMADA} · {TOM}</div>
  </div>

  <!-- Melhorias Aplicadas -->
  <div class="melhorias">
    <div class="melhorias-title">Melhorias Aplicadas</div>
    <ul>
      {PARA CADA MELHORIA: <li>{texto da melhoria}</li>}
    </ul>
  </div>

  <!-- Blocos do Roteiro -->
  {PARA CADA BLOCO:
  <div class="bloco">
    <div class="bloco-header">
      <span class="bloco-num">BLOCO {N}</span>
      <span class="bloco-name">{NOME DO BLOCO}</span>
      <span class="bloco-duration">{mm:ss – mm:ss}</span>
    </div>
    <div class="bloco-camera">{INDICAÇÃO DE CÂMERA / ÂNGULO}</div>
    <div class="bloco-body">{TEXTO DO ROTEIRO}</div>
  </div>
  }

  <!-- Referências Legais -->
  <div class="referencias">
    <div class="referencias-title">Referências Legais</div>
    <ul>
      {PARA CADA REFERÊNCIA: <li>{artigo / lei}</li>}
    </ul>
  </div>

  <!-- Descrição YouTube -->
  <div class="descricao">
    <div class="referencias-title">Descrição do Vídeo (YouTube)</div>
    <pre>{DESCRIÇÃO COMPLETA COM CAPÍTULOS}</pre>
  </div>

</body>
</html>
```

## Quality Criteria

- [ ] Seções 3, 5, 6 e 7 do relatório de análise foram lidas antes de escrever
- [ ] Todas as sugestões de melhoria da Seção 7 foram incorporadas ou justificadamente descartadas
- [ ] Pontos negativos da Seção 3 estão corrigidos ou suprimidos no roteiro
- [ ] Seção "Melhorias Aplicadas" preenchida no MD e no HTML
- [ ] Hook da abertura tem nota >= 7 — se o original era inferior, foi reescrito
- [ ] Roteiro cobre todos os subtópicos relevantes do tema, sem exceder 20 min
- [ ] Inclui referências legais e descrição com capítulos
- [ ] `roteiro-youtube-{slug}.md` salvo em `output/{run-id}/Roteiros/`
- [ ] `roteiro-youtube-{slug}.html` salvo em `output/{run-id}/Roteiros/`
- [ ] HTML auto-suficiente com design Premium Dark — todos os blocos presentes
- [ ] **ZERO emojis** em qualquer parte do roteiro (MD e HTML)

## Veto Conditions

1. Roteiro sem hook na abertura
2. Sugestões de melhoria da análise ignoradas sem justificativa
3. Pontos negativos identificados na análise presentes no roteiro sem correção
4. Seção "Melhorias Aplicadas" ausente ou em branco (MD ou HTML)
5. Dado não rastreável ao vídeo analisado ou ao Código Civil
6. Arquivos salvos fora da pasta `Roteiros/`
7. Roteiro sem referências legais citadas
8. HTML com blocos faltando ou layout quebrado
9. **Qualquer emoji encontrado em qualquer parte do roteiro**

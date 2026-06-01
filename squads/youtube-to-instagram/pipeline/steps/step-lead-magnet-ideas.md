---
type: agent
agent: yago-video
execution: subagent
inputFile: squads/youtube-to-instagram/output/{run-id}/v1/youtube-analysis.md
outputFile: squads/youtube-to-instagram/output/{run-id}/lead-magnet-ideas.md
model_tier: powerful
---

# Step: Yago Vídeo — Ideias de Isca Digital

Yago lê o relatório de análise do vídeo e propõe exatamente 3 ideias de isca digital relacionadas ao tema principal. O usuário aprova 1 ideia no próximo checkpoint para criação.

## Context Loading

Antes de iniciar, Yago deve carregar:
- `squads/youtube-to-instagram/output/{run-id}/v1/youtube-analysis.md` — Relatório completo da análise do vídeo (**fonte principal**)
- `_opensquad/_memory/company.md` — Perfil da Sucesso Imóvel

## Instructions

Com base nos tópicos, insights-chave e pontos de maior valor do relatório de análise, propor **3 ideias distintas de isca digital** para o tema do vídeo.

Cada isca deve:
- Ser diretamente rastreável ao conteúdo do vídeo
- Ter valor prático imediato para o corretor de imóveis
- Ser entregável via mensagem direta (DM) após comentário no Reel Viral
- Ser referenciada genericamente no CTA do Reel (ex: "o checklist", "o guia", "o modelo") — o título real é definido aqui

**Formatos possíveis de isca digital:**
- Checklist — lista de verificação acionável (ex: "Checklist de documentos para contrato de C&V")
- Guia — explicação prática de um processo ou conceito (ex: "Guia de cláusulas obrigatórias no contrato")
- Modelo — template preenchível (ex: "Modelo de notificação extrajudicial")
- Mini-guia — versão compacta de 1-2 páginas com o essencial
- Glossário — termos jurídicos do tema explicados de forma simples

Para cada ideia, definir:
- **Título:** nome completo e específico da isca
- **Formato:** tipo de documento (checklist, guia, modelo, etc.)
- **Conteúdo proposto:** lista dos tópicos ou seções que o documento deve ter
- **Palavra do CTA:** a 1 palavra em CAPS que o seguidor deve comentar para receber (ex: CONTRATO, PRAZO, CLÁUSULA)
- **Por que funciona:** justificativa de valor para o corretor — específica ao tema do vídeo

Salvar as 3 ideias em `output/{run-id}/lead-magnet-ideas.md`.

## Output Format

```markdown
# Ideias de Isca Digital — {título do vídeo}

Baseado em: output/{run-id}/v1/youtube-analysis.md
Data: {YYYY-MM-DD}

---

## Isca 1 — {Título}

**Formato:** {checklist / guia / modelo / mini-guia / glossário}
**Palavra do CTA:** {PALAVRA}
**Conteúdo proposto:**
- {tópico ou seção 1}
- {tópico ou seção 2}
- {tópico ou seção 3}
[...]
**Por que funciona:** {justificativa 1-2 frases — específica ao tema}

---

## Isca 2 — {Título}

**Formato:** {tipo}
**Palavra do CTA:** {PALAVRA}
**Conteúdo proposto:**
- {tópico ou seção 1}
[...]
**Por que funciona:** {justificativa}

---

## Isca 3 — {Título}

**Formato:** {tipo}
**Palavra do CTA:** {PALAVRA}
**Conteúdo proposto:**
- {tópico ou seção 1}
[...]
**Por que funciona:** {justificativa}
```

## Quality Criteria

- [ ] Exatamente 3 ideias geradas
- [ ] Cada ideia tem: título, formato, palavra do CTA, conteúdo proposto e justificativa
- [ ] As 3 palavras de CTA são diferentes entre si
- [ ] Cada ideia aborda o tema por um ângulo distinto — nenhuma repete o mesmo foco
- [ ] Todo conteúdo rastreável ao relatório de análise — sem inventar tópicos fora do tema
- [ ] Formatos variados — não usar o mesmo formato nas 3 ideias
- [ ] `output/{run-id}/lead-magnet-ideas.md` salvo antes de encerrar

## Veto Conditions

1. Menos ou mais de 3 ideias geradas
2. Duas ideias com a mesma palavra de CTA
3. Conteúdo proposto não rastreável ao tema do vídeo
4. Justificativa genérica sem relação específica ao conteúdo do vídeo

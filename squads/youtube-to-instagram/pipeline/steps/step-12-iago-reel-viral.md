---
type: agent
agent: iago-instagram
execution: inline
inputFile: squads/youtube-to-instagram/output/Posts/post-content.md
outputFile: squads/youtube-to-instagram/output/{run-id}/Roteiros/
---

# Step 12: Iago Instagram — Roteiros de Reels Virais

Iago cria 6 roteiros de Reel Viral — um por dia de publicação (Dom, Seg, Ter, Qua, Qui, Sex). Cada roteiro usa a estrutura de 7 blocos obrigatórios e deriva seu ângulo do post correspondente ao dia.

## Context Loading

Antes de iniciar, Iago deve carregar:
- `squads/youtube-to-instagram/output/{run-id}/Posts/post-content.md` — Conteúdo dos posts (fonte de ângulo para Ter, Qua, Qui e Sex)
- `squads/youtube-to-instagram/output/{run-id}/v1/youtube-analysis.md` — Análise do vídeo original (fonte de ângulo para Seg)
- `squads/youtube-to-instagram/output/{run-id}/lead-magnet-ideas.md` — Isca digital aprovada (**obrigatório para o Sex-Reel — extrair título e palavra do CTA**)
- `squads/youtube-to-instagram/pipeline/data/tone-of-voice.md` — Guia de tons de voz
- `squads/youtube-to-instagram/pipeline/data/hashtags.md` — Lista oficial de hashtags
- `_opensquad/_memory/company.md` — Perfil da Sucesso Imóvel

## Estrutura de Output

Sete arquivos salvos em `output/{run-id}/Roteiros/`:
- `roteiro-reel-viral-01-dom-{slug}.md` — Dom: teaser semanal — apresentação do tema
- `roteiro-reel-viral-02-seg-{slug}.md` — Seg: tema principal abrangente
- `roteiro-reel-viral-03-ter-{slug}.md` — Ter: derivado do Ter-PU1
- `roteiro-reel-viral-04-qua-{slug}.md` — Qua: derivado do Qua-PU2
- `roteiro-reel-viral-05-qui-{slug}.md` — Qui: derivado do Qui-PU3
- `roteiro-reel-viral-06-sex-{slug}.md` — Sex: isca digital — incentivar download do material
- `roteiros-reels-virais-{slug}.html` — HTML visual agrupando todos os 6 roteiros

## Ângulos por Reel

| Reel | Fonte | Ângulo | Objetivo específico |
|------|-------|--------|---------------------|
| Dom-Reel | `youtube-analysis.md` — tema central + títulos dos posts | Teaser semanal — apresentação do tema sem aprofundar | Despertar curiosidade máxima para os próximos posts da semana |
| Seg-Reel | `youtube-analysis.md` — tema central do vídeo | Abordagem abrangente do tema principal | Cobrir o tema de forma completa |
| Ter-Reel | `post-content.md` — seção Ter-PU1 | Tema central / ponto principal do post | Aprofundar o ângulo editorial do Ter-PU1 |
| Qua-Reel | `post-content.md` — seção Qua-PU2 | Impacto e consequência — o "e agora?" | Aprofundar o ângulo editorial do Qua-PU2 |
| Qui-Reel | `post-content.md` — seção Qui-PU3 | Reflexão e princípio — o "por que isso importa" | Aprofundar o ângulo editorial do Qui-PU3 |
| Sex-Reel | `lead-magnet-ideas.md` — isca digital aprovada | Isca digital — apresentar o valor do material e incentivar download | Fazer o seguidor comentar [PALAVRA] para receber a isca |

Cada reel tem ângulo distinto. Não repetir o mesmo gancho, polêmica ou prova entre os 6 roteiros.

### Regras específicas do Dom-Reel

O Dom-Reel é um teaser — sua única missão é fazer o seguidor querer assistir o conteúdo da semana toda.

- **Bloco 1 — Gancho:** nomear o tema da semana de forma intrigante, sem revelar a resposta
- **Bloco 2 — Dor:** mostrar brevemente o problema que o tema resolve para o corretor
- **Bloco 3 — Polêmica/Quebra:** uma afirmação contraintuitiva sobre o tema que gera dúvida — não resolver, apenas plantar
- **Bloco 4 — Prova:** indicar que o conteúdo da semana vem com embasamento real (documento, lei, caso)
- **Bloco 5 — Vulnerabilidade:** relato curto do Dr. Jeorge sobre como o tema aparece no dia a dia dos corretores
- **Bloco 6 — CTA:** "Comenta [PALAVRA] que você recebe o conteúdo completo" — a isca digital aqui é o próprio calendário semanal de posts
- **Bloco 7 — Saída:** corte seco
- **Regra de ouro:** o Dom-Reel não pode resolver nenhuma dúvida — só criar. Qualquer slide ou fala que entregue a resposta deve ser reescrito.

### Regras específicas do Sex-Reel

O Sex-Reel tem uma única missão: fazer o seguidor comentar a palavra do CTA para receber a isca digital.

- **Antes de escrever:** ler `lead-magnet-ideas.md` e extrair o título da isca e a **palavra do CTA** — usar exatamente essa palavra no Bloco 6. Não inventar outra.
- **Bloco 1 — Gancho:** apresentar o problema que a isca resolve — dor financeira ou risco jurídico real para o corretor
- **Bloco 2 — Dor:** detalhar a situação específica que o material ajuda a resolver — mostrar documento, contrato ou print
- **Bloco 3 — Polêmica/Quebra:** confrontar a crença de que o corretor "não precisa" do material (ex: "Corretor que improvisa X Corretor que tem o documento certo")
- **Bloco 4 — Prova:** mostrar o que o material contém — um trecho visual do PDF, lista de tópicos ou estrutura do checklist
- **Bloco 5 — Vulnerabilidade:** relato do Dr. Jeorge sobre corretores que teriam se beneficiado do material — número específico obrigatório
- **Bloco 6 — CTA:** "Comenta [PALAVRA] aqui embaixo e te mando o [referência genérica ao material]" — PALAVRA extraída de `lead-magnet-ideas.md`
- **Bloco 7 — Saída:** corte seco
- **Regra de ouro:** a PALAVRA do CTA deve ser idêntica à registrada em `lead-magnet-ideas.md` e à usada no Sex-CCTA. Consistência entre reel e post é obrigatória.

## Prompt de Criação

Usar exatamente o seguinte prompt para criar o roteiro:

---

Você é roteirista especialista em Reels de alta retenção para o nicho de direito imobiliário. Público-alvo: corretores de imóveis e imobiliárias no Brasil, que fecham negócios no dia a dia e precisam de segurança jurídica para proteger suas comissões e reputação.

TAREFA: Crie um roteiro de Reel com alto potencial de viralização seguindo EXATAMENTE esta estrutura. Não mude a ordem. Não pule etapas.

CONTEXTO: Você já sabe o TEMA do vídeo (extraído da análise do YouTube). Foque só na estrutura. O porta-voz é o Dr. Jeorge, advogado especialista em direito imobiliário, que fala diretamente para a câmera com autoridade e linguagem acessível.

DURAÇÃO: Defina o tempo ideal para o tema, respeitando o limite de 45 segundos. Informe a duração escolhida no início do roteiro.

ESTRUTURA OBRIGATÓRIA - 7 BLOCOS:

1. GANCHO 0-3s
   Objetivo: Parar o scroll. Usar 1 destes 4 gatilhos:
   [Polêmica que quebra crença do corretor] | [Dor financeira específica] | [Número chocante do mercado imobiliário] | [Pergunta sim/não]
   Formato:
   - FALA: frase curta, máx 7 palavras
   - TEXTO NA TELA: a mesma frase em CAPS
   - AÇÃO: expressão facial de impacto ou gesto direto para câmera
   Regra: Se não gerar curiosidade ou incômodo em 2s, reescreve.

2. DOR 3-7s
   Objetivo: Provar que o gancho é real para o corretor.
   Usar: [Situação de venda travada] | [Erro comum em contrato] | [Dado do mercado imobiliário]
   Formato:
   - FALA: contextualiza a dor do corretor
   - TEXTO NA TELA: dado ou situação em destaque
   - AÇÃO: mostra documento, trecho de contrato ou print de caso real
   Regra: Sem prova visual, retenção cai 40%. Sempre mostra algo.

3. POLÊMICA/QUEBRA 7-11s
   Objetivo: Criar comentário. Confrontar uma crença comum do corretor.
   Exemplos de estrutura:
   "Contrato bonito X Contrato válido" | "Corretor intermediador X Corretor assessor" | "Você assina X. O risco fica com Y"
   Formato:
   - FALA: frase de embate curta e direta
   - TEXTO NA TELA: [A] vs [B] em destaque
   - AÇÃO: gesto com as mãos comparando os dois lados
   Regra: Tem que dividir opinião. Se todo mundo concorda, não viraliza.

4. PROVA 11-18s
   Objetivo: Mostrar autoridade jurídica real, não só discurso.
   Formato:
   - FALA: ex: "O corretor que entende isso fecha sem dor de cabeça"
   - TEXTO NA TELA: 2s de prova visual — trecho de contrato com cláusula destacada, print de jurisprudência ou documento real
   - AÇÃO: aponta para o documento ou tela com o caso
   Regra: 2s de prova prática valem 20s de discurso. Sem isso é só opinião.

5. VULNERABILIDADE 18-23s
   Objetivo: Conexão humana. Algoritmo prioriza conteúdo real.
   Formato:
   - FALA: relato curto do Dr. Jeorge com número específico — ex: "Já atendi X corretores que perderam a comissão por isso"
   - TEXTO NA TELA: NÚMERO + RESULTADO (ex: "12 CORRETORES > COMISSÃO PERDIDA")
   - AÇÃO: expressão séria, tom de alerta genuíno
   Regra: Número específico obrigatório. "Vários casos" não conecta. "11 casos em 2024" conecta.

6. CTA 23-28s (ou até 40s conforme duração definida)
   Objetivo: Engajamento máximo + entrega de isca digital.
   Formato:
   - FALA: "Quer [descrição genérica do PDF]? Comenta [PALAVRA]"
   - TEXTO NA TELA: COMENTA: [PALAVRA] 👇
   - AÇÃO: aponta para baixo
   Regra:
   - A PALAVRA deve ser 1 única palavra em CAPS relacionada ao tema do vídeo
   - O PDF é referenciado genericamente (ex: "o checklist", "o guia", "o modelo") — não inventar título específico
   - Sem "link na bio". Sem "arrasta pra cima". Apenas "comenta X"

7. SAÍDA
   Corte seco imediatamente após o CTA. Sem despedida. Sem "até mais".

FORMATO DE ENTREGA:

Duração definida: Xs

[BLOCO 1 — GANCHO]
FALA: ...
TEXTO NA TELA: ...
AÇÃO: ...

[BLOCO 2 — DOR]
FALA: ...
TEXTO NA TELA: ...
AÇÃO: ...

[BLOCO 3 — POLÊMICA/QUEBRA]
FALA: ...
TEXTO NA TELA: ...
AÇÃO: ...

[BLOCO 4 — PROVA]
FALA: ...
TEXTO NA TELA: ...
AÇÃO: ...

[BLOCO 5 — VULNERABILIDADE]
FALA: ...
TEXTO NA TELA: ...
AÇÃO: ...

[BLOCO 6 — CTA]
FALA: ...
TEXTO NA TELA: ...
AÇÃO: ...

[BLOCO 7 — SAÍDA]
Corte seco.

LEGENDA:
{hook do reel — primeiros 125 chars}
{corpo curto contextualizando o tema}
{CTA: "Comenta [PALAVRA] aqui embaixo"}
{hashtags da lista oficial}

REGRAS GERAIS:
- ZERO emojis no texto do roteiro (exceto o 👇 no CTA)
- Linguagem B2B — o público é o corretor, nunca o comprador do imóvel
- Todo conteúdo deve ser rastreável ao vídeo analisado — sem inventar dados ou casos
- Tom: autoridade acessível — Dr. Jeorge fala como parceiro estratégico, não como professor

---

## Output Format

### Arquivos Markdown (6 — um por dia)

Salvar cada roteiro em `output/{run-id}/Roteiros/` com o seguinte template:

```markdown
# Roteiro Reel Viral — {01-Dom / 02-Seg / 03-Ter / 04-Qua / 05-Qui} — {título do tema}

Data: {YYYY-MM-DD}
Dia: {01-Dom / 02-Seg / 03-Ter / 04-Qua / 05-Qui}
Ângulo: {descrição do ângulo derivado do post correspondente}
Duração definida: Xs
Palavra do CTA: {PALAVRA}

---

[BLOCO 1 — GANCHO]
FALA: ...
TEXTO NA TELA: ...
AÇÃO: ...

[BLOCO 2 — DOR]
FALA: ...
TEXTO NA TELA: ...
AÇÃO: ...

[BLOCO 3 — POLÊMICA/QUEBRA]
FALA: ...
TEXTO NA TELA: ...
AÇÃO: ...

[BLOCO 4 — PROVA]
FALA: ...
TEXTO NA TELA: ...
AÇÃO: ...

[BLOCO 5 — VULNERABILIDADE]
FALA: ...
TEXTO NA TELA: ...
AÇÃO: ...

[BLOCO 6 — CTA]
FALA: ...
TEXTO NA TELA: ...
AÇÃO: ...

[BLOCO 7 — SAÍDA]
Corte seco.

---

## Legenda
{legenda completa}

## Hashtags
{hashtags da lista oficial}
```

### HTML Unificado (`roteiros-reels-virais-{slug}.html`)

Após gerar os 6 Markdown, gerar um HTML auto-suficiente agrupando todos os roteiros. Design Premium Dark da Sucesso Imóvel.

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <title>Roteiros Reels Virais — {TÍTULO} | Sucesso Imóvel</title>
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
      padding-bottom: 28px; border-bottom: 1px solid rgba(255,255,255,0.08);
    }
    .page-header h1 { font-family: 'Montserrat', sans-serif; font-size: 24px; font-weight: 800; }
    .page-header .meta { font-size: 13px; color: rgba(255,255,255,0.4); margin-top: 6px; }

    /* Reel container */
    .reel-section {
      max-width: 960px; margin: 0 auto 40px;
      border: 1px solid rgba(168,85,247,0.2); border-radius: 16px; overflow: hidden;
    }
    .reel-header {
      background: rgba(168,85,247,0.12); padding: 20px 28px;
      display: flex; align-items: center; gap: 16px;
      border-bottom: 1px solid rgba(168,85,247,0.2);
    }
    .reel-day {
      font-family: 'Montserrat', sans-serif; font-size: 11px; font-weight: 800;
      color: #A855F7; text-transform: uppercase; letter-spacing: 2px;
      background: rgba(168,85,247,0.15); padding: 4px 12px; border-radius: 100px;
    }
    .reel-title { font-family: 'Montserrat', sans-serif; font-size: 16px; font-weight: 700; }
    .reel-meta { font-size: 12px; color: rgba(255,255,255,0.4); margin-left: auto; }

    /* Blocos */
    .blocos-grid {
      display: grid; grid-template-columns: repeat(3, 1fr);
      gap: 0; padding: 0;
    }
    .bloco {
      padding: 20px 24px;
      border-right: 1px solid rgba(255,255,255,0.05);
      border-bottom: 1px solid rgba(255,255,255,0.05);
    }
    .bloco:nth-child(3n) { border-right: none; }
    .bloco-label {
      font-size: 10px; font-weight: 700; color: #A855F7;
      text-transform: uppercase; letter-spacing: 1.5px; margin-bottom: 12px;
    }
    .bloco-field { margin-bottom: 10px; }
    .bloco-field-name {
      font-size: 10px; font-weight: 600; color: rgba(255,255,255,0.35);
      text-transform: uppercase; letter-spacing: 1px; margin-bottom: 4px;
    }
    .bloco-field-value { font-size: 13px; line-height: 1.6; color: rgba(255,255,255,0.82); }

    /* Legenda */
    .reel-footer { padding: 20px 28px; background: rgba(255,255,255,0.02); }
    .reel-footer-label {
      font-size: 10px; font-weight: 700; color: rgba(255,255,255,0.35);
      text-transform: uppercase; letter-spacing: 1px; margin-bottom: 8px;
    }
    .reel-legenda { font-size: 13px; line-height: 1.7; color: rgba(255,255,255,0.7); }
    .cta-word {
      display: inline-block; background: rgba(168,85,247,0.2);
      color: #A855F7; font-weight: 700; font-size: 12px;
      padding: 3px 10px; border-radius: 100px; margin-left: 8px;
    }
  </style>
</head>
<body>

  <div class="page-header">
    <div class="meta">Roteiros Reels Virais · Sucesso Imóvel</div>
    <h1>{TÍTULO DO TEMA}</h1>
    <div class="meta">6 roteiros · {DATA}</div>
  </div>

  {PARA CADA ROTEIRO (01-Dom a 06-Sex):
  <div class="reel-section">
    <div class="reel-header">
      <span class="reel-day">{01-Dom / 02-Seg / ...}</span>
      <span class="reel-title">{TÍTULO DO ROTEIRO}</span>
      <span class="reel-meta">{DURAÇÃO}s · CTA: <span class="cta-word">{PALAVRA}</span></span>
    </div>

    <div class="blocos-grid">
      {PARA CADA BLOCO 1-7:
      <div class="bloco">
        <div class="bloco-label">Bloco {N} — {NOME}</div>
        <div class="bloco-field">
          <div class="bloco-field-name">Fala</div>
          <div class="bloco-field-value">{FALA}</div>
        </div>
        <div class="bloco-field">
          <div class="bloco-field-name">Texto na Tela</div>
          <div class="bloco-field-value">{TEXTO NA TELA}</div>
        </div>
        <div class="bloco-field">
          <div class="bloco-field-name">Ação</div>
          <div class="bloco-field-value">{AÇÃO}</div>
        </div>
      </div>
      }
    </div>

    <div class="reel-footer">
      <div class="reel-footer-label">Legenda</div>
      <div class="reel-legenda">{LEGENDA COMPLETA}</div>
    </div>
  </div>
  }

</body>
</html>
```

Salvar em `output/{run-id}/Roteiros/roteiros-reels-virais-{slug}.html`.

## Quality Criteria

- [ ] 6 roteiros criados — Dom, Seg, Ter, Qua, Qui e Sex
- [ ] Cada roteiro tem ângulo distinto derivado da fonte correta (análise, post ou isca digital)
- [ ] Nenhum gancho, polêmica ou prova se repete entre os 6 roteiros
- [ ] Dom-Reel não resolve nenhuma dúvida — apenas cria curiosidade para a semana
- [ ] Sex-Reel: palavra do CTA idêntica à registrada em `lead-magnet-ideas.md` e à usada no Sex-CCTA
- [ ] Duração definida e informada no início de cada roteiro (máx 45s)
- [ ] 7 blocos presentes na ordem correta em cada roteiro — nenhum pulado
- [ ] Bloco 1: fala com máx 7 palavras + texto em CAPS
- [ ] Bloco 2: prova visual descrita (documento, contrato, print)
- [ ] Bloco 3: confronto A vs B que divide opinião
- [ ] Bloco 4: prova prática de autoridade jurídica (2s de visual)
- [ ] Bloco 5: número específico obrigatório no relato
- [ ] Bloco 6: 1 palavra em CAPS + referência genérica ao PDF + 👇
- [ ] Bloco 7: corte seco — sem despedida
- [ ] Legenda com hook nos primeiros 125 chars em cada roteiro
- [ ] Hashtags da lista oficial em cada roteiro
- [ ] ZERO emojis (exceto 👇 no CTA)
- [ ] Todo conteúdo rastreável ao vídeo analisado, ao post correspondente ou à isca digital
- [ ] `roteiros-reels-virais-{slug}.html` gerado com todos os 6 roteiros e blocos completos
- [ ] 7 arquivos salvos em `output/{run-id}/Roteiros/` (6 MD + 1 HTML)

## Veto Conditions

1. Menos de 6 roteiros gerados
2. Dois roteiros com o mesmo gancho ou polêmica
3. Dom-Reel entrega resposta ou resolve dúvida — deve apenas criar curiosidade
4. Ter-Reel não derivado do conteúdo do Ter-PU1
5. Qua-Reel não derivado do conteúdo do Qua-PU2
6. Qui-Reel não derivado do conteúdo do Qui-PU3
7. Sex-Reel usa palavra do CTA diferente da registrada em `lead-magnet-ideas.md`
8. CTA com mais de 1 palavra-chave em qualquer roteiro
9. CTA menciona "link na bio" ou "arrasta pra cima"
10. Bloco 5 sem número específico ("vários casos" é proibido)
11. Qualquer bloco fora de ordem ou ausente
12. Duração definida acima de 45 segundos
13. Dado ou caso não rastreável ao vídeo, ao post ou à isca correspondente
14. Qualquer emoji fora do 👇 do CTA
15. HTML unificado ausente ou com roteiros/blocos faltando

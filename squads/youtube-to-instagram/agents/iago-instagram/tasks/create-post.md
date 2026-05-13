---
task: "Create Post"
order: 1
input: |
  - approved_ideas: Ideias aprovadas pelo usuário (arquivo approved-ideas.md)
  - tone_of_voice: Guia de tons disponíveis (tone-of-voice.md)
  - company_context: Perfil da Sucesso Imóvel (company.md)
output: |
  - post_content: Estrutura completa de slides, legenda e hashtags para cada post aprovado
---

# Create Post

Transforma as ideias aprovadas pelo usuário em posts completos para o Instagram. Primeiro recomenda o tom de voz, depois apresenta 3 opções de hook, aguarda escolha, e só então escreve o post completo com estrutura de slides (carrossel) ou texto visual (post único), legenda e hashtags.

## Process

1. Ler as ideias aprovadas em `approved-ideas.md`.
2. Ler `tone-of-voice.md` e `_opensquad/_memory/company.md`.
3. Para cada ideia aprovada:
   a. Recomendar o tom de voz mais adequado ao conteúdo (citando o nome do tom do guia). Aguardar aprovação do usuário.
   b. Redigir 3 hooks com ângulos diferentes: Hook A (urgência/alerta), Hook B (dado/especificidade), Hook C (pergunta/curiosidade). Aguardar escolha.
   c. Com o hook escolhido como âncora, escrever o post completo:
      - **Carrossel:** Slide por slide. Cada slide com: Headline, Supporting text (40-80 palavras total), indicação de fundo (escuro/destaque roxo/padrão), Accent keywords.
      - **Post único:** Headline principal, subtítulo/supporting text.
   d. Escrever a legenda completa: hook (primeiros 125 chars), corpo (2-3 parágrafos curtos), pergunta de engajamento, CTA específico.
   e. Selecionar 8-12 hashtags: 3-4 de nicho (#direitoimobiliario, #consultoriajuridica) + 3-4 médio alcance (#corretor, #imobiliaria) + 2-3 amplo (#imoveis, #mercadoimobiliario).
4. Salvar todo o conteúdo em `post-content.md`.

## Output Format

```markdown
# Conteúdo do Post — {titulo_da_ideia}

**Tom selecionado:** {nome_do_tom}
**Hook escolhido:** Hook {A/B/C}
**Formato:** Carrossel / Post único
**Estrutura:** {nome_da_estrutura}

---

## Slides

### Slide 1 (Cover)
**Eyebrow:** {categoria_em_uppercase}
**Headline:** {titulo_impactante — max 15 palavras}
**Tag lateral:** {tag_de_categoria}
**Background:** Gradiente roxo-preto Premium Dark

### Slide 2
**Headline:** {headline_bold}
**Supporting text:** {texto_de_apoio_40_a_80_palavras}
**Accent keywords:** {palavras_para_destacar_em_roxo}
**Background:** {escuro_padrao / destaque_roxo / card_translucido}

...slides 3 a N...

### Slide N (CTA)
**Headline:** {chamada_para_acao}
**Supporting text:** {contexto_breve_e_beneficio}
**CTA:** {acao_especifica}
**Background:** Gradiente roxo-preto

---

## Legenda

{hook_nos_primeiros_125_chars}

{corpo_paragrafo_1}

{corpo_paragrafo_2}

{pergunta_de_engajamento}

{cta_especifico}

---

## Hashtags

#hashtag1 #hashtag2 #hashtag3 ... (8-12 total)
```

## Output Example

```markdown
# Conteúdo do Post — 4 cláusulas que corretores esquecem — e que podem custar a comissão

**Tom selecionado:** Alerta e Urgência
**Hook escolhido:** Hook A
**Formato:** Carrossel
**Estrutura:** Listicle (8 slides)

---

## Slides

### Slide 1 (Cover)
**Eyebrow:** CONTRATOS IMOBILIÁRIOS
**Headline:** 4 cláusulas que corretores esquecem — e que podem custar a comissão
**Tag lateral:** Jurídico
**Background:** Gradiente roxo-preto Premium Dark

### Slide 2
**Headline:** Cláusula 1: Arrependimento sem multa definida
**Supporting text:** Sem esta cláusula, o comprador pode desistir a qualquer momento sem pagar nada. O corretor, que já investiu tempo, visitas e negociação, fica sem comissão e sem amparo jurídico para cobrar. A cláusula deve definir: prazo para exercer o arrependimento e percentual de multa sobre o valor do negócio.
**Accent keywords:** "sem pagar nada", "sem amparo jurídico"
**Background:** Escuro padrão

### Slide 3
**Headline:** Cláusula 2: ITBI — quem paga não está definido
**Supporting text:** A lei atribui o ITBI ao comprador, mas o contrato pode prever divisão diferente. Quando o documento é omisso, cada parte interpreta à sua maneira — e o impasse aparece na hora do fechamento em cartório, travando o negócio que já estava fechado.
**Accent keywords:** "travando o negócio"
**Background:** Card translúcido roxo

### Slide 4
**Headline:** Cláusula 3: Procuração sem poderes específicos para o imóvel
**Supporting text:** Procuração geral não vale para alienação de imóvel. O instrumento precisa especificar: endereço completo, número da matrícula no registro de imóveis e poderes expressos para assinar escritura e receber o preço. Um erro aqui e o tabelionato recusa o ato — negócio desfeito por burocracia evitável.
**Accent keywords:** "recusa o ato"
**Background:** Escuro padrão

### Slide 5
**Headline:** Cláusula 4: Prazo de entrega sem penalidade por atraso
**Supporting text:** Construtoras e vendedores precisam de prazo com multa atrelada ao descumprimento. Sem penalidade definida, o comprador prejudicado busca indenização na Justiça — e o corretor que intermediou pode ser acionado como testemunha ou, em casos extremos, responsável solidário.
**Accent keywords:** "responsável solidário"
**Background:** Escuro padrão

### Slide 6 (Síntese)
**Headline:** Contrato mal feito custa mais do que honorários jurídicos
**Supporting text:** Cada cláusula ausente é um risco latente. O problema não é a má-fé das partes — é a ausência de previsão para quando as coisas não saem como planejado. E quando isso acontece, é o corretor que responde primeiro.
**Accent keywords:** "responde primeiro"
**Background:** Card translúcido roxo

### Slide 7 (CTA)
**Headline:** Seus contratos têm essas cláusulas?
**Supporting text:** A Sucesso Imóvel revisa contratos imobiliários e orienta corretores e imobiliárias sobre documentação e riscos jurídicos. Primeira consulta gratuita.
**CTA:** Comenta CONTRATO aqui embaixo
**Background:** Gradiente roxo-preto

---

## Legenda

Você fecha o contrato. O cliente some. E você fica sem receber.

Isso acontece mais do que parece — e quase sempre é culpa de cláusulas que faltaram, não de má-fé.

O contrato é o único documento que te protege quando o negócio azeda. E quem não preenche os buracos certos paga o preço depois.

Arraste e veja as 4 que mais causam problema.

Qual desses erros você já viu acontecer na prática? Comenta aqui.

Comenta CONTRATO e eu te mando um checklist gratuito das cláusulas essenciais.

---

## Hashtags

#direitoimobiliario #consultoriajuridica #corretor #contratocompravenda #corretordeimoveis #mercadoimobiliario #imobiliaria #documentacaoimobiliaria #juridicoimobiliario #sucessoimovel #clausulascontratuais #assessoriajuridica
```

## Quality Criteria

- [ ] Tom recomendado e aprovado antes de escrever
- [ ] 3 hooks apresentados; usuário escolheu um antes do post ser escrito
- [ ] Carrossel: mínimo 6, máximo 10 slides
- [ ] Cada slide: headline + supporting text com 40-80 palavras combinadas
- [ ] Accent keywords identificadas em cada slide
- [ ] Legenda: hook nos primeiros 125 caracteres
- [ ] Legenda: pergunta de engajamento + CTA específico
- [ ] Hashtags: 8-12, mix de nicho / médio / amplo

## Veto Conditions

Rejeitar e refazer se QUALQUER condição for verdadeira:
1. Algum slide tem menos de 40 palavras combinadas (headline + supporting text)
2. A legenda não tem CTA específico (CTA genérico como "curta e siga" conta como ausente)

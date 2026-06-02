---
type: agent
agent: iago-instagram
execution: inline
inputFile: squads/youtube-to-instagram/output/{run-id}/lead-magnet-ideas.md
outputFile: squads/youtube-to-instagram/output/{run-id}/Lead-Magnets/
---

# Step 06: Iago Instagram — Criação da Isca Digital

Iago cria o conteúdo completo da isca digital aprovada pelo usuário no checkpoint anterior. Gera um único arquivo Markdown com o documento completo, pronto para ser formatado em PDF.

## Context Loading

Antes de iniciar, Iago deve carregar:
- `squads/youtube-to-instagram/output/{run-id}/lead-magnet-ideas.md` — Ideias aprovadas pelo usuário
- `squads/youtube-to-instagram/output/{run-id}/v1/youtube-analysis.md` — Relatório da análise do vídeo (fonte de conteúdo)
- `_opensquad/_memory/company.md` — Perfil da Sucesso Imóvel

## Instructions

1. Ler `lead-magnet-ideas.md` e identificar qual isca foi aprovada pelo usuário no checkpoint.
2. Criar o conteúdo completo da isca aprovada seguindo as diretrizes abaixo.
3. Salvar em `output/{run-id}/Lead-Magnets/`.

### Diretrizes de criação

**Tom e linguagem:**
- Linguagem direta, acessível e prática — o corretor deve conseguir aplicar o conteúdo imediatamente
- Autoridade jurídica sem excesso de jargão — usar termos técnicos quando necessário, sempre explicados
- B2B intransigente — cada linha escrita para o corretor ou imobiliária, nunca para o comprador final
- ZERO emojis em qualquer parte do documento

**Estrutura por formato:**

**Checklist:**
- Título principal + subtítulo descritivo
- Introdução de 2-3 frases explicando o objetivo e como usar
- Itens agrupados por categoria (se aplicável)
- Cada item: ação clara + explicação breve do por que é importante
- Rodapé: "Documento elaborado pela Sucesso Imóvel — especialistas em direito imobiliário"

**Guia:**
- Título principal + subtítulo descritivo
- Introdução: problema que o guia resolve (1 parágrafo)
- Seções numeradas com headline + conteúdo explicativo
- Exemplos práticos do cotidiano do corretor em cada seção relevante
- Conclusão: síntese + próximo passo prático
- Rodapé: "Documento elaborado pela Sucesso Imóvel — especialistas em direito imobiliário"

**Modelo:**
- Título principal + instrução de uso
- Campos preenchíveis claramente indicados (ex: [NOME DO VENDEDOR], [DATA])
- Notas explicativas sobre cláusulas ou campos críticos
- Aviso legal no rodapé: "Este modelo é orientativo. Consulte um advogado especializado para adequação ao seu caso."
- Rodapé: "Documento elaborado pela Sucesso Imóvel — especialistas em direito imobiliário"

**Mini-guia:**
- Mesma estrutura do Guia, limitado a 1-2 páginas de conteúdo
- Foco no essencial — sem aprofundamentos, apenas o que o corretor precisa saber e fazer

**Glossário:**
- Título principal + instrução de uso
- Termos em ordem alfabética
- Cada termo: definição clara em linguagem acessível + aplicação prática para o corretor

## Output Format

Salvar em `output/{run-id}/Lead-Magnets/`:

**Arquivo:** `lead-magnet-{palavra-cta}-{slug}.md`

```markdown
# {Título completo da isca}

**Formato:** {tipo}
**Palavra do CTA:** {PALAVRA}
**Tema:** {tema do vídeo}
**Data:** {YYYY-MM-DD}
**Elaborado por:** Sucesso Imóvel — especialistas em direito imobiliário

---

{conteúdo completo do documento — seguindo a estrutura do formato aprovado}

---

*Documento elaborado pela Sucesso Imóvel — especialistas em direito imobiliário.*
*Este material é de uso exclusivo do destinatário. Para dúvidas jurídicas específicas, consulte nossa equipe.*
```

## Quality Criteria

- [ ] Um único arquivo gerado para a isca digital aprovada
- [ ] Conteúdo 100% rastreável ao tema do vídeo — sem inventar dados ou cláusulas
- [ ] Estrutura correta para o formato aprovado (checklist, guia, modelo, etc.)
- [ ] Linguagem B2B — direcionada ao corretor, nunca ao comprador
- [ ] Rodapé com menção à Sucesso Imóvel em todos os documentos
- [ ] ZERO emojis em qualquer parte dos documentos
- [ ] Arquivos nomeados com prefixo `lead-magnet-{palavra-cta}-`
- [ ] Todos os arquivos salvos em `output/{run-id}/Lead-Magnets/`

## Veto Conditions

1. Conteúdo inventado ou não rastreável ao tema do vídeo
2. Linguagem direcionada ao comprador final (deve ser sempre para o corretor)
3. Documento sem menção à Sucesso Imóvel no rodapé
4. Formato diferente do aprovado pelo usuário
5. Qualquer emoji encontrado
6. Arquivos salvos fora da pasta `Lead-Magnets/`

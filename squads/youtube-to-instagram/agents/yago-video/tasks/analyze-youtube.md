---
task: "Analyze YouTube"
order: 1
input: |
  - youtube_url: URL do vídeo do YouTube a ser analisado
output: |
  - video_title: Título do vídeo
  - channel: Nome do canal
  - description: Descrição completa extraída
  - topics: Lista de tópicos identificados (3-7 itens)
  - insights: Insights relevantes para corretores e imobiliárias
  - data_points: Dados, estatísticas ou números citados no vídeo (se houver)
---

# Analyze YouTube

Acessa o vídeo do YouTube informado e extrai todo o conteúdo disponível via WebFetch: título, canal, descrição, tópicos e dados. Identifica os pontos de maior relevância para corretores e imobiliárias no mercado imobiliário jurídico.

## Process

1. Ler a URL do YouTube em `squads/youtube-to-instagram/output/youtube-focus.md`.
2. Executar WebFetch na URL do YouTube. Extrair do HTML: título da página, nome do canal, descrição completa do vídeo, tags e qualquer transcrição disponível.
3. Identificar os 3-7 tópicos principais abordados no vídeo, com base na descrição e no título.
4. Filtrar pelos tópicos mais relevantes para o público B2B da Sucesso Imóvel: erros em contratos, documentação, tributação imobiliária (ITBI, IPTU), processos jurídicos, riscos para o corretor.
5. Extrair dados e estatísticas citados explicitamente no vídeo (números, percentuais, prazos).
6. Registrar apenas o que está presente no conteúdo do vídeo — sem inferências ou adições externas.

## Output Format

```markdown
# Análise do Vídeo YouTube

**URL:** {url}
**Título:** {titulo}
**Canal:** {canal}

## Descrição
{descricao_completa}

## Tópicos Identificados
1. {topico_1}
2. {topico_2}
3. {topico_3}
...

## Insights para Corretores
- {insight_1}: {descricao_breve}
- {insight_2}: {descricao_breve}
...

## Dados e Estatísticas (somente do vídeo)
- {dado_1}
- {dado_2}
(Deixar em branco se o vídeo não contém dados explícitos)
```

## Output Example

```markdown
# Análise do Vídeo YouTube

**URL:** https://youtube.com/watch?v=abc123
**Título:** Os erros mais comuns em contratos de compra e venda — Dr. Ricardo Alves
**Canal:** Direito Imobiliário Prático

## Descrição
Neste vídeo, o Dr. Ricardo Alves aborda os principais erros cometidos por corretores e imobiliárias na elaboração e revisão de contratos de compra e venda de imóveis. São discutidos: cláusula de arrependimento, responsabilidade pelo ITBI, procuração com poderes específicos e prazo de entrega com penalidade. O vídeo é voltado para profissionais do setor imobiliário que querem reduzir riscos jurídicos em suas transações.

## Tópicos Identificados
1. Cláusula de arrependimento — multa por desistência
2. Responsabilidade pelo ITBI (Imposto sobre Transmissão de Bens Imóveis)
3. Procuração: necessidade de poderes específicos para alienação de imóvel
4. Prazo de entrega e cláusula de penalidade por atraso
5. Vício de consentimento em contratos de adesão

## Insights para Corretores
- Cláusula de arrependimento: sem ela, o comprador pode desistir sem pagar multa, deixando o corretor sem comissão e sem amparo jurídico
- ITBI: a responsabilidade é do adquirente por lei, mas o contrato pode prever divisão diferente — omissão cria conflito no fechamento
- Procuração geral não vale para venda de imóvel: precisa especificar matrícula e poderes de alienação
- Prazo de entrega sem penalidade abre espaço para litígio e pode tornar o corretor responsável solidário

## Dados e Estatísticas (somente do vídeo)
- Segundo o Dr. Ricardo Alves, mais de 60% dos contratos analisados em sua prática carecem de pelo menos uma cláusula essencial
- Litígios por contrato mal elaborado têm prazo médio de resolução de 2 a 4 anos na Justiça do Rio de Janeiro
```

## Quality Criteria

- [ ] URL lida corretamente do arquivo de input
- [ ] Título e canal extraídos com precisão
- [ ] Tópicos refletem o conteúdo real do vídeo (não inferências)
- [ ] Insights são filtrados para relevância B2B (corretor/imobiliária)
- [ ] Dados e estatísticas marcados como "somente do vídeo" e deixados em branco se ausentes
- [ ] Nenhuma informação adicionada que não esteja presente no conteúdo extraído

## Veto Conditions

Rejeitar e refazer se QUALQUER condição for verdadeira:
1. A análise contém dado ou estatística não presente no conteúdo extraído do vídeo
2. Os tópicos identificados não correspondem ao conteúdo do vídeo (foram inferidos ou inventados)

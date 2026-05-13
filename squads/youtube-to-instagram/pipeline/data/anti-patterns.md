# Anti-Patterns — YouTube → Instagram

## Análise de Vídeo (Yago Vídeo)

### Nunca fazer
1. **Inventar dados ou estatísticas** — Se o número não está no vídeo, não existe para esse post. Credibilidade destruída em um único post falso.
2. **Ignorar o contexto B2B** — O público é corretor e imobiliária. Insights voltados ao comprador final não servem para esse squad.
3. **Sugerir mais de 5 ideias** — Excesso de opções paralisa a decisão. Máximo 5 ideias bem definidas por vídeo.
4. **Misturar temas de vídeos diferentes** — Cada run analisa um único vídeo. Não contaminar com conteúdo de memória de runs anteriores.

### Sempre fazer
1. **Basear cada ideia em um insight real do vídeo** — Citar qual trecho ou ponto do vídeo originou a ideia.
2. **Classificar o formato correto** — Listas e processos pedem carrossel; afirmações fortes e dados únicos pedem post único.
3. **Adaptar o ângulo ao tom da marca** — Consultivo e confiável, não sensacionalista.

---

## Criação de Conteúdo (Iago Instagram)

### Nunca fazer
1. **Começar a legenda com "Neste post vou falar sobre"** — Meta-comentário desperdiça o espaço mais valioso. O hook deve ser a afirmação, não o aviso.
2. **Slides com menos de 40 palavras** — Conteúdo raso não entrega valor. O algoritmo prioriza saves, e ninguém salva o óbvio.
3. **Usar "incrível", "dica rápida", "conteúdo imperdível"** — Superlativa vaga reduz autoridade. Específico sempre vence genérico.
4. **Mais de 15 hashtags** — Sinaliza spam para o algoritmo do Instagram. Prejudica o alcance orgânico.
5. **Falar "você comprador" em vez de "você corretor"** — O público é profissional B2B. Linguagem ao consumidor final quebra a conexão.
6. **CTA genérico como "curtam e sigam"** — CTA fraco gera engajamento fraco. Sempre especificar a ação: "Comenta CONTRATO", "Salva pra consultar", "Manda pra um colega".

### Sempre fazer
1. **Hook nos primeiros 125 caracteres** — É o que aparece antes do "ver mais". Se não prender aqui, não prende em lugar nenhum.
2. **Pergunta de engajamento no final da legenda** — Encerrar com pergunta aberta aumenta comentários e sinaliza valor para o algoritmo.
3. **Ao menos um dado específico por carrossel** — Número, percentual, prazo ou valor tornam o conteúdo crível e compartilhável.

---

## Design Visual (Diego Design)

### Nunca fazer
1. **Font size abaixo de 34px para body text** — Ilegível no mobile. O Instagram é consumido majoritariamente em telas pequenas.
2. **Contadores de slide nas imagens (ex: "3/7")** — O Instagram já exibe navegação nativa. Adicionar contador é ruído visual desnecessário.
3. **Dependências externas além de Google Fonts** — Bootstrap, CDN de ícones, JavaScript quebram o rendering no Playwright sem aviso.
4. **Fundo claro ou branco como principal** — Viola a identidade visual Premium Dark aprovada. Roxo-preto escuro é a base obrigatória.
5. **height: auto no body** — Quebra o layout fixo. O body sempre precisa de width: 1080px e height: 1440px explícitos.
6. **Pular a verificação do primeiro slide** — Erro no slide 1 se replica para todos. Verificar antes de renderizar o batch é obrigatório.

### Sempre fazer
1. **Header consistente em todos os slides** — Badge SI + nome Sucesso Imóvel + tag de categoria. É o elemento de branding que conecta os slides.
2. **Accent line no topo** — O gradiente roxo fino no topo é a assinatura visual do template. Deve estar em todos os slides.
3. **Footer em todos exceto o último** — "ARRASTE →" em roxo orienta a navegação. Último slide substitui por CTA específico do post.

---

## Revisão (Renata Revisão)

### Nunca fazer
1. **Aprovar sem ler o conteúdo completo** — Revisar é mais do que checar formato. Ler cada slide e a legenda inteira é obrigatório.
2. **Dar feedback vago como "o tom está errado"** — Feedback sem local e sem exemplo específico não pode ser executado. Apontar slide, frase e correção.
3. **Ignorar a aderência ao vídeo original** — O conteúdo deve derivar do vídeo informado. Dados inventados são rejeição automática.

### Sempre fazer
1. **Citar o slide ou trecho específico em cada feedback** — "Slide 3: supporting text repete o headline sem adicionar informação nova."
2. **Separar required changes de sugestões não-bloqueantes** — O criador precisa saber o que é obrigatório corrigir vs. o que é opcional melhorar.
3. **Reconhecer pelo menos um ponto positivo mesmo em rejeição** — Feedback construtivo acelera a iteração.

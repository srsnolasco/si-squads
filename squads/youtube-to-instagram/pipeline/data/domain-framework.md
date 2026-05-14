# Domain Framework — YouTube → Instagram

## Fluxo completo de transformação

```
YouTube Link
     ↓
[Análise] Extrair título, descrição, tópicos, insights do vídeo
     ↓
[Ideação] Gerar 3-5 ideias de posts com formato e ângulo
     ↓
[Seleção] Usuário aprova as ideias que quer desenvolver
     ↓
[Criação] Iago escreve conteúdo completo (slides + legenda + hashtags)
     ↓
[Aprovação] Usuário aprova o texto antes das imagens
     ↓
[Design] Diego cria os slides HTML e renderiza as imagens
     ↓
[Revisão] Renata avalia qualidade e emite veredito
     ↓
[Aprovação final] Usuário revisa e libera para publicação
```

---

## Framework de Análise de Conteúdo YouTube

### O que extrair de cada vídeo
1. **Título e canal** — Define o nicho e o nível técnico do conteúdo
2. **Descrição** — Frequentemente contém os tópicos principais, timestamps e referências
3. **Tópicos identificados** — Os 3-5 pontos mais relevantes do vídeo para o público (corretores)
4. **Dados e estatísticas** — Números citados no vídeo que podem anchorar posts de autoridade
5. **Processos e passos** — Sequências que se traduzem bem em carrosséis tutoriais
6. **Mitos ou erros comuns** — Pontos onde o vídeo desafia crenças do mercado

### Classificação de formato por tipo de insight
| Tipo de insight | Formato recomendado | Estrutura de carrossel |
|----------------|-------------------|----------------------|
| Lista de erros / riscos | Carrossel Listicle | Um erro por slide + consequência |
| Dado ou estatística impactante | Post único ou Editorial | Dado em destaque + contexto |
| Processo passo a passo | Carrossel Tutorial | Um passo por slide |
| Mito vs Realidade | Carrossel Mito vs Realidade | Par mito/realidade por slide |
| Afirmação de autoridade forte | Post único | Headline + subtítulo |
| Análise de mercado | Carrossel Editorial/Tese | Tese → argumentos → síntese |

---

## Framework de Criação de Conteúdo (Iago Instagram)

### Diagnóstico pré-escrita (obrigatório)
1. **Nível de consciência do público:** corretores são Solution Aware — sabem que têm problemas jurídicos, querem soluções concretas
2. **Driver psicológico dominante:** Segurança (proteger o negócio) + Controle (conhecer as regras do jogo)
3. **Big Idea:** qual crença do mercado esse post desafia ou confirma?
4. **Framework de copy:** PAS (erros/riscos) ou BAB (antes/depois da consultoria) ou Listicle (lista de itens)

### Estrutura de carrossel
- **Slide 1 (capa):** Hook visual + título impactante. Primeiro 1,5 segundo decide se o usuário swipa.
- **Slides 2-N (corpo):** Um ponto por slide. Headline em destaque + supporting text explicando/contextualizando.
- **Último slide (CTA):** Ação específica para o corretor tomar agora.

### Estrutura da legenda
- **Primeiros 125 chars:** Hook autossuficiente — funciona como post separado
- **Corpo:** Expandir o contexto do carrossel, adicionar uma camada de insight
- **Pergunta final:** Aberta, que o corretor vai querer responder ou salvar
- **CTA:** Ação específica ("Comenta CONTRATO", "Manda pra um colega corretor")
- **Hashtags:** 8-12, variadas, no final da legenda ou primeiro comentário

---

## Framework de Design Visual (Diego Design)

### Sistema de design — Template C Premium Dark
1. **Fundo:** Gradiente roxo-preto `linear-gradient(160deg, #0A0012, #1A0A2E 45%, #0D0D0D)`
2. **Accent line:** 3px no topo, gradiente roxo
3. **Header:** Badge SI (ícone 56px, border-radius 12px) + nome + tag de categoria
4. **Glow effects:** Radial gradient roxo no canto superior direito e inferior esquerdo
5. **Cards:** Background rgba(255,255,255,0.04) com borda roxa semitransparente
6. **Footer:** Dot gradiente + @sucessoimovel + "ARRASTE →" em roxo (exceto último slide)
7. **Tipografia:** Montserrat 900 para títulos, Inter 500-800 para corpo

### Paleta de cores
- Roxo principal: #7B2FBE
- Roxo médio: #A855F7
- Roxo claro (gradient): #D4A0FF
- Preto base: #0D0D0D
- Preto profundo: #0A0012
- Cinza texto secundário: #9B9B9B
- Cinza muted: #6B6B6B
- Branco: #FFFFFF

### Processo de rendering
1. Ler conteúdo dos slides em post-content.md
2. Criar um HTML por slide (slide-01.html, slide-02.html...)
3. Iniciar HTTP server em output/Posts/
4. Renderizar slide-01 e verificar visualmente
5. Renderizar restantes
6. Parar HTTP server

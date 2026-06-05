---
type: checkpoint
run_id_slug: true
outputFile: squads/youtube-to-instagram/output/{run-id}/v1/youtube-focus.md
---

# Step 01: Seleção de Vídeo

Bem-vindo ao squad **YouTube → Instagram** da Sucesso Imóvel.

Este squad transforma um vídeo em um calendário semanal completo para o Instagram: 5 posts (2 carrosséis + 3 posts únicos), isca digital em PDF, roteiro YouTube, 6 roteiros de Reels virais, 7 roteiros de Stories diários e um dashboard semanal.

**Como funciona:**
1. Você seleciona a origem do conteúdo (vídeo local, URL do YouTube ou documento de texto)
2. O squad transcreve/extrai e analisa o conteúdo, gerando um relatório completo
3. Você aprova a isca digital e as ideias de posts
4. O squad cria todo o conteúdo da semana e gera as imagens
5. Você revisa o resultado final e recebe o dashboard semanal

---

## Instruções para o Runner

### 1. Listar fontes disponíveis

Verificar as duas pastas de origem:

```bash
ls squads/youtube-to-instagram/assets/videos-originais/ 2>/dev/null
ls squads/youtube-to-instagram/assets/documentos/ 2>/dev/null
```

- Vídeos: filtrar extensões `.mp4`, `.mov`, `.avi`, `.mkv`, `.webm`, `.m4v`
- Documentos: filtrar extensões `.pdf`, `.txt`, `.doc`, `.docx`, `.md`, `.html`

### 2. Perguntar ao usuário

Apresentar todas as fontes encontradas via AskUserQuestion, agrupadas por tipo:

- Uma opção para cada vídeo local encontrado
- Uma opção para cada documento encontrado
- Uma opção: "Informar URL do YouTube"
- Uma opção: "Ainda vou colocar o arquivo na pasta correta"

**Se o usuário escolher "Informar URL do YouTube":**
Peça a URL em uma segunda AskUserQuestion (o usuário digita via "Other").

### 3. Leitura prévia para sugestão de foco

Antes de perguntar sobre o foco, fazer uma leitura rápida do conteúdo para gerar sugestões relevantes:

**Se `source_type: youtube`:**
Usar `web_fetch` na URL para obter título e descrição do vídeo. Com base nesses dados, identificar os 3 ângulos mais relevantes presentes no conteúdo.

**Se `source_type: document`:**
- TXT / MD / HTML: ler os primeiros 1.000 caracteres do arquivo
- PDF: extrair o texto da primeira página com `pdftotext {file_path} - | head -c 1000`
- DOC / DOCX: extrair os primeiros parágrafos com python-docx ou pandoc

Com base no trecho lido, identificar os 3 ângulos mais relevantes presentes no documento.

**Se `source_type: local` (vídeo):**
Não é possível ler o conteúdo sem transcrição. Usar o nome do arquivo como único indício e sugerir focos genéricos do nicho.

### 4. Pergunta sobre foco (sempre)

Com base na leitura prévia, gerar **até 3 sugestões de foco específicas ao conteúdo** e apresentar via AskUserQuestion. As sugestões devem ser concretas — não genéricas.

Exemplos de sugestões geradas a partir do conteúdo:
- "Foco nos 3 erros mais comuns no contrato de compra e venda"
- "Foco na cláusula de rescisão e suas consequências práticas"
- "Foco nos documentos obrigatórios para qualificação do vendedor"

Incluir sempre a opção extra via "Other" para o usuário digitar um foco personalizado caso nenhuma sugestão atenda.

**Formato da pergunta:**
"Com base no conteúdo, identifiquei estes ângulos relevantes. Qual você quer destacar?"
- {Sugestão 1 derivada do conteúdo}
- {Sugestão 2 derivada do conteúdo}
- {Sugestão 3 derivada do conteúdo} *(se houver)*
- "Sem foco — você decide o melhor ângulo"
- Campo livre via "Other"

**Se o usuário escolher "Sem foco — você decide o melhor ângulo":**
Salvar `focus: auto` no `youtube-focus.md`. O Yago interpretará isso no step 3 como autorização para escolher autonomamente o ângulo de maior potencial para o público de corretores, com base na análise completa do conteúdo.

### 4. Salvar o output

Salve em `squads/youtube-to-instagram/output/{run-id}/v1/youtube-focus.md` usando o formato abaixo.

**Se vídeo local:**
```markdown
source_type: local
file_name: nome-do-arquivo.mp4
file_path: squads/youtube-to-instagram/assets/videos-originais/nome-do-arquivo.mp4
focus: [foco informado pelo usuário]
```

**Se URL do YouTube:**
```markdown
source_type: youtube
url: https://www.youtube.com/watch?v=...
focus: [foco informado pelo usuário]
```

**Se documento de texto:**
```markdown
source_type: document
file_name: nome-do-arquivo.pdf
file_path: squads/youtube-to-instagram/assets/documentos/nome-do-arquivo.pdf
file_format: [pdf / txt / doc / docx / md / html]
focus: [foco informado pelo usuário]
```

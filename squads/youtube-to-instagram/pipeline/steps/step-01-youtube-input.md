---
type: checkpoint
outputFile: squads/youtube-to-instagram/output/youtube-focus.md
---

# Step 01: Seleção de Vídeo

Bem-vindo ao squad **YouTube → Instagram** da Sucesso Imóvel.

Este squad transforma um vídeo em um calendário semanal completo para o Instagram: 5 posts (2 carrosséis + 3 posts únicos), isca digital em PDF, roteiro YouTube, 6 roteiros de Reels virais, 7 roteiros de Stories diários e um dashboard semanal.

**Como funciona:**
1. Você seleciona o vídeo (arquivo local ou URL do YouTube)
2. O squad transcreve e analisa o conteúdo, gerando um relatório completo
3. Você aprova a isca digital e as ideias de posts
4. O squad cria todo o conteúdo da semana e gera as imagens
5. Você revisa o resultado final e recebe o dashboard semanal

---

## Instruções para o Runner

### 1. Listar vídeos disponíveis

Use o Bash tool para escanear a pasta de vídeos:

```bash
ls squads/youtube-to-instagram/assets/videos-originais/ 2>/dev/null
```

Filtre apenas arquivos com extensão de vídeo: `.mp4`, `.mov`, `.avi`, `.mkv`, `.webm`, `.m4v`.

### 2. Perguntar ao usuário

**Se houver arquivos de vídeo na pasta:**

Use AskUserQuestion com:
- Uma opção para cada arquivo encontrado (nome do arquivo como label)
- Uma opção extra: "Informar URL do YouTube"

**Se a pasta estiver vazia ou não existir:**

Use AskUserQuestion com apenas:
- "Informar URL do YouTube"
- "Ainda vou colocar o vídeo na pasta assets/videos-originais/"

**Se o usuário escolher "Informar URL do YouTube":**

Peça a URL em uma segunda AskUserQuestion (use exemplos como opções para ajudar, mas o usuário vai digitar via "Other").

### 3. Pergunta sobre foco (sempre)

Após a seleção do vídeo, pergunte com AskUserQuestion:

"Qual é o foco ou tema principal que você quer destacar neste vídeo?"
- "Sem foco específico — analisar tudo"
- "Foco em aspectos jurídicos/legais"
- "Foco em dicas práticas para corretores"

(o usuário pode digitar um foco personalizado via "Other")

### 4. Salvar o output

Salve em `squads/youtube-to-instagram/output/youtube-focus.md` usando o formato abaixo.

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

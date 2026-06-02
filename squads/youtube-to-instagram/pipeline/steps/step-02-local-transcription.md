---
type: agent
agent: transcription
execution: inline
inputFile: squads/youtube-to-instagram/output/youtube-focus.md
outputFile: squads/youtube-to-instagram/output/video-transcript.md
---

# Step 02: Transcrição / Extração de Conteúdo

Este step processa a fonte de conteúdo selecionada no step 1:
- **Vídeo local:** transcreve o áudio com ffmpeg + Groq Whisper
- **YouTube:** cria marcador vazio (o Yago faz o fetch diretamente)
- **Documento de texto:** extrai o conteúdo textual do arquivo

---

## Instruções

### 1. Verificar fonte do conteúdo

Leia `squads/youtube-to-instagram/output/youtube-focus.md`.

- Se `source_type: youtube` → pule direto para o **Passo 5 (Output vazio)**.
- Se `source_type: local` → continue com o **Passo 2 (vídeo)**.
- Se `source_type: document` → pule para o **Passo 4b (documento)**.

### 2. Verificar pré-requisitos

Verifique se ffmpeg está instalado:

```bash
which ffmpeg
```

Se não estiver instalado, informe o usuário:
> "ffmpeg não encontrado. Instale com: `brew install ffmpeg`"
> E encerre o step sem criar output.

Verifique se o arquivo de vídeo existe:

```bash
ls "squads/youtube-to-instagram/assets/videos-originais/{file_name}"
```

Se não existir, informe o usuário e encerre.

### 3. Extrair áudio do vídeo

Execute via Bash:

```bash
ffmpeg -i "squads/youtube-to-instagram/assets/videos-originais/{file_name}" \
  -vn -acodec libmp3lame -q:a 2 \
  /tmp/si_transcription_audio.mp3 -y
```

Onde `{file_name}` é o valor de `file_name` lido do youtube-focus.md.

Se ffmpeg falhar, informe o erro ao usuário e encerre.

### 4. Transcrever com Groq Whisper

Carregue a variável de ambiente:

```bash
export $(grep -v '^#' .env | xargs) 2>/dev/null
```

Execute a transcrição:

```bash
curl -s -X POST \
  https://api.groq.com/openai/v1/audio/transcriptions \
  -H "Authorization: Bearer $GROQ_API_KEY" \
  -F "file=@/tmp/si_transcription_audio.mp3" \
  -F "model=whisper-large-v3" \
  -F "language=pt" \
  -F "response_format=text"
```

Se `GROQ_API_KEY` não estiver definida, informe o usuário:
> "GROQ_API_KEY não encontrada no arquivo .env. Adicione a linha: `GROQ_API_KEY=sua_chave_aqui`"
> E encerre o step.

Capture o resultado da transcrição (texto puro retornado pelo curl).

### 4b. Extrair texto do documento (`source_type: document`)

Verificar se o arquivo existe:
```bash
ls "squads/youtube-to-instagram/assets/documentos/{file_name}"
```

Extrair o conteúdo de acordo com o `file_format`:

**TXT / MD:**
```bash
cat "squads/youtube-to-instagram/assets/documentos/{file_name}"
```

**HTML:**
```bash
python3 -c "
from html.parser import HTMLParser
class P(HTMLParser):
    def __init__(self): super().__init__(); self.text=[]
    def handle_data(self,d): self.text.append(d)
p=P(); p.feed(open('squads/youtube-to-instagram/assets/documentos/{file_name}').read()); print(' '.join(p.text))
"
```

**PDF:**
```bash
python3 -c "
import subprocess
result = subprocess.run(['pdftotext', 'squads/youtube-to-instagram/assets/documentos/{file_name}', '-'], capture_output=True, text=True)
print(result.stdout)
"
```
Se `pdftotext` não estiver disponível, tentar com PyPDF2:
```bash
python3 -c "
import PyPDF2
with open('squads/youtube-to-instagram/assets/documentos/{file_name}','rb') as f:
    r=PyPDF2.PdfReader(f); print('\n'.join(p.extract_text() for p in r.pages))
"
```

**DOC / DOCX:**
```bash
python3 -c "
import docx
doc=docx.Document('squads/youtube-to-instagram/assets/documentos/{file_name}')
print('\n'.join(p.text for p in doc.paragraphs))
"
```
Se python-docx não estiver disponível, tentar com pandoc:
```bash
pandoc "squads/youtube-to-instagram/assets/documentos/{file_name}" -t plain
```

Se nenhuma ferramenta estiver disponível, informar o usuário com instrução de instalação e encerrar.

### 5. Salvar output

**Se fonte for local (transcrição realizada):**

Salve em `squads/youtube-to-instagram/output/video-transcript.md`:

```markdown
# Transcrição do Vídeo

source_type: local
file_name: {file_name}
transcribed_at: {data e hora atual}
model: whisper-large-v3

---

{texto completo retornado pelo Groq}
```

**Se fonte for documento:**

Salve em `squads/youtube-to-instagram/output/video-transcript.md`:

```markdown
# Conteúdo do Documento

source_type: document
file_name: {file_name}
file_format: {pdf / txt / doc / docx / md / html}
extracted_at: {data e hora atual}

---

{texto completo extraído do documento}
```

**Se fonte for YouTube (step pulado):**

Salve em `squads/youtube-to-instagram/output/video-transcript.md`:

```markdown
# Transcrição do Vídeo

source_type: youtube
transcript: none
```

### 6. Limpeza

Remova o arquivo de áudio temporário (apenas se fonte for local):

```bash
rm -f /tmp/si_transcription_audio.mp3
```

---

## Quality Criteria

- [ ] youtube-focus.md lido corretamente
- [ ] Se local: ffmpeg executado sem erros e Groq API respondeu com sucesso
- [ ] Se document: texto extraído com sucesso e salvo completo
- [ ] Se document: formato do arquivo identificado e extrator correto utilizado
- [ ] video-transcript.md salvo com conteúdo correto para o source_type
- [ ] Arquivo de áudio temporário removido após uso (apenas fonte local)

## Veto Conditions

Rejeitar e informar usuário se QUALQUER condição for verdadeira:
1. ffmpeg não está instalado e a fonte é vídeo local
2. Arquivo (vídeo ou documento) não existe no caminho especificado
3. GROQ_API_KEY não está no .env e a fonte é vídeo local
4. Groq API retornou erro ou resposta vazia
5. Nenhuma ferramenta de extração disponível para o formato do documento
6. Texto extraído do documento está vazio

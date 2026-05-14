---
type: agent
agent: transcription
execution: inline
inputFile: squads/youtube-to-instagram/output/youtube-focus.md
outputFile: squads/youtube-to-instagram/output/video-transcript.md
---

# Step 02: Transcrição de Vídeo Local

Este step transcreve o áudio de um vídeo local usando ffmpeg + Groq Whisper.
Se a fonte for YouTube, o step cria um arquivo de transcrição vazio e encerra sem fazer nada.

---

## Instruções

### 1. Verificar fonte do vídeo

Leia `squads/youtube-to-instagram/output/youtube-focus.md`.

- Se `source_type: youtube` → pule direto para o **Passo 5 (Output vazio)**.
- Se `source_type: local` → continue com o **Passo 2**.

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

**Se fonte for YouTube (step pulado):**

Salve em `squads/youtube-to-instagram/output/video-transcript.md`:

```markdown
# Transcrição do Vídeo

source_type: youtube
transcript: none
```

### 6. Limpeza

Remova o arquivo de áudio temporário:

```bash
rm -f /tmp/si_transcription_audio.mp3
```

---

## Quality Criteria

- [ ] youtube-focus.md lido corretamente
- [ ] Se local: ffmpeg executado sem erros
- [ ] Se local: Groq API chamada com sucesso e resposta recebida
- [ ] video-transcript.md salvo com conteúdo correto
- [ ] Arquivo de áudio temporário removido após uso

## Veto Conditions

Rejeitar e informar usuário se QUALQUER condição for verdadeira:
1. ffmpeg não está instalado e a fonte é local
2. Arquivo de vídeo não existe no caminho especificado
3. GROQ_API_KEY não está no .env
4. Groq API retornou erro ou resposta vazia

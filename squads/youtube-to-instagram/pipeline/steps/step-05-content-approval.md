---
type: checkpoint
inputFile: squads/youtube-to-instagram/output/{run-id}/Posts/post-content.md
outputFile: squads/youtube-to-instagram/output/{run-id}/selected-jeorge-photo.md
---

# Step 16: Aprovação do Conteúdo + Seleção de Foto

Todo o conteúdo do ciclo foi criado. Antes de gerar as imagens, você revisa o material e escolhe qual foto do Dr. Jeorge usar no Ter-PU1.

## O que está disponível para revisão

### Posts
- `output/{run-id}/Posts/post-content.md` — conteúdo dos 5 posts (Seg-CT, Ter-PU1, Qua-PU2, Qui-PU3, Sex-CCTA)
- `output/{run-id}/Posts/post-content.html` — brief visual dos 5 posts em Premium Dark — **abrir no navegador para revisar**

### Isca Digital
- `output/{run-id}/Lead-Magnets/lead-magnet-{PALAVRA}-{slug}.pdf` — PDF final da isca digital

### Roteiro YouTube
- `output/{run-id}/Roteiros/roteiro-youtube-{slug}.html` — versão visual do roteiro

### Reels Virais
- `output/{run-id}/Roteiros/roteiros-reels-virais-{slug}.html` — todos os 6 roteiros agrupados

### Stories
- `output/{run-id}/Stories/stories-semana-{slug}.html` — todos os stories da semana agrupados

### Análise do Vídeo
- `output/{run-id}/v1/youtube-analysis.html` — relatório completo do vídeo

---

## Pergunta 1: Conteúdo dos Posts

**O conteúdo dos 5 posts está aprovado para gerar as imagens?**

- **Aprovar** — Conteúdo ótimo, pode gerar as imagens
- **Ajustar texto** — Descrever o que mudar (post específico, slide, legenda, hashtags) e Iago corrige antes de prosseguir
- **Mudar tom** — Reescrever com tom de voz diferente
- **Cancelar** — Voltar ao step 10 (ideas-approval) e escolher outras ideias

> Após a aprovação, Diego Design renderiza os 5 posts. Mudanças de texto depois desta etapa exigem re-renderização.

---

## Pergunta 2: Foto do Dr. Jeorge (Ter-PU1)

Listar as fotos disponíveis:

```bash
ls assets/imagens/jeorge/ | grep -E 'SI-Jeorge-[0-9]+' | sort
```

**Qual foto do Dr. Jeorge usar no Ter-PU1?**

Apresentar as opções com base no resultado do `ls` acima. Usar `AskUserQuestion` com as fotos disponíveis como opções dinâmicas.

Salvar a escolha em `output/{run-id}/selected-jeorge-photo.md`:

```markdown
# Foto Dr. Jeorge Selecionada

Arquivo: {nome-do-arquivo-escolhido}
Número: {01 | 02 | 03 | ...}
```

---

Se o conteúdo for aprovado e a foto selecionada, Diego Design será acionado no step 17 para renderizar os 5 posts em `output/{run-id}/Posts/`.

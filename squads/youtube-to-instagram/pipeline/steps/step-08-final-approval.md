---
type: checkpoint
inputFile: squads/youtube-to-instagram/output/{run-id}/review.md
outputFile: squads/youtube-to-instagram/output/{run-id}/final-approval.md
---

# Step 19: Aprovação Final

O conteúdo foi revisado por Renata Revisão. Este é o resultado final do squad para este ciclo.

## Context

O arquivo `output/{run-id}/review.md` contém o veredito completo com scores, feedback e resultado da revisão de qualidade.

Todos os entregáveis do ciclo estão disponíveis em `output/{run-id}/`.

---

**O que você quer fazer com este resultado?**

- **Aprovar** — O ciclo está encerrado. Todos os arquivos estão prontos para uso.
- **Solicitar ajuste** — Descrever o que quer mudar. O pipeline volta ao step 11 (iago-content-creation) para revisão.
- **Ver os posts** — Exibir as imagens geradas para revisão visual antes de decidir.
- **Descartar e recomeçar** — Voltar ao step 10 (ideas-approval) e escolher outras ideias.

---

## Arquivos gerados neste ciclo

### `output/{run-id}/v1/`
- `youtube-analysis.md` — Relatório completo do vídeo (8 seções)
- `youtube-analysis.html` — Versão visual do relatório

### `output/{run-id}/Lead-Magnets/`
- `lead-magnet-{PALAVRA}-{slug}.md` — Conteúdo da isca digital
- `lead-magnet-{PALAVRA}-{slug}.html` — HTML intermediário
- `lead-magnet-{PALAVRA}-{slug}.pdf` — PDF final entregável

### `output/{run-id}/Roteiros/`
- `roteiro-youtube-{slug}.md` — Roteiro YouTube com melhorias
- `roteiro-youtube-{slug}.html` — Versão visual do roteiro
- `roteiro-reel-viral-01-dom-{slug}.md` a `roteiro-reel-viral-06-sex-{slug}.md` — 6 Roteiros Reel Viral
- `roteiros-reels-virais-{slug}.html` — HTML unificado dos 6 roteiros

### `output/{run-id}/Stories/`
- `stories-01-dom-{slug}.md` a `stories-07-sab-{slug}.md` — 7 roteiros de stories diários
- `stories-semana-{slug}.html` — HTML semanal unificado

### `output/{run-id}/Prompts/`
- `ai-image-prompt-post2.md` — Prompt de imagem IA para o Qua-PU2
- `media-prompts.md` — 3 prompts Imagen (Alerta, Dado, Reflexão)

### `output/{run-id}/Posts/`
- `post-content.md` — Conteúdo dos 5 posts (Seg-CT, Ter-PU1, Qua-PU2, Qui-PU3, Sex-CCTA)
- `post-content.html` — Brief visual dos 5 posts
- `{slug}-single-post-1.png` — Ter-PU1 (1080×1350)
- `{slug}-single-post-2.png` — Qua-PU2 (1080×1350)
- `{slug}-single-post-3.png` — Qui-PU3 (1080×1350)
- `{slug}-slide-01.png` a `{slug}-slide-NN.png` — Seg-CT (1080×1440)
- `{slug}-ccta-slide-01.png` a `{slug}-ccta-slide-NN.png` — Sex-CCTA (1080×1440)

### `output/{run-id}/_html/`
- HTMLs de renderização intermediária de todos os posts e carrosséis

### `output/{run-id}/`
- `review.md` — Relatório de qualidade de Renata

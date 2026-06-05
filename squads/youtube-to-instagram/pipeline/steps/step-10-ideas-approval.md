---
type: checkpoint
inputFile: squads/youtube-to-instagram/output/{run-id}/post-ideas.md
outputFile: squads/youtube-to-instagram/output/{run-id}/approved-ideas.md
---

# Step 10: Aprovação das Ideias + Seleção de Foto

Yago Vídeo gerou 5 ideias de posts com base no vídeo analisado. Agora você aprova as ideias e escolhe a foto do Dr. Jeorge para o Ter-PU1 — antes de Iago criar o conteúdo.

## Context

As ideias estão em `output/{run-id}/post-ideas.md`. Cada ideia inclui formato, ângulo editorial, hook e conceito visual.

---

## Pergunta 1: Aprovação das Ideias

**As 5 ideias de posts estão aprovadas para desenvolvimento?**

- **Aprovar todas** — Iago desenvolve os 5 posts como propostos
- **Ajustar** — Descrever o ajuste (ângulo, formato, hook) e Iago incorpora antes de criar
- **Cancelar** — Voltar ao step 9 para gerar novas ideias

---

## Pergunta 2: Foto do Dr. Jeorge (Ter-PU1)

Listar as fotos disponíveis na pasta global de fotos do CEO:

```bash
ls /Users/sandronolasco/Antigravity/Projetos/SucessoImovel/si-squads/assets/imagens/fotos-ceo/ | sort
```

**Qual foto do Dr. Jeorge usar no Ter-PU1?**

Apresentar as opções disponíveis com base no resultado acima. Usar `AskUserQuestion` com as fotos como opções dinâmicas.

Salvar a escolha em `output/{run-id}/selected-jeorge-photo.md`:

```markdown
# Foto Dr. Jeorge Selecionada

Arquivo: {nome-do-arquivo-escolhido}
Pasta: /Users/sandronolasco/Antigravity/Projetos/SucessoImovel/si-squads/assets/imagens/fotos-ceo/
```

---

Após a aprovação e seleção da foto, Iago criará o conteúdo completo dos 5 posts no step seguinte, já referenciando a foto escolhida.

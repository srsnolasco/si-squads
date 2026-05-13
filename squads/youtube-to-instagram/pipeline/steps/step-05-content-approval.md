---
type: checkpoint
inputFile: squads/youtube-to-instagram/output/post-content.md
outputFile: squads/youtube-to-instagram/output/post-content.md
---

# Step 05: Aprovação do Conteúdo + Seleção de Foto

Iago Instagram criou o conteúdo completo dos 4 posts. Antes de gerar as imagens, você revisa o texto e escolhe qual foto do Dr. Jeorge usar no Post Único 1.

## Context

O arquivo `output/post-content.md` contém:
- Texto para os 3 posts únicos (headlines, body text, quote, accent keywords)
- Estrutura do carrossel (slides, supporting text)
- Legendas completas (hook + corpo + CTA) para todos os posts
- Hashtags

Esta é sua oportunidade de ajustar qualquer texto antes que as imagens sejam geradas. Após a aprovação, Diego Design criará os arquivos HTML e renderizará as imagens — mudanças de texto depois desta etapa exigem re-renderização.

---

## Pergunta 1: Conteúdo

**O conteúdo está aprovado para gerar as imagens?**

Opções:
- **Aprovar** — O conteúdo está ótimo, pode gerar as imagens
- **Ajustar texto** — Descreva o que quer mudar (post específico, legenda, hashtags) e Iago corrige antes de prosseguir
- **Mudar o tom** — Reescrever com tom de voz diferente
- **Cancelar este post** — Voltar para a seleção de ideias e escolher outra

---

## Pergunta 2: Foto do Dr. Jeorge (Post Único 1)

Antes de iniciar a renderização, listar as fotos disponíveis:

```bash
ls assets/imagens/jeorge/ | grep -E 'SI-Jeorge-[0-9]+' | sort
```

**Qual foto do Dr. Jeorge usar no Post Único 1?**

Apresentar as opções disponíveis com base no resultado do ls acima. Exemplos esperados:
- **Foto 01** — `SI-Jeorge-01.png`
- **Foto 02** — `SI-Jeorge-02.png`
- **Foto 03** — `SI-Jeorge-03.png`
- *(novas fotos adicionadas seguirão a sequência 04, 05, 06...)*

Usar `AskUserQuestion` com as fotos disponíveis como opções dinâmicas.

Salvar a escolha em `output/selected-jeorge-photo.md`:

```markdown
# Foto Dr. Jeorge Selecionada

Arquivo: {nome-do-arquivo-escolhido}
Número: {01 | 02 | 03 | ...}
```

---

Se o conteúdo for aprovado e a foto selecionada, Diego Design será acionado para criar e renderizar os 4 posts em `output/{run-id}/Posts/`.

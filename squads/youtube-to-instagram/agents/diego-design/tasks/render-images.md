---
task: "Render Images"
order: 2
input: |
  - slide_htmls: Arquivos HTML dos slides em output/slides/ (gerados pela tarefa design-slides)
output: |
  - slide_pngs: Um PNG por slide em output/slides/ (slide-01.png, slide-02.png, ...)
---

# Render Images

Renderiza cada slide HTML como PNG via Playwright (skill image-creator). Inicia um servidor HTTP local, renderiza o slide 1 e verifica visualmente, depois processa o batch completo. Para o servidor após concluir.

## Process

1. Verificar quais arquivos slide-NN.html existem em `output/slides/`.
2. Iniciar servidor HTTP local na porta 8765 apontando para o diretório `output/slides/`:
   ```bash
   python3 -m http.server 8765 --directory "{absolute_path}/output/slides/" &
   for i in $(seq 1 30); do curl -s http://localhost:8765 > /dev/null 2>&1 && break || sleep 0.1; done
   ```
3. Renderizar o slide 1:
   - `browser_navigate` para `http://localhost:8765/slide-01.html`
   - `browser_resize` para width: 1080, height: 1440
   - `browser_take_screenshot` salvando em `output/slides/slide-01.png`
4. Verificar visualmente o slide-01.png: texto legível, cores corretas, layout sem clipping, header e footer presentes.
5. Se o slide 1 passar a verificação: renderizar os demais slides em sequência (slide-02, slide-03, ...) repetindo o mesmo processo de navigate → resize → screenshot.
6. Se o slide 1 falhar: identificar o problema no HTML, corrigir, e re-renderizar antes de prosseguir.
7. Parar o servidor HTTP após o último slide:
   ```bash
   pkill -f "http.server 8765" 2>/dev/null || true
   ```
8. Confirmar que todos os PNGs foram gerados em `output/slides/`.

## Output Format

```
Renderização concluída:
- slide-01.png ✅ (verificado)
- slide-02.png ✅
- slide-03.png ✅
...
- slide-NN.png ✅

Total: N slides renderizados em output/slides/
Design system aplicado: Template C Premium Dark — Roxo #7B2FBE / Preto #0A0012 / Branco #FFFFFF
```

## Output Example

```
Renderização concluída:
- slide-01.png ✅ (verificado — headline 60px, footer visível, contraste aprovado)
- slide-02.png ✅
- slide-03.png ✅
- slide-04.png ✅
- slide-05.png ✅
- slide-06.png ✅
- slide-07.png ✅ (CTA slide — "Comenta CONTRATO" substituiu "ARRASTE →")

Total: 7 slides renderizados em squads/youtube-to-instagram/output/slides/
Design system: Template C Premium Dark
Viewport: 1080x1440px
Fontes: Montserrat 900 (títulos) + Inter 500-800 (corpo)
Paleta: #7B2FBE (roxo) / #0A0012-#0D0D0D (preto) / #9B9B9B (cinza) / #FFFFFF (branco)
```

## Quality Criteria

- [ ] Servidor HTTP iniciado e confirmado antes de qualquer rendering
- [ ] Slide 1 renderizado e verificado visualmente antes do batch
- [ ] Viewport definido como 1080x1440 para cada slide antes do screenshot
- [ ] Todos os PNGs salvos com nomes zero-padded (slide-01.png, slide-02.png, ...)
- [ ] Servidor HTTP parado após o último slide
- [ ] Relatório de conclusão inclui contagem de slides e design system aplicado

## Veto Conditions

Rejeitar e refazer se QUALQUER condição for verdadeira:
1. O slide 1 renderizado mostra texto clippado, ilegível (fonte < 34px no body) ou layout quebrado
2. Algum PNG está ausente — o número de PNGs deve ser igual ao número de HTMLs gerados

---
task: "Design Slides"
order: 1
input: |
  - post_content: Estrutura de slides com headline, supporting text e accent keywords (post-content.md)
  - visual_identity: Regras de identidade visual da Sucesso Imóvel (visual-identity.md)
  - template_reference: HTML de referência do Template C Premium Dark (template-reference.html)
output: |
  - slide_htmls: Um arquivo HTML por slide, salvos em output/slides/
---

# Design Slides

Cria um arquivo HTML auto-suficiente por slide, seguindo o Template C Premium Dark da Sucesso Imóvel. Cada HTML contém o design system completo inline, o conteúdo do slide (headline, supporting text, accent keywords) e todos os elementos de marca (header, accent line, footer).

## Process

1. Ler `post-content.md` para obter a estrutura de slides aprovada.
2. Ler `visual-identity.md` para as regras de design e paleta de cores.
3. Ler `template-reference.html` como modelo base de estrutura HTML/CSS.
4. Documentar o design system para este post específico: cores exatas, família tipográfica, tamanhos de fonte, espaçamento.
5. Para cada slide:
   a. Criar um HTML completo e auto-suficiente baseado no template-reference.html.
   b. Substituir o conteúdo de exemplo pelo conteúdo real do slide (headline, supporting text).
   c. Aplicar accent keywords em roxo (#A855F7) dentro do headline.
   d. Ajustar o background do slide conforme indicado (escuro padrão / card translúcido roxo / destaque roxo).
   e. Manter header (badge SI + nome + tag), accent line e footer em todos os slides exceto configurações específicas do último.
   f. No último slide: substituir "ARRASTE →" pelo CTA específico do post.
   g. Garantir font sizes: hero 60px+, heading 43px+, body 34px+, caption 24px+.
   h. Verificar contraste WCAG AA 4.5:1 para todos os textos.
6. Salvar cada HTML como `output/slides/slide-01.html`, `slide-02.html`, etc. (zero-padded).

## Output Format

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@500;600;700;800&family=Montserrat:wght@800;900&display=swap');
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      width: 1080px; height: 1440px; overflow: hidden;
      background: linear-gradient(160deg, #0A0012 0%, #1A0A2E 45%, #0D0D0D 100%);
      font-family: 'Inter', sans-serif;
      display: flex; flex-direction: column;
      padding: 72px; position: relative;
    }
    /* [design system completo inline] */
  </style>
</head>
<body>
  <!-- glow effects, accent line, header, content, footer -->
</body>
</html>
```

## Output Example

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@500;700;800&family=Montserrat:wght@900&display=swap');
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      width: 1080px; height: 1440px; overflow: hidden;
      background: linear-gradient(160deg, #0A0012 0%, #1A0A2E 45%, #0D0D0D 100%);
      font-family: 'Inter', sans-serif;
      display: flex; flex-direction: column;
      padding: 72px; position: relative;
    }
    .glow-top { position: absolute; top: -100px; right: -100px; width: 500px; height: 500px; background: radial-gradient(circle, #7B2FBE44, transparent 65%); pointer-events: none; }
    .accent-line { position: absolute; top: 0; left: 72px; right: 72px; height: 3px; background: linear-gradient(90deg, transparent, #7B2FBE, #A855F7, transparent); }
    .header { display: flex; align-items: center; justify-content: space-between; position: relative; z-index: 1; margin-bottom: 48px; }
    .badge { display: flex; align-items: center; gap: 16px; }
    .badge-icon { width: 56px; height: 56px; border-radius: 12px; background: linear-gradient(135deg, #7B2FBE, #A855F7); display: flex; align-items: center; justify-content: center; font-size: 28px; font-weight: 900; color: #fff; }
    .badge-name { font-size: 28px; font-weight: 700; color: #fff; }
    .tag { background: #7B2FBE33; border: 1px solid #7B2FBE; border-radius: 8px; padding: 8px 20px; font-size: 22px; color: #A855F7; font-weight: 700; text-transform: uppercase; letter-spacing: 2px; }
    .content { flex: 1; display: flex; flex-direction: column; justify-content: center; position: relative; z-index: 1; }
    .eyebrow { font-size: 24px; font-weight: 700; color: #A855F7; text-transform: uppercase; letter-spacing: 3px; margin-bottom: 24px; }
    .headline { font-size: 60px; font-weight: 900; line-height: 1.18; font-family: 'Montserrat', sans-serif; color: #fff; margin-bottom: 32px; }
    .headline .accent { color: #A855F7; }
    .supporting { font-size: 34px; font-weight: 500; color: #9B9B9B; line-height: 1.55; }
    .footer { display: flex; align-items: center; justify-content: space-between; padding-top: 28px; border-top: 1px solid rgba(255,255,255,0.08); position: relative; z-index: 1; margin-top: 40px; }
    .footer-left { display: flex; align-items: center; gap: 16px; }
    .footer-dot { width: 40px; height: 40px; border-radius: 50%; background: linear-gradient(135deg, #7B2FBE, #A855F7); }
    .footer-handle { font-size: 24px; color: #6B6B6B; font-weight: 500; }
    .swipe { font-size: 24px; color: #A855F7; font-weight: 600; }
  </style>
</head>
<body>
  <div class="glow-top"></div>
  <div class="accent-line"></div>
  <div class="header">
    <div class="badge">
      <div class="badge-icon">SI</div>
      <span class="badge-name">Sucesso Imóvel</span>
    </div>
    <div class="tag">Contratos</div>
  </div>
  <div class="content">
    <div class="eyebrow">Contratos Imobiliários</div>
    <h1 class="headline">Cláusula 1: Arrependimento <span class="accent">sem multa</span> definida</h1>
    <p class="supporting">Sem esta cláusula, o comprador pode desistir a qualquer momento sem pagar nada. O corretor, que já investiu tempo, visitas e negociação, fica <strong style="color:#fff;">sem amparo jurídico</strong> para cobrar a comissão. Defina prazo e percentual de multa no contrato.</p>
  </div>
  <div class="footer">
    <div class="footer-left">
      <div class="footer-dot"></div>
      <span class="footer-handle">@sucessoimovel</span>
    </div>
    <span class="swipe">ARRASTE →</span>
  </div>
</body>
</html>
```

## Quality Criteria

- [ ] Um arquivo HTML por slide, nomeado slide-01.html, slide-02.html, etc.
- [ ] Cada HTML é auto-suficiente: inline CSS, apenas Google Fonts @import externo
- [ ] body tem width: 1080px e height: 1440px explícitos com overflow: hidden
- [ ] Hero/headline mínimo 60px (Montserrat 900); body/supporting mínimo 34px (Inter 500+)
- [ ] Accent keywords aplicadas com cor #A855F7 inline no HTML
- [ ] Header (badge + nome + tag), accent line e footer presentes em todos os slides
- [ ] Último slide com CTA específico em vez de "ARRASTE →"

## Veto Conditions

Rejeitar e refazer se QUALQUER condição for verdadeira:
1. Qualquer arquivo HTML tem dependência externa além de Google Fonts @import (CSS framework, JavaScript, CDN de ícones)
2. O body não tem width: 1080px e height: 1440px explícitos — qualquer valor auto ou percentual é inválido

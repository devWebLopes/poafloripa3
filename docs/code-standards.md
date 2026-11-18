# Padrões de Código

## HTML
- Semântico (`header`, `main`, `section`, `footer`, `nav`); um único `<h1>`.
- `lang="pt-BR"`, `title` e `meta description` sempre presentes.
- IDs únicos e descritivos em elementos interativos; `label for` ligado a cada campo.
- Imagens com `alt` descritivo.

## CSS
- Utilitários Tailwind para layout; classes customizadas (`.sarda-card`, `.motion-canvas`…) para efeitos.
- Cores sempre via tokens (`pool`, `minimal`, `brand`); nada de hex solto fora do tema.
- Respeitar `prefers-reduced-motion` ao adicionar/ajustar animações.

## JavaScript
- ES2020+, `const`/`let`, funções pequenas, nomes em inglês para código e português para textos de UI.
- Sem dependências novas sem aprovação.
- Escapar/sanitizar qualquer string inserida via `innerHTML` (dados são internos, mas manter o hábito).
- Formatar preço com `Intl.NumberFormat('pt-BR', {style:'currency', currency:'BRL'})`.
- Sem `console.log` em produção.

## Acessibilidade e SEO
- Foco visível, contraste AA, botões como `<button>`, modais com `Esc` para fechar e foco gerenciado.
- Open Graph e dados estruturados são desejáveis.

## Git
- Mensagens: `tipo(escopo): descrição` (ex.: `refactor(js): extrai filtros`).

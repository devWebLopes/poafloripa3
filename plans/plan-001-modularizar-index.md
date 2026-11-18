# Plano 001 — Modularizar `index.html`

> **Premissa:** a tarefa não foi informada; foi inferida do código (arquivo único de ~1 MB com CSS, JS e dados embutidos). Ajuste se a tarefa real for outra.

- **Status:** Rascunho
- **Agente líder:** Arquiteto ([agents/arquiteto.md](../agents/arquiteto.md))
- **Apoio:** Frontend, Conteúdo & Dados, QA & Deploy
- **Skills:** vanilla-js-modular, otimizacao-imagens, tailwind-design-system, catalogo-imoveis, qa-validacao-web, deploy-vercel

## Objetivo
Separar CSS, JS, dados e imagens do `index.html`, reduzindo seu tamanho e facilitando manutenção, **sem alterar visual ou comportamento**.

## Critérios de aceite
- `index.html` < 100 KB.
- Comportamento e visual idênticos ao original.
- Checklist de `docs/deploy.md` completo; Lighthouse ≥ 90.

## Passos
1. **Baseline (QA):** capturar screenshots (375/768/1280) e anotar fluxos; branch `refactor/modularizar`.
2. **Mapear (Arquiteto):** ler `index.html` inteiro (linhas 800–1483 = JS/dados), listar funções globais usadas em `onclick`, dados e base64.
3. **Imagens (Conteúdo):** extrair base64 → `assets/img/*.webp`, atualizar referências, lazy-load.
4. **Dados (Conteúdo):** mover array de imóveis para `assets/js/data.js`; derivar contadores "Todos (6)" etc.
5. **CSS (Frontend):** mover `<style>` para `assets/css/styles.css`; manter tailwind.config inline; adicionar `prefers-reduced-motion`.
6. **JS (Frontend):** dividir em `filters.js`, `render.js`, `effects.js`, `main.js` (ES modules); expor em `window` funções chamadas inline.
7. **Cache (Deploy):** headers de cache para `/assets/*` em `vercel.json`.
8. **Validação (QA):** comparar com baseline, console limpo, checklist e Lighthouse.
9. **Entrega:** commits atômicos, preview Vercel, aprovação do usuário, deploy `--prod`.

## Riscos e mitigação
| Risco | Mitigação |
|---|---|
| Quebra de `onclick` inline | Inventário de funções e teste de cada fluxo |
| `file://` bloqueia ES modules | Testar com `npx serve .` |
| Perda de qualidade das fotos | Revisão visual, WebP q≈80 |

## Rollback
Reverter branch / commit anterior ao baseline.

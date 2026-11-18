# Skill: vanilla-js-modular

**Objetivo:** organizar e evoluir o JavaScript sem frameworks.

## Regras
- Separar em módulos ES: `data`, `filters`, `render`, `effects`, `main`.
- Funções hoje usadas em `onclick` (`applySearchFilters`, `searchByCode`, `resetAllFilters`, `filterByCityQuick`, `openCatalogDrawer`, `openPrivateVisitModal`, etc.) devem continuar funcionando: expor em `window` ou migrar para `addEventListener`.
- Funções puras para filtro/ordenação (testáveis).
- Sem libs novas; Lucide: chamar `lucide.createIcons()` após render dinâmico.
- Lag scroll com `requestAnimationFrame` e listener `passive`.

## Referências
[../docs/architecture.md](../docs/architecture.md) · [../docs/code-standards.md](../docs/code-standards.md)

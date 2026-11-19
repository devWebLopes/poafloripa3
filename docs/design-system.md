# Design System

## Cores (tailwind.config)
| Token | Valor | Uso |
|---|---|---|
| `pool` | `#00B4D8` | CTA, destaques |
| `pool-secondary` | `#007791` | links, rótulos |
| `pool-deep` / `pool-abyss` | `#072A36` / `#041B24` | textos escuros, rodapé |
| `pool-light` | `#EBF9FC` | fundos suaves |
| `pool-bar` | `#12B8D8` | **exclusivo da barra superior** (D-02: barra apenas) |
| `brand-red` | `#D62828` | apenas ícone do logo |
| `minimal-*` | bg, offwhite, border, muted, ink | neutros |

### Barra superior (D-02/D-03 — 18/11/2026)
- Gradiente: `--pool-bar-start #14BBDC` → `--pool-bar #12B8D8` (55%) → `--pool-bar-end #0E9CC4`.
- **Texto/ícones: brancos** (revisão de 18/11/2026, a pedido do solicitante — a versão com texto petróleo foi rejeitada visualmente).
- Contraste medido com texto branco: 2,29:1 / 2,37:1 / 3,20:1 — **abaixo de AA**. É uma exceção aprovada pelo solicitante; `docs/code-standards.md` continua valendo para o restante do site.
- Alternativa AA, se solicitada: escurecer a barra para ~`#07809B` (branco ≈ 4,5:1), o que reduz a percepção de azul claro.
- Estado `scrolled`: `rgba(16,169,210,0.96)` + blur + borda `rgba(7,42,54,0.2)`; o foco de teclado usa outline petróleo para permanecer visível.
- Escopo fechado: CTAs, links, rodapé e `pool-secondary` **não** foram alterados.
- Sublinhado de hover/focus usa `currentColor`, acompanhando a cor do texto.

## Tipografia
- Títulos: Cormorant Garamond (`font-serif`).
- Texto/UI: Plus Jakarta Sans (`font-sans`); rótulos em caixa-alta com `tracking-[0.15–0.22em]`.

## Efeitos assinatura
1. **Ken Burns** no hero (`.motion-canvas`, 26s).
2. **Itens flutuantes** (`.architectural-float*`).
3. **Lag scroll** (`.lag-item[data-lag]`).
4. **Hover elegante** em cards (`.sarda-card`, zoom da imagem).
5. **Mosaico de 5 fotos** no modal (`.auxiliadora-mosaic`).
6. **Pulso do WhatsApp** (`.wa-official-pulse`).

## Princípios
Minimalismo, muito espaço em branco, bordas finas `#EAEAEA`, sombras suaves, sem excesso de cor.

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
- Texto/ícones: `--pool-bar-ink #072A36` (petróleo), substituindo o branco.
- Contraste medido: 6,58:1 / 6,37:1 / 4,72:1 entre texto e cada parada do gradiente — AA para texto normal (≥ 4,5:1).
- Estado `scrolled`: `rgba(16,169,210,0.96)` + blur + borda `rgba(7,42,54,0.2)`.
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

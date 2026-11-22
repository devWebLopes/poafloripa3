# Design System

## Cores (tailwind.config)
| Token | Valor | Uso |
|---|---|---|
| `pool` | `#00B4D8` | CTA, destaques |
| `pool-secondary` | `#007791` | links, rótulos |
| `pool-deep` / `pool-abyss` | `#072A36` / `#041B24` | textos escuros, rodapé |
| `pool-light` | `#EBF9FC` | fundos suaves |
| `pool-bar` | `#12B8D8` | **exclusivo da barra superior** (D-02: barra apenas) |
| `brand-red` | `#D62828` | apenas ícone do logo. **Atenção:** o PNG oficial do logo renderiza esse vermelho como `#FD0215` (medido pixel a pixel em 20/11/2026); o favicon usa o valor do ativo, não o do token |
| `minimal-*` | bg, offwhite, border, muted, ink | neutros |

### Barra superior (D-02/D-03 — 18/11/2026)
- Gradiente: `--pool-bar-start #14BBDC` → `--pool-bar #12B8D8` (55%) → `--pool-bar-end #0E9CC4`.
- **Texto/ícones: brancos** (revisão de 18/11/2026, a pedido do solicitante — a versão com texto petróleo foi rejeitada visualmente).
- Contraste medido com texto branco: 2,29:1 / 2,37:1 / 3,20:1 — **abaixo de AA**. É uma exceção aprovada pelo solicitante; `docs/code-standards.md` continua valendo para o restante do site.
- Alternativa AA, se solicitada: escurecer a barra para ~`#07809B` (branco ≈ 4,5:1), o que reduz a percepção de azul claro.
- Estado `scrolled`: `rgba(16,169,210,0.96)` + blur + borda `rgba(7,42,54,0.2)`; o foco de teclado usa outline petróleo para permanecer visível.
- Escopo fechado: CTAs, links, rodapé e `pool-secondary` **não** foram alterados.
- Sublinhado de hover/focus usa `currentColor`, acompanhando a cor do texto.

## Logomarca (D-01 — 20/11/2026)
- Arquivo de produção: `assets/img/logo-poa-floripa-imoveis.png` (720×148, PNG com transparência, 41 KB).
- Composição: "POA" + casa vermelha + "FLORIPA" em branco, com "IMÓVEIS" em branco centralizado na segunda linha.
- Aplicação: header (`h-[46px]` no mobile, `h-[54px]` a partir de `sm`) e rodapé (`h-12`), **direto sobre o azul**, sem selo.
- `alt="Poa Floripa Imóveis"`; o link da marca continua resetando os filtros.
- Fonte: opção 2 aprovada em 20/11/2026. Os arquivos originais recebidos tinham fundo preto; a versão de produção foi recortada, teve o fundo removido e foi redimensionada.
- Contraste: o logo é branco sobre `#12B8D8` (2,37:1). Vale a mesma exceção registrada para a barra.

### Favicon (20/11/2026)
- Desenho: **apenas a casinha da marca**, redesenhada em vetor (sem as letras) no **vermelho exato do ativo do logo (`#FD0215`)**, num quadrado de 120×120 com ~6,7% de respiro em cada lado. Não é o logo inteiro reduzido — a 16 px as letras seriam ilegíveis.
- Ativos em `assets/img/`:
  | Arquivo | Uso |
  |---|---|
  | `favicon.svg` | vetor (0,6 KB); navegadores modernos |
  | `favicon.ico` | 16/32/48 px; aba, favoritos e requisições legadas de `/favicon.ico` |
  | `favicon-96x96.png` | fallback PNG para navegadores sem SVG |
  | `apple-touch-icon.png` | 180×180 com fundo branco (iOS ignora transparência) |
- Markup no `<head>` do `index.html`: `favicon.ico` → `favicon.svg` → PNG 96 → `apple-touch-icon`. Resolve o 404 de `/favicon.ico` registrado no PRD (C-04).
- `assets/img/fav_icon.svg` (SVG que embute o logo inteiro, 720×148, em PNG base64) **não é mais usado**.

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
7. **Slideshow editorial estilo Hero com molduras Glassmorphism** (`#duasCapitais`): crossfade de 1100 ms, ciclo de 6,5 s, movimento Ken Burns contínuo (`slowKenBurns`, 24s), pílula flutuante seletora de cidade e textos organizados em 4 blocos com moldura translúcida (`backdrop-filter: blur(12px)`), flutuação contínua (`.dc-float-wrap*`) e elevação no hover (`.dc-glass-card:hover`).

## Princípios
Minimalismo, muito espaço em branco, bordas finas `#EAEAEA`, sombras suaves, sem excesso de cor.

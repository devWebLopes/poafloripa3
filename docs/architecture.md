# Arquitetura

## Estado atual
```
poaflorpia3/
├── index.html   # ~1 MB, 1483 linhas: HTML + CSS + JS + dados
├── vercel.json
└── README.md
```

## Estrutura alvo (sem build, compatível com Vercel estático)
```
├── index.html
├── assets/
│   ├── css/styles.css
│   ├── js/
│   │   ├── data.js        # array de imóveis
│   │   ├── filters.js     # busca, ordenação, código
│   │   ├── render.js      # cards, modal, drawer
│   │   ├── effects.js     # hero, float, lag scroll
│   │   └── main.js        # init
│   └── img/               # imagens extraídas (WebP)
└── vercel.json
```

## Decisões
- Manter **sem build** (CDN + ES modules nativos `<script type="module">`).
- Imagens base64 → arquivos em `assets/img/` em WebP, com `loading="lazy"` e `width/height`.
- Estado global mínimo: lista filtrada + imóvel ativo.
- Funções chamadas por `onclick` inline devem ser expostas em `window` ou migradas para `addEventListener`.
- Tailwind CDN é aceitável para este escopo; se performance for crítica, migrar para build do Tailwind (decisão a registrar em plano).
- Desde a Onda 1 de 13/11/2026 (PRD em `docs/prd-alteracoes-site-2026-11-13.md`), o **drawer do catálogo não tem entrada no desktop**: é aberto apenas pelo botão "Menu" (`lg:hidden`), no mobile. Decisão D-04 registrada no plano 003.

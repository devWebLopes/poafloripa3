# Skill: otimizacao-imagens

**Objetivo:** reduzir o peso do `index.html` (~1 MB) e acelerar o carregamento.

## Regras
- Extrair imagens base64 para `assets/img/` com nomes padronizados: `{codigo}-{bairro}-{n}.webp`.
- Converter para WebP (qualidade ~80), máx. 1600 px de largura; thumbnails ~800 px para cards.
- `loading="lazy"`, `decoding="async"`, `width`/`height` explícitos; hero sem lazy.
- Guardar originais fora do repositório de deploy ou em `assets/img/originals/` ignorado.
- Verificar visualmente após conversão.

## Ferramentas
`sharp` via `npx`, ou script Node temporário (não versionar dependências desnecessárias).

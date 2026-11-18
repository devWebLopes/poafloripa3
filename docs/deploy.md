# Deploy e Validação

## Publicação
- Vercel, site estático na raiz: `npx vercel --prod` ou importação do repositório Git.
- `vercel.json`: `cleanUrls: true`, `trailingSlash: false`.

## Servidor local
`npx serve .` (necessário se usar ES modules; `file://` bloqueia módulos).

## Checklist antes de entregar
- [ ] Sem erros no console.
- [ ] Filtros (tipo, local, ordenação) e busca por código funcionam.
- [ ] Modal abre/fecha (botão e `Esc`), mosaico e lightbox OK.
- [ ] WhatsApp e telefones corretos.
- [ ] Responsivo: 375, 768, 1280 px.
- [ ] Lighthouse: Performance, SEO e Acessibilidade ≥ 90.
- [ ] Efeitos visuais preservados.

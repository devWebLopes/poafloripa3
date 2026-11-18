# Documentação — Poa Floripa Imóveis

Site WEB estático de imóveis de médio/alto padrão **exclusivamente para venda** em Porto Alegre e Florianópolis.

## Stack (detectada no código)
| Camada | Tecnologia |
|---|---|
| Estrutura | HTML5 semântico (`index.html`, página única) |
| Estilo | Tailwind CSS via CDN + `<style>` customizado |
| Lógica | JavaScript puro (Vanilla), sem build |
| Ícones | Lucide (CDN) |
| Fontes | Cormorant Garamond (serif) + Plus Jakarta Sans (sans) |
| Deploy | Vercel (`vercel.json`: `cleanUrls`, `trailingSlash: false`) |

## Arquitetura
- SPA de arquivo único: header fixo, hero com Ken Burns, busca (completa / por código), grade de imóveis renderizada via JS, modal de detalhes com mosaico de 5 fotos, drawer de catálogo, modal de contato, newsletter e rodapé.
- Dados dos imóveis ficam em JS dentro do `index.html` (imagens possivelmente em base64, causa do tamanho de ~1 MB).
- Sem backend: formulários são simulados no cliente; WhatsApp via `wa.me`.

## Índice
| Arquivo | Conteúdo |
|---|---|
| [guidelines.md](guidelines.md) | Regras gerais, marca, conteúdo e fluxo de trabalho |
| [architecture.md](architecture.md) | Estrutura atual, alvo e decisões |
| [code-standards.md](code-standards.md) | Padrões de HTML, CSS, JS e acessibilidade |
| [design-system.md](design-system.md) | Cores, tipografia, efeitos |
| [deploy.md](deploy.md) | Publicação e validação |
| [prd-evolucao-producao.md](prd-evolucao-producao.md) | Requisitos para catálogo, CMS, fotos e operação em produção |
| [prd-alteracoes-site-2026-11-13.md](prd-alteracoes-site-2026-11-13.md) | PRD das alterações solicitadas em 13/11/2026 (marca, cor, filtros, textos e nova seção) |

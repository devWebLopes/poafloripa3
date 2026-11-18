# Skill: deploy-vercel

**Objetivo:** publicar com segurança.

## Regras
- Site estático na raiz; sem build command.
- Manter `vercel.json` (`cleanUrls`, `trailingSlash:false`); adicionar headers de cache longo para `/assets/*` (`Cache-Control: public, max-age=31536000, immutable`).
- Testar preview (`npx vercel`) antes de produção (`--prod`).
- Nunca commitar segredos.

## Referências
[../docs/deploy.md](../docs/deploy.md)

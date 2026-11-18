# Plano 002 — PRD de evolução para produção

- **Status:** Concluído
- **Agente líder:** Arquiteto ([agents/arquiteto.md](../agents/arquiteto.md))
- **Apoio:** Conteúdo & Dados, QA & Deploy
- **Skills:** vanilla-js-modular, html-semantico-seo, catalogo-imoveis, otimizacao-imagens, qa-validacao-web, deploy-vercel

## Objetivo

Analisar o repositório atual e documentar os requisitos de produto e arquitetura para transformar a demonstração em um site de produção, com foco no cadastro de imóveis, gestão de textos, armazenamento e envio de fotos e publicação segura.

## Entregáveis

- Diagnóstico do estado atual baseado no repositório.
- PRD em `docs/prd-evolucao-producao.md`.
- Modelo de conteúdo de imóvel e regras para fotos.
- Fluxo editorial de cadastro, revisão, publicação e retirada.
- Comparação das opções de arquitetura e recomendação.
- Roadmap por fases, critérios de aceite, riscos e decisões pendentes.

## Etapas

- [x] Ler as regras, arquitetura, agentes e skills do projeto.
- [x] Inventariar o modelo atual de imóveis, imagens, páginas e formulários.
- [x] Escrever o PRD e registrar premissas sem inventar dados comerciais.
- [x] Atualizar o índice da documentação.
- [x] Validar consistência, links e aderência às regras do projeto.

## Critérios de aceite

- O PRD diferencia claramente estado atual, estado alvo e itens fora de escopo.
- Há uma recomendação objetiva para CMS, banco/API, mídia, autenticação e deploy.
- O cadastro contempla todos os campos atualmente exibidos na página de imóvel.
- O fluxo de fotos contempla upload em lote, ordenação, capa, legendas, otimização e exclusão segura.
- O roadmap permite implementar um MVP antes das melhorias avançadas.
- Decisões que dependem do negócio estão explicitamente marcadas para validação do usuário.

## Validação

- [x] Arquivos Markdown legíveis e sem links locais quebrados.
- [x] Nenhum dado de imóvel, preço ou contato novo foi inventado.
- [x] Nenhuma dependência ou deploy foi executado.

## Riscos

| Risco | Mitigação |
|---|---|
| Escolher tecnologia antes de conhecer orçamento e equipe | Recomendar uma opção e manter alternativas e gatilhos de decisão documentados |
| Transformar o MVP em um CRM completo | Delimitar escopo e fases |
| Upload simples gerar mídia pesada e lenta | Definir pipeline automático, limites e critérios de aceite |
| Expor endereço ou dados internos | Separar campos públicos e privados e adotar controle por papéis |

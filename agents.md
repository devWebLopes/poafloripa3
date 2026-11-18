# agents.md — Ponto de Entrada da IA

## Contexto
**Poa Floripa Imóveis**: site WEB estático (HTML + Tailwind CDN + JavaScript puro) de imóveis de médio/alto padrão **somente para venda** em Porto Alegre e Florianópolis. Deploy na Vercel.

**Objetivos:** vitrine elegante e minimalista, conversão via WhatsApp/contato, performance e manutenção simples.

## Mapa da estrutura
| Pasta | Conteúdo |
|---|---|
| [docs/](docs/README.md) | Arquitetura, padrões, design system, deploy |
| [skills/](skills/README.md) | Habilidades técnicas e regras de negócio |
| [agents/](agents/README.md) | Agentes especializados e quando acioná-los |
| [plans/](plans/) | Planos numerados (`plan-NNN-nome.md`); atual: [plan-001](plans/plan-001-modularizar-index.md) |

## Regras rígidas
1. **Sempre** ler este arquivo e `docs/README.md` antes de iniciar qualquer tarefa ou modificar código.
2. Escolher o agente em `agents/README.md` e carregar as skills dele.
3. Toda tarefa não trivial exige um plano em `plans/` (próximo número sequencial) antes da execução.
4. Seguir `docs/code-standards.md` e `docs/design-system.md`; não adicionar dependências sem aprovação.
5. Preservar paleta, efeitos visuais e a regra "somente venda".
6. Não inventar dados de imóveis, preços ou contatos; perguntar ao usuário.
7. Validar com `skills/qa-validacao-web.md` antes de declarar concluído.
8. Nunca fazer deploy em produção nem apagar arquivos/dados sem confirmação explícita.
9. Ao mudar estrutura ou padrões, atualizar `docs/`, `skills/`, `agents/` e este arquivo.

# Skill: catalogo-imoveis

**Objetivo:** garantir regras de negócio e integridade dos dados.

## Regras
- Somente venda; cidades POA e Floripa; 6 imóveis atuais (3 + 3) — contadores "Todos (6)" devem refletir os dados reais.
- Campos obrigatórios: código, cidade, bairro, tipo, título, preço, condomínio, IPTU, quartos/suítes/vagas/área, descrição, características, 5 fotos.
- Ordenação: recentes, menor valor, maior valor.
- Busca por código exata; mensagem clara quando não encontrado.
- WhatsApp com mensagem pré-preenchida contendo código do imóvel.
- Evitar contadores e textos fixos no HTML: derivá-los dos dados.

## Taxonomia do filtro "Tipos de Imóveis"
O valor interno deve ser igual ao campo `type` do imóvel. Rótulo visível em plural.

| Rótulo visível | Valor interno (`type`) |
|---|---|
| Todas as categorias | `todos` |
| Sobrados | `Sobrado` |
| Coberturas | `Cobertura` |
| Apartamentos | `Apartamento` |
| Casas em Condomínio | `Condomínio` |
| Casas | `Casa` |
| Terrenos | `Terreno` |
| Sala comercial | `Sala Comercial` |
| Lojas | `Loja` |

- `Casa` e `Condomínio` são categorias **distintas** (casa de rua vs. casa em condomínio).
- Categorias sem estoque exibem o estado vazio já existente ("Nenhum imóvel encontrado com estes filtros" + "Limpar filtros"). Não ocultar a opção.
- Não criar imóveis fictícios para preencher categorias sem estoque.

## Referências
[../docs/guidelines.md](../docs/guidelines.md)

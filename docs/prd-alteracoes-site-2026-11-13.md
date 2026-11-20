# PRD — Alterações do site solicitadas em 13/11/2026

- **Produto:** Poa Floripa Imóveis
- **Versão:** 0.3
- **Data desta revisão:** 20/11/2026
- **Status:** Ondas 1, 2 e 3 concluídas, incluindo a marca oficial; Onda 4 com conteúdo publicado e galeria bloqueada. Aguardando validações e fotos para encerramento.
- **Fonte de requisitos:** [levantamento-alteracoes-site-2026-11-13.md](../prds/levantamento-alteracoes-site-2026-11-13.md)
- **Plano relacionado:** [Plano 003](../plans/plan-003-prd-alteracoes-site.md)
- **Backlog:** [tasks.md](../tasks.md) (versão 1.3)
- **Escopo do produto:** site estático de imóveis exclusivamente para venda em Porto Alegre e Florianópolis
- **Base técnica analisada:** `index.html` (~1.357 linhas), `vercel.json`, `docs/`, `agents/`, `skills/`

> Este PRD **não** é um redesenho. Ele converte os 9 pedidos do levantamento em requisitos verificáveis e separa, de forma explícita, o que está **concluído**, o que **exige definição do cliente** e o que está **bloqueado ou fora de escopo**. Nenhum dado de imóvel, preço ou contato foi inventado.

---

## 0. Controle de versões

| Versão | Data | Mudança |
|---|---|---|
| 0.1 | 18/11/2026 | Primeira proposta: requisitos, decisões, bloqueios e fora de escopo, a partir do levantamento de 13/11/2026 e da inspeção do `index.html`. |
| **0.2** | **19/11/2026** | Consolidação da execução das Ondas 1–4: status real por requisito, decisões D-01 a D-15 atualizadas, evidências de QA, pendências de encerramento, achados de conformidade fora do escopo e critérios de conclusão. |
| **0.3** | **20/11/2026** | D-01 resolvida: marca oficial (opção 2, "IMÓVEIS" branco) aplicada direto sobre o azul no header e no rodapé. RF-01 e A-01 concluídos; B-01 encerrado. |

### 0.1 O que mudou da 0.1 para a 0.2

1. **Status por requisito:** RF-02, RF-04, RF-05, RF-06, RF-07, RF-09 e RF-10 concluídos no código; RF-01 e RF-03 concluídos com ressalva; RF-08 concluído em conteúdo e bloqueado na galeria.
2. **Decisões fechadas:** D-02, D-03, D-04, D-05, D-06, D-07, D-09 e D-13 registradas como resolvidas.
3. **Decisões ainda abertas:** D-01 (ativo da marca), D-08 (fotos), D-10 (item de menu), D-11 (validação jurídica/factual), D-12 (telefone vigente), D-14 e D-15 (governança).
4. **Evidências de QA incorporadas:** testes de interação, responsividade e Lighthouse de 18/11/2026.
5. **Nova seção 13:** pendências de encerramento com responsável, impacto e critério de aceite.
6. **Nova seção 14:** achados de conformidade identificados no código que **não** pertencem a esta entrega, mas precisam de decisão antes do uso institucional do site.

---

## 1. Resumo executivo

O site vigente é uma SPA de arquivo único (`index.html`) com HTML, CSS, dados de imóveis (base64) e JavaScript no mesmo arquivo. As solicitações de 13/11/2026 são **ajustes editoriais e de identidade visual**, não uma reestruturação:

| # | Pedido | Natureza | Esforço | Situação em 19/11/2026 |
|---|---|---|---|---|
| ALT-01 | Nova logomarca com "IMÓVEIS" centralizado | Identidade visual | Médio | ✅ Marca oficial aplicada em 20/11/2026 |
| ALT-02 | Remover "Explorar Imóveis de Luxo" da barra | Navegação | Baixo | ✅ Concluído |
| ALT-03 | Clarear o azul para "azul piscina" | Design system | Médio | ✅ Concluído com exceção de contraste registrada |
| ALT-04 | 4 novas categorias no filtro | Funcional | Baixo | ✅ Concluído |
| ALT-05 | Novo texto de contato + remover CTA | Conteúdo/UI | Baixo | ✅ Concluído |
| ALT-06 | Novo título e subtítulo do hero | Conteúdo/SEO | Baixo | ✅ Concluído |
| ALT-07 | "Quem é Poa Floripa" → "Sobre Nós" | Conteúdo/UI | Baixo | ✅ Código concluído; publicação condicionada a D-11 |
| ALT-08 | Nova seção final POA + Floripa | Feature nova | Alto | 🟡 Texto no ar; galeria bloqueada (A-03) |
| ALT-09 | Manter o telefone atual | Verificação | Baixo | ✅ Auditoria concluída; aceite de negócio em D-12 |

**Achados de engenharia relevantes:**

1. **A cor solicitada já existia como token.** `pool.DEFAULT = #00B4D8` já era um "azul piscina". O que escurecia a barra era o gradiente `#00B4D8 → #0099BA → #007791`. A solução adotada foi um token exclusivo da barra (`pool.bar = #12B8D8`), sem tocar nos demais azuis.
2. **O azul claro não sustenta texto branco em AA.** O solicitante rejeitou o texto petróleo e pediu branco de volta. O contraste ficou em 2,29:1–3,20:1, abaixo de AA. A exceção está registrada em `docs/design-system.md` e continua sendo dívida de acessibilidade.
3. **O drawer do catálogo perdeu acesso no desktop.** Com ALT-02 + ALT-05, as duas entradas visíveis foram removidas. O drawer continua acessível pelo botão "Menu" no mobile (`lg:hidden`); a perda no desktop foi aceita em D-04.
4. **A logomarca agora é imagem.** O ativo `assets/img/logo-poa-floripa-imoveis.png` (720×148, transparência) substituiu a composição CSS no header e no rodapé. Os originais recebidos tinham fundo preto; foram recortados e tratados.
5. **Existem dois telefones publicados:** `(51) 99999-0149` (Porto Alegre) e `(48) 99999-0240` (Florianópolis). "Manter o telefone atual" foi tratado como "não alterar nenhum dos dois".
6. **A galeria não pode ser publicada com as imagens recebidas.** Duas das quatro referências têm marca do Google Lens e a licença é desconhecida.
7. **A seção histórica foi entregue sem interação.** D-07 decidiu texto sempre visível; o bloco de revelar por clique não se aplica.
8. **O logo branco sobre a barra clara mantém a exceção de contraste.** A opção aprovada tem "IMÓVEIS" branco e foi aplicada direto sobre `#12B8D8` (2,37:1), coerente com a decisão D-03.

---

## 2. Escopo

### 2.1 Dentro do escopo

- Ajustes de conteúdo textual nos pontos explicitamente citados.
- Ajustes de navegação, filtros e CTAs citados.
- Evolução controlada do design system de cor (token único da barra).
- Nova seção editorial ao final do conteúdo principal.
- Correções derivadas **estritamente necessárias** para não quebrar o que já funciona (SEO técnico, acessibilidade, responsividade, estados vazios).

### 2.2 Fora do escopo

Ver seção 10.2 (lista completa e justificada).

### 2.3 Princípio de não-ampliação

Conforme o levantamento (seção 9, item 3): **não** expandir automaticamente "Porto Alegre e Florianópolis" para "Rio Grande do Sul e Santa Catarina" em outros textos. A alteração geográfica vale apenas para a chamada de contato (ALT-05), salvo aprovação explícita.

---

## 3. Diagnóstico do estado vigente

Situação conferida no `index.html` em 19/11/2026:

| Requisito | Componente real | Localização atual | Situação |
|---|---|---|---|
| ALT-01 | Logo no header e no rodapé | header e rodapé | Imagem oficial em `<img>`, "IMÓVEIS" branco centralizado |
| ALT-02 | `<nav>` desktop | menu minimalista | 4 links; item removido; título do drawer preservado de propósito |
| ALT-03 | Tokens `pool.bar` + `--pool-bar-*` | `tailwind.config` e `:root` | Barra `#12B8D8` com gradiente claro e texto branco |
| ALT-04 | `<select id="filterType">` | L349-359 | 9 opções: `todos`, Sobrado, Cobertura, Apartamento, Condomínio, Casa, Terreno, Sala Comercial, Loja |
| ALT-05 | Faixa de consultoria | L454-465 | Título novo; CTA único "Falar com Especialista" |
| ALT-06 | Hero `<h1>` + subtítulo | L298-302 | Textos novos; um único `<h1>` |
| ALT-07 | Seção `#quemSomos` | L502-510 | "Sobre Nós", texto integral, sem os três pilares |
| ALT-08 | `#duasCapitais` | L518-556 | Título + 4 parágrafos no ar; galeria como bloco comentado |
| ALT-09 | Telefones | header, rodapé, modais, JS | Números originais mantidos; paridade exibido ↔ `wa.me` confirmada |

**Dados disponíveis para o filtro:** 6 imóveis — 2 `Sobrado`, 1 `Cobertura`, 1 `Condomínio`, 2 `Apartamento`. **Nenhum** imóvel nas 4 categorias novas.

**Estado vazio:** já implementado em `renderProperties()`. Incluir categorias sem estoque **não gera tela quebrada** — retorna a mensagem "Nenhum imóvel encontrado com estes filtros" e o botão "Limpar filtros".

---

## 4. Premissas e decisões

### 4.1 Premissas de engenharia (não são decisões de negócio)

| ID | Premissa | Justificativa |
|---|---|---|
| P-01 | Manter arquitetura sem build, Tailwind CDN e JS puro | `docs/architecture.md`; regra 4 do `agents.md` |
| P-02 | Não introduzir dependências novas | regra 4 do `agents.md` |
| P-03 | Cores apenas via tokens (`pool`, `minimal`, `brand`) | `docs/code-standards.md` |
| P-04 | Preservar efeitos assinatura (Ken Burns, float, lag, mosaico) | `docs/design-system.md` |
| P-05 | Não criar dados de imóvel para preencher as novas categorias | regra 6 do `agents.md` |
| P-06 | Textos fornecidos por Tiago são transcritos literalmente, sem revisão editorial não aprovada | levantamento seção 5 |
| P-07 | Um único `<h1>` na página | `docs/code-standards.md` |

### 4.2 Decisões — status atualizado

| ID | Pergunta | Impacta | Status em 19/11/2026 |
|---|---|---|---|
| **D-01** | Qual é o arquivo final da marca (SVG ou PNG transparente)? | ALT-01 | ✅ **Resolvido em 20/11/2026:** opção 2 ("IMÓVEIS" branco) aplicada direto sobre o azul. Ativo de produção: PNG 720×148 com transparência. SVG continua recomendado para o futuro, mas não bloqueia. |
| **D-02** | O novo azul vale só para a barra ou para toda a identidade? | ALT-03 | ✅ **Resolvido:** barra superior apenas. CTAs, links, rodapé e `pool-secondary` permanecem `#00B4D8` / `#007791`. |
| **D-03** | Qual o valor final do azul e a combinação de contraste? | ALT-03 | ✅ **Resolvido:** barra `#12B8D8` com texto **branco**, por pedido do solicitante. Contraste 2,29:1–3,20:1, abaixo de AA. Exceção registrada em `docs/design-system.md`. |
| **D-04** | O acesso ao catálogo deve continuar no desktop após remover o item de menu e o CTA? | ALT-02, ALT-05 | ✅ **Resolvido:** as duas entradas foram removidas. Drawer permanece pelo botão "Menu" no mobile. Perda no desktop aceita explicitamente. |
| **D-05** | O rótulo "Curadoria" do menu deve virar "Sobre Nós"? | ALT-07 | ✅ **Resolvido:** menu passou a "Sobre Nós"; `id="quemSomos"` preservado para a âncora. |
| **D-06** | Taxonomia final das categorias | ALT-04 | ✅ **Resolvido:** ordem Sobrados, Coberturas, Apartamentos, Casas em Condomínio, Casas, Terrenos, Sala comercial, Lojas. Valores internos: `Sobrado`, `Cobertura`, `Apartamento`, `Condomínio`, `Casa`, `Terreno`, `Sala Comercial`, `Loja`. |
| **D-07** | A seção histórica abre com texto sempre visível ou sob clique? | ALT-08 | ✅ **Resolvido:** texto sempre visível. |
| **D-08** | Quantidade e composição final da galeria | ALT-08 | 🟡 **Parcial:** composição definida (3–4 POA + ~3 FLN, mínimo 2 de Florianópolis). Fotos licenciadas ainda não chegaram. |
| **D-09** | A nova seção entra depois de "Sobre Nós" ou depois da newsletter? | ALT-08 | ✅ **Resolvido:** depois de "Sobre Nós", antes da newsletter (`#contatoSection`). |
| **D-10** | Haverá item de menu apontando para a nova seção? | ALT-08 | ⏳ **Não decidido formalmente.** Nenhum item foi criado. A seção é alcançável por rolagem. |
| **D-11** | Os textos institucionais foram validados jurídica e factualmente? | ALT-07, ALT-08 | ⏳ **Aberto.** Bloqueia a publicação em produção (G-02). |
| **D-12** | Qual telefone é "o atual" — 51, 48 ou ambos? | ALT-09 | ⏳ **Aberto para aceite de negócio.** Nenhum número foi alterado. |
| **D-13** | Autoriza atualizar `<title>`, `meta description` e Open Graph? | ALT-06 | ✅ **Resolvido** para `title` e `description`. Open Graph não existe no arquivo e não foi criado. |
| **D-14** | O levantamento está duplicado em `prds/` e `docs/`. Qual é a fonte única? | Governança | ⏳ **Aberto.** As duas cópias seguem idênticas. |
| **D-15** | Onde estão os anexos citados no levantamento? | Todos | 🟡 **Parcial.** Localizados em `D:\clientes\poafloripa\conversas`, fora do repositório e sem versionamento. |

---

## 5. Requisitos funcionais

### RF-01 — Logomarca com "IMÓVEIS" centralizado (ALT-01) — ✅ concluído

**Requisito.** Exibir a marca "POA + ícone de casa + FLORIPA" com "IMÓVEIS" em segunda linha, **visualmente centralizado** em relação ao conjunto superior, no header e no rodapé.

**Implementado:**
- Ativo oficial `assets/img/logo-poa-floripa-imoveis.png` (720×148, PNG com transparência, 41 KB), aplicado como `<img>` no header e no rodapé, direto sobre o azul.
- Header: `h-[46px]` no mobile e `h-[54px]` a partir de `sm`; rodapé: `h-12`.
- `alt="Poa Floripa Imóveis"` nos dois pontos; link da marca continua resetando os filtros.
- Composição CSS provisória removida.

**Aceite:**
- [x] "IMÓVEIS" centralizado sob o conjunto, no header e no rodapé.
- [x] Marca legível em 375, 768 e 1280 px, sem corte nem deformação.
- [x] Nome acessível presente; link da marca continua resetando filtros.
- [x] Header não sobrepõe o hero.
- [x] Ativo final aprovado e aplicado.

**Observação:** o PNG foi gerado a partir do original de 2172×724 com fundo preto. Para uso em impressão ou grandes formatos, o SVG continua sendo o formato ideal.

---

### RF-02 — Remover "Explorar Imóveis de Luxo" da navegação (ALT-02) — ✅ concluído

**Requisito.** Remover o item textual da barra azul e reequilibrar o espaçamento dos quatro itens restantes.

**Implementado:** item removido; nav desktop com 4 links (`Página inicial`, `Imóveis Selecionados`, `Sobre Nós`, `Contato`). O título interno do drawer foi mantido — é cabeçalho do catálogo, não item de navegação.

**Aceite:**
- [x] O texto não aparece na navegação em nenhuma largura.
- [x] Links restantes alinhados e funcionais; `active` funcionando em "Página inicial".
- [x] Console limpo; nenhum handler órfão.
- [x] Drawer acessível pela entrada definida em D-04.

---

### RF-03 — Azul piscina mais claro (ALT-03) — ✅ concluído com exceção

**Requisito.** Tornar o azul perceptivelmente mais claro, próximo da referência, aplicando a mudança de forma **sistêmica via tokens**.

**Implementado:**
- Token `pool.bar = #12B8D8`, exclusivo da barra.
- Variáveis `--pool-bar-start #14BBDC`, `--pool-bar #12B8D8`, `--pool-bar-end #0E9CC4`, `--pool-bar-ink #072A36`.
- Gradiente do header migrado para as variáveis; estado `scrolled` com `rgba(16,169,210,0.96)`, blur e borda petróleo.
- Nenhum CTA, link, rodapé ou `pool-secondary` alterado.

**Contraste medido:**

| Combinação | Contraste | AA texto normal (4,5:1) | AA texto grande (3:1) |
|---|---|---|---|
| Branco sobre `#14BBDC` | 2,29:1 | Reprovado | Reprovado |
| Branco sobre `#12B8D8` | 2,37:1 | Reprovado | Reprovado |
| Branco sobre `#0E9CC4` | 3,20:1 | Reprovado | Aprovado |
| Petróleo `#072A36` sobre `#12B8D8` (versão anterior) | 6,37:1 | Aprovado | Aprovado |

**Decisão vigente:** o solicitante rejeitou o texto petróleo e pediu branco. A exceção está documentada. Se quiser AA com texto branco, a barra precisa escurecer para ~`#07809B` — decisão pendente de negócio, não de código.

**Aceite:**
- [x] Azul visivelmente mais claro e aderente à referência aprovada.
- [x] Estados interativos distinguíveis; nenhum hex órfão.
- [x] `docs/design-system.md` atualizado com o valor final.
- [ ] Contraste mínimo AA comprovado nos textos da barra e CTAs.

---

### RF-04 — Novas categorias no filtro (ALT-04) — ✅ concluído

**Requisito.** Acrescentar **Casas**, **Terrenos**, **Sala comercial** e **Lojas** ao seletor "Tipos de Imóveis", preservando as opções atuais.

**Implementado:** 9 opções no seletor, com valores internos estáveis `Casa`, `Terreno`, `Sala Comercial` e `Loja`. Taxonomia registrada em `skills/catalogo-imoveis.md`.

**Aceite:**
- [x] 4 novas opções visíveis em desktop e mobile.
- [x] `todos` restaura a lista completa.
- [x] Combinação categoria + localidade + ordenação correta.
- [x] Nenhuma duplicidade semântica não documentada entre `Casa` e `Condomínio`.
- [x] Estado vazio com "Limpar filtros" funcional.
- [x] Console limpo.

---

### RF-05 — Chamada de contato (ALT-05) — ✅ concluído

**Requisito.** Título passa a "Quer encontrar seu próximo imóvel no Rio Grande do Sul ou Santa Catarina?" e o CTA "Explorar Acervo Completo" é removido **daquela seção**.

**Implementado:** título novo, um único CTA centralizado ("Falar com Especialista"), container sem `flex-wrap`. `openCatalogDrawer()` permanece no código.

**Aceite:**
- [x] Novo título exato, sem resquício de "Porto Alegre ou Florianópolis" nessa seção.
- [x] Apenas um CTA, centralizado e equilibrado.
- [x] Modal de contato abre com o assunto "Consultoria Personalizada — Porto Alegre & Florianópolis".
- [x] Linha de apoio inalterada.

---

### RF-06 — Título e subtítulo da abertura (ALT-06) — ✅ concluído

**Requisito.**
- Título: "Imóveis de Médio e Alto Padrão em Porto Alegre e Florianópolis"
- Subtítulo: "Curadoria imobiliária para quem busca sofisticação, localização privilegiada e qualidade de vida"

**Aceite:**
- [x] Textos exatos no hero.
- [x] Quebra de linha adequada em 375, 768 e 1280 px.
- [x] Um único `<h1>`.
- [x] Nenhuma ocorrência de "Curadoria exclusiva" no hero.

---

### RF-07 — "Sobre Nós" (ALT-07) — ✅ concluído em código

**Requisito.** Trocar o título da seção `#quemSomos`, substituir os parágrafos pelo texto aprovado e remover integralmente o bloco `<ul>` de três pilares.

**Implementado:** título "Sobre Nós", texto integral do levantamento (seção 5.3), três pilares removidos, `id="quemSomos"` preservado e menu atualizado.

**Aceite:**
- [x] Título "Sobre Nós"; texto integral; três tópicos ausentes.
- [x] Layout equilibrado em 375, 768 e 1280 px.
- [x] Header/nav sem link quebrado.
- [x] Nenhuma alegação nova além do texto fornecido.
- [ ] Validação jurídica/factual antes de publicar (D-11).

---

### RF-08 — Seção final "De Porto Alegre a Florianópolis" (ALT-08) — 🟡 conteúdo concluído, galeria bloqueada

**Requisito.** Criar uma seção editorial, com título e quatro parágrafos aprovados e galeria de imagens das duas capitais, posicionada como última seção de conteúdo do site.

**Implementado:**
- `section#duasCapitais` entre "Sobre Nós" e a newsletter.
- Título e 4 parágrafos literais, conferidos caractere a caractere contra o levantamento.
- Eyebrow "Porto Alegre & Florianópolis", primeiro parágrafo em destaque, dois parágrafos em grade de 2 colunas no desktop e fechamento com barra lateral petróleo.
- Texto sempre visível (D-07); nenhuma interação de revelar.
- Bloco comentado no HTML com os requisitos da futura galeria.

**Aceite:**
- [x] Seção presente na posição aprovada, com título e 4 parágrafos literais.
- [x] Legível em 375 px sem bloco denso.
- [x] Sem interação quebra ou erro de console.
- [ ] Galeria com a distribuição mínima acordada e identificação correta.
- [ ] Imagens licenciadas, sem marcas de ferramenta, com `alt`.
- [ ] Fatos históricos e alegações validados (D-11).

**Dependências:** D-08, A-03 e D-11.

---

### RF-09 — Manter telefone atual (ALT-09) — ✅ auditoria concluída

**Requisito.** Não substituir os números publicados; garantir consistência entre número exibido e destino do `wa.me`.

**Inventário:**

| Ponto | Número exibido | Destino do link | Paridade |
|---|---|---|---|
| Header | (48) 99999-0240 | `wa.me/5548999990240` | OK |
| Rodapé, coluna Contato | (51) 99999-0149 e (48) 99999-0240 (texto) | sem link | OK (apenas texto) |
| Modal de cidades — Porto Alegre | (51) 99999-0149 | `wa.me/5551999990149` + mensagem POA | OK |
| Modal de cidades — Florianópolis | (48) 99999-0240 | `wa.me/5548999990240` + mensagem FLN | OK |
| `openPropertyModal` | não exibe número | 51 se POA, 48 se FLN | OK |

**Aceite:**
- [x] Números exibidos iguais aos links `wa.me` correspondentes.
- [x] Nenhum número novo introduzido.
- [ ] Divergência 51/48 esclarecida como decisão de negócio (D-12).

---

### RF-10 — Consistência de SEO (derivado de ALT-06) — ✅ concluído

**Implementado:**
- `title`: "Poa Floripa Imóveis | Médio e Alto Padrão em POA e Floripa" (58 caracteres).
- `description`: 136 caracteres, com "Curadoria imobiliária" e sem "exclusiva".
- Nenhuma tag Open Graph criada.

**Aceite:**
- [x] Metadados refletem "Médio e Alto Padrão" e "Curadoria imobiliária".
- [x] Sem meta description duplicada ou ausente.
- [x] Nenhuma mudança de URL/estrutura.

---

## 6. Requisitos não funcionais — resultado medido

| ID | Requisito | Critério verificável | Status em 19/11/2026 |
|---|---|---|---|
| RNF-01 | Acessibilidade AA | Contraste ≥ 4,5:1 (normal) e ≥ 3:1 (grande); foco visível; teclado | ⚠️ **Parcial:** foco e teclado OK; contraste da barra reprovado por decisão do solicitante |
| RNF-02 | Responsividade | Sem overflow, corte ou sobreposição em 375/768/1280 px | ✅ 0 de overflow nas seções alteradas |
| RNF-03 | Performance | Sem novas dependências; imagens WebP com dimensões e lazy loading | ⚠️ **Não atingido:** Lighthouse Performance 25 (base64 + Tailwind CDN) |
| RNF-04 | SEO técnico | Um `<h1>`; `title`/`description` coerentes; conteúdo indexável | ✅ Lighthouse SEO 100 |
| RNF-05 | Consistência visual | Cores só por tokens; efeitos assinatura intactos | ✅ |
| RNF-06 | Sem backend | Nenhuma chamada de API, formulário real ou serviço novo | ✅ |
| RNF-07 | Rastreabilidade | Cada texto publicado corresponde ao levantamento | ✅ comparação automatizada 5/5 na seção histórica |
| RNF-08 | Regressão funcional | Filtros, busca, modal, lightbox, drawer, formulários e WhatsApp operando | ✅ testado em duas rodadas |
| RNF-09 | Manutenibilidade | Alterações localizadas e comentadas; sem refatoração ampla | ✅ |
| RNF-10 | Console limpo | Zero erros e warnings relevantes | ⚠️ Zero erros; resta apenas o aviso do Tailwind CDN (o 404 de `favicon.ico` foi resolvido em 20/11/2026 com os favicons da marca) |

**Lighthouse 12 (18/11/2026, Chrome headless, servidor local):** Performance **25** · Acessibilidade **96** · Boas Práticas **96** · SEO **100**. FCP 11,3 s e LCP 11,6 s por causa dos 1,59 MB de página com imagens em base64. Corrigir isso exige mudar o modelo de mídia e pertence ao [PRD de evolução para produção](prd-evolucao-producao.md).

---

## 7. Priorização e ondas — status

### 7.1 Por complexidade × prontidão

| Complexidade | Concluído | Concluído com ressalva | Bloqueado por ativo externo |
|---|---|---|---|
| **Baixa** | RF-02, RF-04, RF-05, RF-06, RF-07, RF-09, RF-10 | — | — |
| **Média** | RF-01 | RF-03 | — |
| **Alta** | — | RF-08 (conteúdo) | RF-08 (galeria) |

### 7.2 Ondas

- **Onda 1 — Conteúdo e filtros:** RF-05, RF-06, RF-04, RF-07, RF-09, RF-02, RF-10. ✅ Executada em 18/11/2026.
- **Onda 2 — Navegação e cor:** RF-02, RF-03. ✅ Executada em 18/11/2026, com revisão de contraste posterior.
- **Onda 3 — Marca:** RF-01. ✅ Executada em código em 18/11/2026 e concluída em 20/11/2026 com a marca oficial.
- **Onda 4 — Seção editorial:** RF-08. 🟡 Texto publicado em 18/11/2026; galeria bloqueada pelas fotos.

### 7.3 Ordem de valor para o cliente (inalterada)

| Ordem | Requisito | Valor | Risco técnico | Situação |
|---|---|---|---|---|
| 1 | RF-05 | Alto | Baixo | ✅ |
| 2 | RF-06 | Alto | Baixo | ✅ |
| 3 | RF-04 | Alto | Baixo | ✅ |
| 4 | RF-02 | Médio | Baixo | ✅ |
| 5 | RF-07 | Alto | Baixo | ✅ (gate D-11) |
| 6 | RF-09 | Médio | Baixo | ✅ (aceite D-12) |
| 7 | RF-10 | Médio | Baixo | ✅ |
| 8 | RF-03 | Alto | Médio | ✅ (exceção AA) |
| 9 | RF-01 | Alto | Médio | ✅ |
| 10 | RF-08 | Alto | Alto | 🟡 (A-03) |

---

## 8. Dependências de ativos e informações

| ID | Necessário | Para | Status |
|---|---|---|---|
| A-01 | Marca em SVG ou PNG com transparência, alta resolução, versão final aprovada | RF-01 | ✅ **Resolvido em 20/11/2026:** PNG 720×148 aplicado; SVG opcional para o futuro |
| A-02 | Confirmação do hex final + escopo de aplicação | RF-03 | ✅ **Resolvido** (`#12B8D8`, barra apenas) |
| A-03 | 3–4 fotos de Porto Alegre e ~3 de Florianópolis, licenciadas, sem marca d'água | RF-08 | ⛔ **Bloqueante** |
| A-04 | Definição de layout da seção histórica | RF-08 | ✅ **Resolvido:** texto sempre visível, blocos editoriais |
| A-05 | Validação jurídica e factual dos textos | RF-07, RF-08 | ⏳ **Ausente** |
| A-06 | Confirmação de qual telefone é o vigente | RF-09 | 🟡 **Parcial:** nenhum número alterado; decisão de negócio pendente |
| A-07 | Anexos do levantamento (imagens, áudios, transcrição, `poafloripa6.html`) | Auditoria | 🟡 **Localizados fora do repositório**, não versionados |
| A-08 | Wireframe ou referência visual da galeria | RF-08 | ✅ **Resolvido:** grid 1 coluna no mobile, composição editorial no desktop (comentário no HTML) |

---

## 9. Registro de QA

Base: `skills/qa-validacao-web.md`. Testes executados em 18/11/2026, em servidor local.

| Verificação | Resultado |
|---|---|
| Console (Chrome headless) | zero erros; aviso do Tailwind CDN (o 404 de `favicon.ico`, medido em 18/11/2026, foi resolvido em 20/11/2026) |
| Filtros: 9 opções | OK |
| 4 novas categorias | 0 cards + estado vazio com "Limpar filtros" |
| "Limpar filtros" | restaura os 6 imóveis |
| Combinação Condomínio + Porto Alegre + maior valor | 1 card |
| `resetAllFilters()` | 6 cards, tipo e localização em `todos` |
| Um único `<h1>` | OK |
| Responsivo 375 / 768 / 1280 px | sem overflow ou sobreposição |
| Telefones/`wa.me` | paridade em todos os pontos; nenhum número novo |
| Modal do imóvel | 5 fotos, 5 specs, 6 características, `wa.me` da cidade correta |
| Lightbox | abre na foto 3/5, legenda correta, fecha por botão |
| `Esc` em modal e drawer | fecha os dois e restaura `body.style.overflow` |
| Drawer | 3 imóveis de POA + 3 de FLN |
| CTA "Falar com Especialista" | abre o modal com o assunto correto |
| Formulário de contato | "Solicitação enviada..." e fecha em 2 s |
| Newsletter | feedback de sucesso |
| Teclado | foco visível nos `select` |
| Marca no header/rodapé | imagem 720×148 aplicada em 20/11/2026; 375/768/1280 px sem overflow |
| Texto da seção histórica | 5/5 idênticos ao levantamento |
| Marca no header | 54 px em header de 81 px; "IMÓVEIS" a 1 px do centro óptico |
| Marca no rodapé | mesma composição, sem divergência |
| Lighthouse | Performance 25 · A11y 96 · BP 96 · SEO 100 |

---

## 10. Limitações, bloqueios e fora de escopo

### 10.1 Bloqueios

| ID | Bloqueio | Consequência | Como destravar | Status |
|---|---|---|---|---|
| B-01 | Marca final inexistente em formato de produção | RF-01 não pode ser concluído com qualidade | Tiago envia SVG/PNG aprovado | ✅ Resolvido em 20/11/2026 |
| B-02 | Imagens da seção histórica com marca do Google Lens e licença não comprovada | Publicação ilegal ou visualmente inadequada | Substituir por fotos próprias ou licenciadas | ⏳ Aberto |
| B-03 | Conflito entre "clarear o azul" e contraste AA com texto branco | AA não atendido na barra | Escurecer a barra para ~`#07809B` ou aceitar a exceção | ✅ Resolvido por exceção aprovada |
| B-04 | Perda de acesso ao drawer no desktop | Funcionalidade existente deixa de ser alcançável no desktop | Reintroduzir entrada ou aceitar a perda | ✅ Resolvido: perda aceita em D-04 |
| B-05 | Alegações institucionais não validadas | Risco jurídico/reputacional | Validação de Tiago/jurídico (D-11) | ⏳ Aberto |
| B-06 | Anexos-fonte ausentes no repositório | Impossível auditar pelo repositório | Versionar os anexos | 🟡 Parcial (existem fora do repo) |
| B-07 | Ambiguidade dos dois telefones publicados | Aceite de RF-09 inconclusivo | Esclarecer D-12 | ⏳ Aberto |

### 10.2 Fora de escopo (não implementar nesta entrega)

1. Redesenho completo do site ou mudança de identidade além da marca e do azul.
2. Remoção geral do catálogo, do drawer, do modal ou de imóveis.
3. Troca de número de telefone, e-mail, CRECI ou redes sociais.
4. Expansão automática de "Porto Alegre e Florianópolis" para "Rio Grande do Sul e Santa Catarina" em outros textos.
5. Definição de novo formato de galeria para os imóveis ou do mosaico de 5 fotos.
6. Migração para CMS, banco de dados, API, backend ou formulários reais (tema do `docs/prd-evolucao-producao.md`).
7. Modularização do `index.html` em `assets/css`, `assets/js` (plan-001).
8. Extração das imagens base64 para arquivos, salvo se estritamente necessário para RF-08.
9. Revisão editorial dos textos do cliente (copywriting, gramática, SEO editorial).
10. Novas animações, novos efeitos ou novas dependências.
11. Alterações na newsletter, no rodapé, no modal de contato ou no WhatsApp flutuante não solicitadas.
12. Inclusão das imagens `WA0057`, `WA0059` e `WA0061` (sem vínculo com requisito).
13. Deploy em produção.
14. Aquisição/compra de licenças de imagem pela equipe de desenvolvimento.
15. Publicação de conteúdo com marca d'água de ferramenta de busca.

### 10.3 Limitações técnicas conhecidas

| ID | Limitação | Impacto |
|---|---|---|
| L-01 | Arquivo único de ~1 MB com base64 | Edições exigem cuidado; novas imagens não devem entrar em base64 |
| L-02 | Tailwind CDN sem build | Sem purge/JIT local; tokens dependem do `tailwind.config` inline |
| L-03 | Header fixo `h-20` + hero `h-[500px]` | Textos mais longos podem estourar no mobile |
| L-04 | Logo duplicada manualmente (header e rodapé) | Risco de divergência a cada alteração |
| L-05 | Sem testes automatizados | Validação é manual, via `skills/qa-validacao-web.md` |
| L-06 | Menu mobile não é navegação | O botão "Menu" abre o drawer do catálogo |
| L-07 | Link do Gemini exige autenticação | Referência da marca não é verificável |

---

## 11. Rastreabilidade

| Origem | Requisito | Decisões | Ativos | Bloqueio | Situação |
|---|---|---|---|---|---|
| ALT-01 | RF-01 | D-01 | A-01 | B-01 | ✅ |
| ALT-02 | RF-02 | D-04 | — | B-04 | ✅ |
| ALT-03 | RF-03 | D-02, D-03 | A-02 | B-03 | ✅ com exceção |
| ALT-04 | RF-04 | D-06 | — | — | ✅ |
| ALT-05 | RF-05 | D-04 | — | B-04 | ✅ |
| ALT-06 | RF-06, RF-10 | D-13 | — | — | ✅ |
| ALT-07 | RF-07 | D-05, D-11 | A-05 | B-05 | ✅ código / ⏳ publicação |
| ALT-08 | RF-08 | D-07, D-08, D-09, D-10, D-11 | A-03, A-04, A-08 | B-02, B-05 | 🟡 |
| ALT-09 | RF-09 | D-12 | A-06 | B-07 | ✅ código / ⏳ aceite |
| Governança | — | D-14, D-15 | A-07 | B-06 | ⏳ |

---

## 12. Critérios de encerramento da entrega

A entrega só pode ser considerada concluída quando **todos** os itens abaixo forem verdadeiros:

| # | Critério | Responsável | Verificação |
|---|---|---|---|
| 1 | Ativo final da marca aplicado no header e no rodapé | Tiago + `@frontend-dev` | ✅ **Concluído em 20/11/2026** — PNG aprovado; comparado em 375/768/1280 px |
| 2 | Galeria da seção histórica publicada com 3–4 fotos de POA e ≥2 de FLN | Tiago + `@frontend-dev` | Imagens licenciadas, sem marca d'água, com `alt` e WebP |
| 3 | Textos institucionais validados jurídica e factualmente | Tiago/jurídico | D-11 registrada como aprovada |
| 4 | Telefone vigente definido (51, 48 ou ambos) | Tiago | D-12 registrada |
| 5 | Endereço das duas cópias do levantamento definido | Evandro | D-14 registrada |
| 6 | Anexos versionados ou referenciados de forma estável | Evandro | D-15 registrada |
| 7 | QA final sem regressão | `@qa-engineer` | Checklist da seção 9 repetido no build final |
| 8 | Deploy aprovado explicitamente | Tiago/Evandro | Regra 8 do `agents.md` |

**Itens que não bloqueiam o encerramento, mas devem ser transferidos para o PRD de evolução:**

- Contraste AA da barra (RNF-01) — depende de decisão visual do cliente.
- Performance (RNF-03) — depende de sair do base64 e do Tailwind CDN.
- ~~`favicon.ico` ausente — 404 no console.~~ ✅ Resolvido em 20/11/2026 (ver C-04).

---

## 13. Achados de conformidade fora do escopo

Identificados ao conferir o `index.html` em 19/11/2026. **Não são requisitos desta entrega** (ver 10.2, item 3), mas afetam a confiabilidade institucional do site e devem ser decididos antes de divulgá-lo como site oficial de uma imobiliária registrada.

| # | Achado | Evidência | Risco | Recomendação |
|---|---|---|---|---|
| C-01 | Rodapé exibe "CRECI RS/SC" **sem número** | `index.html` L643 | Descumpre a regra de exibição do CRECI/SC informada pelo cliente (sigla + número + sufixo J, com no mínimo 25% da altura do nome) | Publicar **"CRECI/SC 12028-J"** no rodapé e nas peças de divulgação |
| C-02 | Rodapé não exibe CNPJ, razão social nem endereço | `index.html` L642-645 | Enfraquece a identificação da pessoa jurídica e a confiança do usuário | Incluir "TSR Assessoria Empresarial Ltda · CNPJ 49.975.398/0001-70 · Rua Procópio Manoel Pires, 84 — Trindade, Florianópolis/SC" |
| C-03 | Telefones publicados são placeholders (`99999-…`) | header, rodapé, modais | Passa impressão de contato falso | Substituir pelos números reais quando o chip for adquirido (D-12) |
| C-04 | `favicon.ico` ausente | 404 no console | Ruído técnico e perda de identidade na aba | ✅ **Resolvido em 20/11/2026:** casinha da marca vetorizada (`favicon.svg`, `favicon.ico`, `favicon-96x96.png` e `apple-touch-icon.png` em `assets/img/`), declaradas no `<head>` |
| C-05 | Performance 25 no Lighthouse | 1,59 MB, imagens em base64, Tailwind CDN | Experiência ruim em mobile e prejuízo a SEO | Tratar no PRD de evolução (conteúdo + mídia) |

> **Observação:** C-01 e C-02 são os achados de maior impacto prático. O dossiê institucional (`dossie-poa-floripa-imoveis.md`) já os classificava como divergências críticas.

---

## 14. Próximos passos

1. ~~**Tiago envia A-01** (SVG/PNG transparente da marca) → executar G2-TASK-01.~~ ✅ Concluído em 20/11/2026.
2. **Tiago envia A-03** (fotos licenciadas de POA e FLN) → executar G3-TASK-02/03.
3. **Tiago/jurídico valida D-11** → liberar G-02 e a publicação dos textos institucionais.
4. **Tiago define D-12** (telefone vigente) → fechar o aceite de RF-09.
5. **Evandro decide D-14/D-15** (fonte única do levantamento e versionamento dos anexos).
6. **Decidir C-01/C-02** (CRECI, CNPJ e endereço no rodapé) — pode entrar como uma pequena entrega de conformidade ou no próximo ciclo.
7. **Revisar o contraste da barra** (RNF-01) — manter branco com exceção registrada ou escurecer para `#07809B`.
8. **Atualizar `tasks.md` e o plano 003** após cada item concluído.
9. **Deploy somente após aprovação explícita** (regra 8 do `agents.md`).

---

## 15. Resumo em uma frase

As nove alterações pedidas em 13/11/2026 estão implementadas no código, incluindo a marca oficial; a galeria da seção histórica é o único requisito visual ainda incompleto. Para encerrar a entrega restam **um ativo do cliente** (fotos licenciadas), **duas validações** (jurídica/factual e telefone vigente) e **duas decisões de governança** (fonte única dos documentos e versionamento dos anexos).

# Plano 003 — PRD e backlog das alterações solicitadas em 13/11/2026

- **Status:** Ondas 1, 2 e 3 executadas e Onda 4 com texto publicado em 18/11/2026; restam o ativo final da marca, as fotos da galeria e o Lighthouse de Performance
- **Agente líder:** Arquiteto ([agents/arquiteto.md](../agents/arquiteto.md))
- **Apoio:** Conteúdo & Dados, Frontend, QA & Deploy
- **Skills:** catalogo-imoveis, html-semantico-seo, tailwind-design-system, vanilla-js-modular, otimizacao-imagens, qa-validacao-web
- **Fonte de requisitos:** [prds/levantamento-alteracoes-site-2026-11-13.md](../prds/levantamento-alteracoes-site-2026-11-13.md)

## Objetivo

Transformar o levantamento de 13/11/2026 em documentação de engenharia executável: PRD validável, com requisitos funcionais e não funcionais, matriz de priorização, bloqueios explícitos e, após validação, backlog atômico em `tasks.md`.

## Entregáveis

- PRD em [docs/prd-alteracoes-site-2026-11-13.md](../docs/prd-alteracoes-site-2026-11-13.md). **(concluído)**
- Lista de decisões pendentes (D-01 a D-15) e dependências de ativos (A-01 a A-08). **(concluído)**
- Matriz de priorização por complexidade × prontidão. **(concluído)**
- Limitações, bloqueios e fora de escopo. **(concluído)**
- Backlog em [tasks.md](../tasks.md) com tarefas atômicas ordenadas por complexidade, agente responsável e arquivos impactados. **(concluído)**

## Etapas

- [x] Ler `agents.md`, `docs/README.md`, arquitetura, padrões, design system, agentes e skills.
- [x] Ler integralmente o levantamento e conferir os 9 requisitos (ALT-01 a ALT-09).
- [x] Inspecionar a versão vigente (`index.html`) e mapear cada requisito a componentes, linhas e dados reais.
- [x] Verificar disponibilidade dos anexos citados no levantamento.
- [x] Medir contraste das combinações de azul envolvidas em ALT-03.
- [x] Redigir o PRD com requisitos, matriz, bloqueios e fora de escopo.
- [ ] Obter respostas às decisões bloqueantes (D-01 a D-04).
- [ ] Validar o PRD com o solicitante.
- [x] Gerar `tasks.md` com decomposição atômica.
- [x] Executar a Onda 1 (TASK-01 a TASK-08) e validar com `skills/qa-validacao-web.md` — **parcial** (falta QA manual de modal/drawer/newsletter, teclado e Lighthouse).
- [x] Executar a Onda 2 (G1-TASK-01 a G1-TASK-03) com D-02 e D-03 fechadas.
- [x] Executar a Onda 3 (G2) com a composição em código da marca.
- [x] Executar a Onda 4 no que não depende de fotos (G3-TASK-01, texto sempre visível).
- [ ] Concluir a galeria da Onda 4 (G3-TASK-02/03) quando as fotos licenciadas chegarem.

## Critérios de aceite

- O PRD distingue pedido confirmado, interpretação de implementação e questão pendente.
- Nenhum texto, preço, telefone ou categoria foi inventado.
- Itens inviáveis, bloqueados ou fora de escopo estão isolados e não viram task.
- Cada requisito tem critério de aceite verificável e rastreabilidade para ALT-xx.
- O backlog só é gerado após validação, ordenado estritamente da menor para a maior complexidade.

## Validação

- [x] PRD sem links locais quebrados.
- [x] Referências de código conferidas no `index.html` vigente.
- [x] Nenhuma dependência adicionada.
- [x] Nenhum deploy executado.
- [x] Nenhum arquivo de código alterado na fase de PRD. A Onda 1 alterou apenas `index.html` (textos, navegação, filtro e metadados), `tasks.md`, `skills/catalogo-imoveis.md` e este plano. A Onda 2 alterou apenas `index.html` (tokens e barra superior), `docs/design-system.md` e `tasks.md`.

## Registro de execução — Onda 1 (18/11/2026)

### Decisões tomadas nesta execução

| ID | Decisão | Efeito |
|---|---|---|
| **D-04** | Remover as duas entradas do drawer (item de menu e CTA da faixa de contato). O drawer continua acessível pelo botão "Menu" no mobile (`lg:hidden`). | G-01 destravado; perda de acesso no desktop aceita explicitamente |
| **D-05** | Rótulo "Curadoria" do menu passou a "Sobre Nós" (id `#quemSomos` preservado) | Coerência entre menu e seção |
| **D-06** | Adotados os rótulos propostos: Casas, Terrenos, Sala comercial, Lojas (valores `Casa`, `Terreno`, `Sala Comercial`, `Loja`) | Taxonomia registrada em `skills/catalogo-imoveis.md` |
| **D-13** | `title` e `meta description` alinhados à nova redação | SEO coerente com o hero |

### Alterações em `index.html`

1. **Hero:** título com "Médio e Alto Padrão"; subtítulo "Curadoria imobiliária…" sem ponto final.
2. **Faixa de contato:** novo título com "Rio Grande do Sul ou Santa Catarina"; CTA "Explorar Acervo Completo" removido; um único botão centralizado.
3. **Sobre Nós:** título, texto integral do levantamento (parágrafo único) e remoção dos três pilares.
4. **Filtro:** 4 novas categorias, mantendo as 5 existentes e `todos`.
5. **Navegação:** item "Explorar Imóveis de Luxo" removido; 4 links restantes.
6. **Metadados:** `title` (58 caracteres) e `description` (136 caracteres) atualizados.

### Evidências de QA

| Verificação | Resultado |
|---|---|
| Console (Chrome headless, servidor local) | zero erros |
| Filtros: 6 imóveis com `todos` | OK |
| 4 novas categorias | 0 cards + estado vazio com "Limpar filtros" |
| "Limpar filtros" no estado vazio | restaura 6 imóveis |
| Combinação Condomínio + Porto Alegre + maior valor | 1 card |
| `resetAllFilters()` | 6 cards, tipo e localização em `todos` |
| 9 `<option>` no seletor | OK |
| Um único `<h1>` | OK |
| Drawer (`openCatalogDrawer`) e modal (`openPrivateVisitModal`) | funções presentes; drawer acessível no mobile |
| Responsivo 375 / 768 / 1280 px | sem overflow ou sobreposição nas seções alteradas |
| Telefones/`wa.me` | paridade em todos os pontos; nenhum número novo |
| Modal do imóvel (18/11, 2ª rodada) | 5 fotos no mosaico, 5 specs, 6 características, 3 parágrafos, `wa.me` da cidade correta |
| Lightbox | abre na foto 3/5 com legenda correta e fecha por botão |
| `Esc` em modal e drawer | fecha os dois e restaura `body.style.overflow` |
| Drawer | 3 imóveis de POA + 3 de FLN |
| CTA "Falar com Especialista" | abre o modal com o assunto "Consultoria Personalizada — Porto Alegre & Florianópolis" |
| Formulário de contato | exibe "Solicitação enviada..." e fecha sozinho em 2 s |
| "Contato" no modal do imóvel | fecha o imóvel e abre o contato com `Cód. 204810 — ...` |
| Newsletter | feedback "Cadastro realizado com sucesso..." exibido |
| Teclado | foco visível nos `select` (borda `#00B4D8`) |

### Pendências herdadas

- **D-11 (G-02):** validação jurídica/factual do texto "Sobre Nós" antes de publicar.
- **TASK-09:** 9.3, 9.4 e 9.6 concluídos por teste automatizado de interação em 18/11/2026; resta apenas o item 9.7 (Lighthouse), que depende da etapa de deploy.
- **Ondas 2–4:** a Onda 2 (cor, D-02/D-03) foi executada em seguida; a marca (D-01) e a seção editorial (D-07/D-08/D-09/D-11 + imagens licenciadas) seguem bloqueadas.

## Registro de execução — Onda 2 (18/11/2026)

### Decisões tomadas nesta execução

| ID | Decisão | Efeito |
|---|---|---|
| **D-02** | O novo azul vale **só para a barra superior**; CTAs, links, rodapé e `pool-secondary` permanecem `#00B4D8` / `#007791` | Escopo fechado; nenhuma outra superfície azul foi tocada |
| **D-03** | Barra **clara** (`#12B8D8`) com texto **petróleo** (`#072A36`) | Contraste AA garantido sem escurecer o azul — **revisado em 18/11/2026:** o solicitante pediu o texto **branco** de volta; a barra clara foi mantida e o contraste passou a 2,29:1–3,20:1 (abaixo de AA, exceção registrada) |
| **D-01** | Sem arquivo da marca nesta rodada — o solicitante vai enviar o SVG/PNG | Onda 3 continua parada até o ativo chegar |

### Alterações em `index.html`

1. **Token novo `pool.bar` `#12B8D8`** no `tailwind.config` (uso exclusivo da barra).
2. **Variáveis `:root`:** `--pool-bar-start #14BBDC`, `--pool-bar #12B8D8`, `--pool-bar-end #0E9CC4`, `--pool-bar-ink #072A36`.
3. **`.header-pool-minimal`:** gradiente migrado para as variáveis (antes `#00B4D8 → #0099BA → #007791`); borda inferior virou `rgba(7,42,54,0.14)`.
4. **`.header-pool-minimal.scrolled`:** `rgba(16,169,210,0.96)` + blur + borda `rgba(7,42,54,0.2)` (antes azul escuro opaco).
5. **Texto da barra:** `text-white` → `text-pool-deep` no header, menu, telefone e botão "Menu"; telefone e botão ganharam `focus-visible` próprio.
6. **Sublinhado de hover/active dos links:** `#FFFFFF` → `currentColor`, acompanhando a cor do texto; `focus-visible` com `outline` petróleo.
7. **Hover do telefone:** troca de cor por sublinhado (`hover:underline`), evitando queda de contraste abaixo de AA.

### Revisão pós-validação visual (18/11/2026)

O solicitante rejeitou o texto petróleo na barra e pediu o **branco** de volta. Revertidos apenas os itens 5–7 (header, menu, telefone e botão "Menu" voltaram a `text-white`; sublinhado e `focus-visible` seguem com `currentColor`/petróleo para continuar visíveis). O gradiente claro e o token `pool.bar` foram mantidos. Consequência medida: contraste do texto branco cai para **2,29:1 / 2,37:1 / 3,20:1** nas paradas — abaixo de AA. Exceção aprovada pelo solicitante e documentada em `docs/design-system.md`.

### Evidências de QA (Chrome headless, servidor local, 18/11/2026)

| Verificação | Resultado |
|---|---|
| Gradiente computado | `rgb(20,187,220) → rgb(18,184,216) → rgb(14,156,196)` |
| Cor do texto na barra | `rgb(7,42,54)` na 1ª versão; **`rgb(255,255,255)` após a revisão de 18/11** |
| Contraste por parada do gradiente | 6,58:1 / 6,37:1 / 4,72:1 com petróleo (AA); **2,29:1 / 2,37:1 / 3,20:1 com branco** (abaixo de AA, exceção aprovada) |
| Contraste no estado `scrolled` | 5,67:1 com petróleo; ~2,3:1 com branco |
| Hover nos links | cor preservada + sublinhado de 83 px (sem regressão de contraste) |
| Foco por teclado (Tab) | foco visível no link da marca (anel petróleo de 2 px) |
| Overflow horizontal | 0 em 375 / 768 / 1280 px |
| Nav desktop vs. botão "Menu" | `flex` ≥ 1024 px, alternância correta abaixo disso |
| Console | zero erros de página; apenas o aviso pré-existente do Tailwind CDN e o 404 de `favicon.ico` |
| Regressão funcional | 9 opções de filtro, 6 cards, `openCatalogDrawer`/`openPrivateVisitModal`/`resetAllFilters` presentes |
| Escopo | nenhum CTA, link, rodapé ou `pool-secondary` alterado |

### Pendências herdadas

- **G-04:** parcialmente resolvido — o solicitante viu a barra clara em produção e pediu o texto branco (feito). Falta apenas aprovar o resultado final antes do próximo deploy.
- **D-01/Onda 3:** envio do arquivo final da marca (SVG/PNG transparente) para executar G2.
- **D-07/D-08/D-09/D-11 + fotos licenciadas:** Onda 4 continua bloqueada.
- **G-02:** textos institucionais seguem sem validação jurídica/factual.

## Registro de execução — Ondas 3 e 4 (18/11/2026)

### Decisões tomadas nesta execução

| ID | Decisão | Efeito |
|---|---|---|
| **D-01** | Usar a composição em código agora (texto + SVG inline); trocar por `<img>` quando o arquivo chegar | G2-TASK-02/03 executadas; G2-TASK-01 segue aguardando A-01 |
| **D-07** | Texto da seção editorial **sempre visível** | G3-TASK-04 (revelar por clique) não se aplica |
| **D-08** | Galeria **aguarda fotos licenciadas** | G3-TASK-02/03 bloqueadas; nenhuma imagem improvisada foi publicada |
| **D-09** | Seção **depois de "Sobre Nós"**, antes da newsletter | `#duasCapitais` inserida entre `#quemSomos` e `#contatoSection` |

### Alterações em `index.html`

1. **Marca (header):** caixa branca virou coluna — "Poa + casinha + Floripa" na primeira linha e "Imóveis" centralizada abaixo (compensação de `0.22em` do `letter-spacing`); 54 px de altura dentro dos 80 px do header.
2. **Marca (rodapé):** mesma composição em escala menor (`text-lg` / 9 px), substituindo o rótulo lateral.
3. **Nova seção `#duasCapitais`:** `section` semântica com eyebrow "Porto Alegre & Florianópolis", `h2` com o título literal, primeiro parágrafo em destaque, dois parágrafos em grade de 2 colunas no desktop e o fechamento com barra lateral petróleo.
4. **Galeria:** bloco comentado no HTML com os requisitos de D-08/A-03 (quantidade, WebP, `width`/`height`, `loading`, `alt`, proibição de marcas de ferramenta). Nenhum `<img>` vazio foi deixado na página.

### Evidências de QA

| Verificação | Resultado |
|---|---|
| Texto literal (título + 4 parágrafos) | comparação automatizada contra `prds/levantamento-alteracoes-site-2026-11-13.md`: 5/5 idênticos |
| Marca no header | caixa de 54 px em header de 81 px; "IMÓVEIS" a 1 px do centro óptico |
| Marca no rodapé | mesma composição, sem divergência de alinhamento |
| Posição da seção | `#duasCapitais` imediatamente antes de `#contatoSection` |
| Hierarquia | `h2` próprio; 4 parágrafos visíveis sem interação |
| Responsivo | 0 de overflow em 375 / 768 / 1280 px; título em 2 linhas a 1280 px |
| Lighthouse (Onda 1, item 9.7) | Performance 25 · Acessibilidade 96 · Boas Práticas 96 · SEO 100 |

### Pendências herdadas

- **G2-TASK-01 / A-01:** arquivo final da marca (SVG ou PNG transparente) para substituir a composição.
- **G3-TASK-02/03 / A-03:** 3–4 fotos de Porto Alegre e ~3 de Florianópolis, licenciadas e sem marca de ferramenta.
- **9.7 (Lighthouse):** Performance 25 por causa do HTML de 1,59 MB com imagens em base64 + Tailwind CDN; corrigir exige mudar o modelo de mídia (fora do escopo desta entrega). Acessibilidade perde pontos por contraste de botões brancos sobre `#00B4D8` e por textos do rodapé — dívida anterior a este PRD.
- **D-11 / G-02:** textos institucionais (incluindo os 4 parágrafos novos) seguem sem validação jurídica/factual antes de publicar.

## Riscos

| Risco | Mitigação |
|---|---|
| Executar ALT-02 e ALT-05 juntas e perder o acesso ao drawer no desktop | Decidir D-04 antes de executar; teste de regressão do drawer no aceite |
| Clarear o azul e reprovar contraste AA | Decidir D-03 com base na tabela de contraste do PRD — **resolvido na Onda 2** (texto petróleo, 4,72:1–6,58:1) |
| Implementar marca provisória e retrabalhar | Tratar A-01 como bloqueante de RF-01 |
| Publicar imagens com marca do Google Lens ou sem licença | Gate de licença no aceite de RF-08 |
| Textos institucionais gerarem risco jurídico | Validação de D-11 antes da publicação |
| Escopo crescer para redesenho ou modularização | Seção 9.2 do PRD é vinculante |
| Duplicação do levantamento em `prds/` e `docs/` | Definir fonte única (D-14) antes de editar qualquer cópia |

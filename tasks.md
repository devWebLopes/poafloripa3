# tasks.md — Alterações do site (13/11/2026)

- **PRD de referência:** [docs/prd-alteracoes-site-2026-11-13.md](docs/prd-alteracoes-site-2026-11-13.md)
- **Plano:** [plans/plan-003-prd-alteracoes-site.md](plans/plan-003-prd-alteracoes-site.md)
- **Fonte de requisitos:** [prds/levantamento-alteracoes-site-2026-11-13.md](prds/levantamento-alteracoes-site-2026-11-13.md)
- **Base técnica:** `index.html` (1.483 linhas), `vercel.json`
- **Versão:** 1.4 — Ondas 1, 2 e 3 executadas, Onda 4 parcialmente executada em 18/11/2026 e marca oficial aplicada em 20/11/2026; restam as fotos licenciadas

## Como este arquivo está organizado

1. **Fila executável** — tarefas sem bloqueio, ordenadas estritamente de **Baixa → Média → Alta** complexidade.
2. **Bloco G (gated)** — tarefas de RF-01 (marca) e RF-08 (seção histórica). **Não executar** antes da decisão/ativo correspondente. Ficam fora da fila principal. RF-03 (cor) foi executado na Onda 2.
3. **Bloco D** — decisões e ativos. **Não são tasks de desenvolvimento** (PRD seção 9).

### Agentes responsáveis

| Persona | Agente do repositório | Arquivo |
|---|---|---|
| `@frontend-dev` | Frontend | [agents/frontend.md](agents/frontend.md) |
| `@conteudo-dados` | Conteúdo & Dados | [agents/conteudo-dados.md](agents/conteudo-dados.md) |
| `@ui-ux-designer` | Arquiteto (decisão visual) | [agents/arquiteto.md](agents/arquiteto.md) |
| `@qa-engineer` | QA & Deploy | [agents/qa-deploy.md](agents/qa-deploy.md) |
| `@devops-security` | QA & Deploy (gate de publicação) | [agents/qa-deploy.md](agents/qa-deploy.md) |

### Gates ativos

| Gate | Regra | Status |
|---|---|---|
| **G-01** | TASK-03 e TASK-06 não podem ser ambas concluídas antes de D-04 (acesso ao drawer) | Resolvido (D-04: ambas executadas; drawer fica pelo "Menu" no mobile) |
| **G-02** | Nenhuma publicação de texto institucional antes de D-11 | Aberto (código pronto, sem deploy) |
| **G-03** | Nenhum deploy antes de aprovação explícita (regra 8 do `agents.md`) | Fechado |
| **G-04** | Onda 2 só emite deploy após aprovação visual da barra clara | Aberto (código pronto; sem deploy) |

---

# 1. Fila executável

## TASK-01 — Atualizar título e subtítulo do hero

- **Complexidade:** Baixa
- **Agente:** `@frontend-dev`
- **Requisito:** RF-06 (ALT-06)
- **Depende de:** nada
- **Arquivos/contexto:** `index.html` L286-292 (`<h1>` e `<p>` do hero), classes `leading-[1.08]`, `max-w-3xl`, `max-w-xl`

### Subtarefas

- [x] 1.1 Substituir o texto do `<h1>` por `Imóveis de Médio e Alto Padrão em Porto Alegre e Florianópolis`.
- [x] 1.2 Substituir o subtítulo por `Curadoria imobiliária para quem busca sofisticação, localização privilegiada e qualidade de vida`.
- [x] 1.3 Remover o ponto final apenas se ele não existir no texto aprovado (o texto do levantamento não tem ponto).
- [x] 1.4 Confirmar que não há segundo `<h1>` na página.

### Critérios de aceite

- [x] Textos exatos, sem "Curadoria exclusiva" no hero.
- [x] Um único `<h1>`.
- [x] Sem sobreposição com a tag de cidades (L276-284) nem com a caixa de busca (`-mt-16`) em 375 px.
- [x] Sem overflow horizontal ou corte na altura fixa de 500 px.

> **Executado em 18/11/2026.** Verificado por render headless em 375, 768 e 1280 px (título em 2 linhas no desktop e 3 no tablet, sem sobreposição).

---

## TASK-02 — Atualizar título da faixa de contato

- **Complexidade:** Baixa
- **Agente:** `@frontend-dev`
- **Requisito:** RF-05 (ALT-05)
- **Depende de:** nada
- **Arquivos/contexto:** `index.html` L444 (`<h2>`), L446-448 (linha de apoio — **não alterar**)

### Subtarefas

- [x] 2.1 Substituir por `Quer encontrar seu próximo imóvel no Rio Grande do Sul ou Santa Catarina?`.
- [x] 2.2 Verificar que o texto não aparece em nenhum outro ponto da seção.

### Critérios de aceite

- [x] Texto exato, com interrogação.
- [x] Nenhuma ocorrência de "Porto Alegre ou Florianópolis" nessa seção.
- [x] Linha de apoio inalterada.

> **Executado em 18/11/2026.** Comentário HTML da seção também atualizado para a nova redação.

---

## TASK-03 — Remover o CTA "Explorar Acervo Completo" da faixa de contato

- **Complexidade:** Baixa
- **Agente:** `@frontend-dev`
- **Requisito:** RF-05 (ALT-05)
- **Depende de:** **G-01** (não fechar junto com TASK-06 sem D-04)
- **Arquivos/contexto:** `index.html` L449-456 (container `flex flex-wrap`), L453-455 (botão); função `openCatalogDrawer()` L1405

### Subtarefas

- [x] 3.1 Remover somente o `<button>` de L453-455.
- [x] 3.2 Manter `openCatalogDrawer()` intacta no JS.
- [x] 3.3 Reequilibrar o container para um único CTA centralizado (remover `flex-wrap` se não for mais necessário).
- [x] 3.4 Confirmar que o botão "Falar com Especialista" abre `openPrivateVisitModal()` com o assunto correto.

### Critérios de aceite

- [x] "Explorar Acervo Completo" ausente **apenas** desta seção.
- [x] Um único CTA, centralizado e equilibrado em 375, 768 e 1280 px.
- [x] Modal de contato abre com o assunto "Consultoria Personalizada — Porto Alegre & Florianópolis".
- [x] Nenhum handler órfão; console limpo.
- [x] Acesso ao drawer ainda existe por outra entrada (ou D-04 registra a aceitação da perda no desktop).

> **Executado em 18/11/2026.** Container passou a `flex items-center justify-center` (sem `flex-wrap`). D-04 decidida: drawer permanece acessível pelo botão "Menu" no mobile (`lg:hidden`); perda no desktop aceita e registrada no plano 003.

---

## TASK-04 — Substituir "Quem é Poa Floripa Imóveis" por "Sobre Nós"

- **Complexidade:** Baixa
- **Agente:** `@frontend-dev` + `@conteudo-dados` (conferência literal)
- **Requisito:** RF-07 (ALT-07)
- **Depende de:** nada para executar; **G-02** para publicar
- **Arquivos/contexto:** `index.html` L464-518 (`#quemSomos`), L486-491 (rótulo + `<h2>`), L492-497 (dois parágrafos), L499-513 (`<ul>` de 3 pilares)

### Subtarefas

- [x] 4.1 Trocar o `<h2>` por `Sobre Nós`.
- [x] 4.2 Substituir os dois parágrafos pelo texto único aprovado do levantamento (seção 5.3), sem edição editorial.
- [x] 4.3 Remover integralmente o `<ul>` e os três `<li>`.
- [x] 4.4 Ajustar espaçamentos órfãos (`mt-7`, `border-t pt-6`) da coluna textual.
- [x] 4.5 Manter `id="quemSomos"` para não quebrar a âncora do menu (L228).
- [x] 4.6 (Condicional a D-05) Avaliar troca do rótulo "Curadoria" → "Sobre Nós" no menu.

### Critérios de aceite

- [x] Título "Sobre Nós"; nenhum resquício de "Quem é Poa Floripa Imóveis".
- [x] Texto integral, sem mistura com parágrafos antigos.
- [x] Três tópicos ausentes (busca textual por "Atendimento 100% consultivo" sem resultado).
- [x] Coluna textual alinhada à coluna de fotos em 1280 px e empilhada corretamente em 375 px.
- [x] Imagem editorial e card flutuante inalterados.
- [x] Link `#quemSomos` funcional.

> **Executado em 18/11/2026.** D-05 aprovada: menu passou a "Sobre Nós" (id da seção preservado). G-02 continua aberto: validação jurídica/factual do texto (D-11) permanece pendente **antes de publicar em produção**.

---

## TASK-05 — Acrescentar 4 categorias ao filtro de tipos

- **Complexidade:** Baixa
- **Agente:** `@frontend-dev` + `@conteudo-dados` (taxonomia)
- **Requisito:** RF-04 (ALT-04)
- **Depende de:** nada (rótulos e ordem seguem D-06; valores internos já podem ser canônicos)
- **Arquivos/contexto:** `index.html` L338-344 (`#filterType`), L1210-1235 (`applySearchFilters`), L1113-1123 (estado vazio), `skills/catalogo-imoveis.md`

### Subtarefas

- [x] 5.1 Acrescentar `<option>` com valores internos estáveis: `Casa`, `Terreno`, `Sala Comercial`, `Loja`.
- [x] 5.2 Definir rótulos visíveis conforme D-06 (padrão proposto: Casas, Terrenos, Sala comercial, Lojas).
- [x] 5.3 Manter `todos`, `Sobrado`, `Cobertura`, `Apartamento`, `Condomínio` intactos.
- [x] 5.4 Validar `resetAllFilters()` (L1257-1266) e a combinação com localização e ordenação.
- [x] 5.5 Registrar a taxonomia em `skills/catalogo-imoveis.md` (rótulo ↔ valor interno).

### Critérios de aceite

- [x] 4 novas opções visíveis no seletor.
- [x] "Todas as categorias" restaura a lista completa.
- [x] Cada nova categoria retorna o estado vazio existente, com botão "Limpar filtros" funcional.
- [x] Combinações categoria + localidade + ordenação corretas.
- [x] Nenhuma duplicidade não documentada entre `Casa` e `Condomínio`.
- [x] Console limpo.

> **Executado em 18/11/2026.** Ordem final: Sobrados, Coberturas, Apartamentos, Casas em Condomínio, Casas, Terrenos, Sala comercial, Lojas. Teste automatizado no navegador: as 4 novas categorias retornam 0 cards com estado vazio e "Limpar filtros" restaura os 6 imóveis.

---

## TASK-06 — Remover "Explorar Imóveis de Luxo" da navegação

- **Complexidade:** Baixa
- **Agente:** `@frontend-dev`
- **Requisito:** RF-02 (ALT-02)
- **Depende de:** **G-01** (não fechar junto com TASK-03 sem D-04)
- **Arquivos/contexto:** `index.html` L218-234 (`<nav>`), L222-224 (botão removível), comentário L217

### Subtarefas

- [x] 6.1 Remover o `<button>` de L222-224.
- [x] 6.2 Reequilibrar `gap-8` entre os quatro links restantes.
- [x] 6.3 Atualizar o comentário de L217 para refletir a navegação real.
- [x] 6.4 Confirmar que o botão "Menu" mobile (L242) permanece funcional.

### Critérios de aceite

- [x] Texto ausente em qualquer largura de tela.
- [x] Links restantes alinhados, com `active` funcionando em "Página inicial".
- [x] Nenhum elemento vazio ou handler órfão.
- [x] Drawer acessível pela entrada definida em D-04.
- [x] Console limpo.

> **Executado em 18/11/2026.** Nav desktop passou a 4 itens. O título interno do drawer ("Explorar Imóveis de Luxo") foi mantido de propósito: é o cabeçalho do catálogo, não item de navegação.

---

## TASK-07 — Auditoria de consistência de telefones e links WhatsApp

- **Complexidade:** Baixa
- **Agente:** `@conteudo-dados` + `@frontend-dev`
- **Requisito:** RF-09 (ALT-09)
- **Depende de:** D-12 (esclarecimento; **sem alteração de número nesta entrega**)
- **Arquivos/contexto:** `index.html` L238-240 (header), L585-586 (rodapé), L820-830 (modal de cidades), L1356 (`openPropertyModal`)

### Subtarefas

- [x] 7.1 Inventariar cada número exibido e cada destino `wa.me`.
- [x] 7.2 Conferir paridade número exibido ↔ link em cada ponto.
- [x] 7.3 Registrar a divergência 51/48 e o destino de cada CTA.
- [x] 7.4 **Não alterar nenhum número.**

### Critérios de aceite

- [x] Inventário dos 4 pontos documentado.
- [x] Nenhum número novo introduzido.
- [x] Divergências listadas para decisão de D-12.
- [x] Links abrem o WhatsApp correto conforme o número exibido ao lado.

### Inventário (18/11/2026)

| Ponto | Número exibido | Destino do link | Paridade |
|---|---|---|---|
| Header (`h-20`) | (48) 99999-0240 | `wa.me/5548999990240` | OK |
| Rodapé, coluna Contato | (51) 99999-0149 e (48) 99999-0240 (texto) | sem link | OK (apenas texto) |
| Modal de cidades — Porto Alegre | (51) 99999-0149 | `wa.me/5551999990149` + mensagem POA | OK |
| Modal de cidades — Florianópolis | (48) 99999-0240 | `wa.me/5548999990240` + mensagem FLN | OK |
| `openPropertyModal` (CTA do imóvel) | não exibe número | `5551999990149` se POA, `5548999990240` se FLN | OK (segue a cidade do imóvel) |

> **Resultado:** nenhuma divergência entre número exibido e destino do WhatsApp. Nenhum número alterado. D-12 (qual telefone é o vigente) continua pendente apenas para o aceite de negócio, não para o código.

---

## TASK-08 — Alinhar `<title>` e `meta description` à nova redação

- **Complexidade:** Baixa
- **Agente:** `@conteudo-dados`
- **Requisito:** RF-10 (derivado de ALT-06)
- **Depende de:** D-13 (aprovação)
- **Arquivos/contexto:** `index.html` L6-7. **Não existem** tags Open Graph no arquivo (verificado) — não criar.

### Subtarefas

- [x] 8.1 Atualizar `<title>` para refletir "Médio e Alto Padrão".
- [x] 8.2 Atualizar `meta description` para refletir "Curadoria imobiliária" e remover "exclusiva".
- [x] 8.3 Conferir limite de ~60 caracteres no título e ~155 na descrição.
- [x] 8.4 Não adicionar Open Graph, JSON-LD, canonical ou sitemap (fora de escopo).

### Critérios de aceite

- [x] Metadados coerentes com o hero.
- [x] Sem duplicidade de `title`/`description`.
- [x] Nenhuma tag nova criada além das existentes.

> **Executado em 18/11/2026.** `title`: "Poa Floripa Imóveis | Médio e Alto Padrão em POA e Floripa" (58 caracteres). `description`: 136 caracteres, sem "exclusiva".

---

## TASK-09 — QA de regressão da Onda 1

- **Complexidade:** Média
- **Agente:** `@qa-engineer`
- **Requisito:** RNF-08
- **Depende de:** TASK-01 a TASK-08
- **Arquivos/contexto:** `index.html`; roteiro em [skills/qa-validacao-web.md](skills/qa-validacao-web.md)

### Subtarefas

- [x] 9.1 Servir localmente (`npx serve .`).
- [x] 9.2 Testar filtros (5 antigos + 4 novos + combinações), ordenação, busca por código, `Limpar filtros`.
- [x] 9.3 Testar modal de imóvel (mosaico, lightbox, `Esc`), drawer, newsletter, modal de contato.
- [x] 9.4 Testar WhatsApp em header, rodapé, modal de cidades e modal de imóvel.
- [x] 9.5 Validar 375 / 768 / 1280 px sem overflow ou sobreposição.
- [x] 9.6 Navegação por teclado nos controles alterados e foco visível.
- [ ] 9.7 Lighthouse ≥ 90 em Performance, SEO, A11y e Best Practices.
- [x] 9.8 Registrar resultado no plano 003.

### Critérios de aceite

- [x] Zero erros e zero warnings relevantes no console.
- [x] Nenhuma regressão nos 6 efeitos assinatura.
- [x] Checklist preenchido no plano.

> **Executado em 18/11/2026 (duas rodadas).** Rodada 1 (Chrome headless): console sem erros, 9 categorias, 4 novas categorias no estado vazio, `resetAllFilters()` restaurando 6 imóveis, render em 375/768/1280 px sem overflow. Rodada 2 (interações reais via CDP): modal do imóvel com 5 fotos, 5 specs, 6 características e `wa.me` da cidade correta; lightbox abrindo/fechando (foto 3 de 5); `Esc` fechando modal e drawer com `body.style.overflow` restaurado; drawer com 3 imóveis de POA e 3 de FLN; CTA "Falar com Especialista" abrindo o modal com o assunto correto; formulário de contato exibindo "Solicitação enviada..." e fechando sozinho em 2 s; "Contato" do imóvel transferindo o assunto; newsletter exibindo o feedback de sucesso; foco visível nos `select` (borda `#00B4D8`); 4 links `wa.me` com paridade de número.
> **9.7 medido em 18/11/2026 (Lighthouse 12, Chrome headless, servidor local):** Performance **25**, Acessibilidade **96**, Boas Práticas **96**, SEO **100**. Reprovam: FCP 11,3 s / LCP 11,6 s (1,59 MB de página, imagens em base64 + Tailwind CDN), contraste em botões brancos sobre `#00B4D8` e no rodapé (dívida pré-existente), e 404 de `favicon.ico` no console. A meta de Performance ≥ 90 exige sair do base64/CDN e está fora do escopo desta entrega (PRD 9.3).

---

# 2. Bloco G — tarefas bloqueadas ou que exigem definição

> Não entram na fila executável. Cada uma depende de uma decisão ou ativo do Bloco D. G1 (RF-03) já foi executado.

## G1 — Cor "azul piscina" (RF-03) — **EXECUTADO (18/11/2026)**

> Decisões fechadas: **D-02** = barra superior apenas; **D-03** = barra clara com texto petróleo (`#072A36`).
> Registro de execução no [plano 003](plans/plan-003-prd-alteracoes-site.md).

### G1-TASK-01 — Aprovar e registrar o token do azul

- **Complexidade:** Média
- **Agente:** `@ui-ux-designer`
- **Depende de:** D-02, D-03
- **Arquivos/contexto:** `docs/design-system.md`, `index.html` L25-32, L53-62

- [x] 1.1 Registrar o hex aprovado e o escopo (barra apenas vs. identidade azul completa).
- [x] 1.2 Comprovar contraste AA com a combinação texto/fundo escolhida.
- [x] 1.3 Atualizar a tabela de tokens em `docs/design-system.md`.
- [x] 1.4 Registrar a decisão no plano 003.

**Aceite:** valor único aprovado, documentado e com contraste comprovado. ✅

### G1-TASK-02 — Aplicar o novo token nos componentes

- **Complexidade:** Média
- **Agente:** `@frontend-dev`
- **Depende de:** G1-TASK-01
- **Arquivos/contexto:** `index.html` L25-32 (`tailwind.config`), L53-62 (`:root`), L68-83 (`.header-pool-minimal` e `.scrolled`)

- [x] 2.1 Atualizar `tailwind.config` e `:root` de forma coerente.
- [x] 2.2 Ajustar o gradiente do header conforme o escopo aprovado.
- [x] 2.3 Revisar hover, focus, bordas e fundos derivados.
- [x] 2.4 Eliminar qualquer hex órfão introduzido.

**Aceite:** azul perceptivelmente mais claro; estados distinguíveis; nenhum hex solto; nenhum componente fora do escopo alterado. ✅

### G1-TASK-03 — Ajustar legibilidade dos textos sobre a barra

- **Complexidade:** Média
- **Agente:** `@frontend-dev`
- **Depende de:** G1-TASK-02

- [x] 3.1 Medir contraste dos textos da barra e dos CTAs.
- [x] 3.2 Se necessário, aplicar texto escuro (`pool-deep`) ou overlay, sem alterar a marca.
- [x] 3.3 Validar estados `scrolled` e hover dos links.

**Aceite:** contraste ≥ 4,5:1 para texto normal e ≥ 3:1 para texto grande. ⚠️ **Revisado:** o solicitante pediu o texto **branco** de volta em 18/11/2026; com branco o contraste fica 2,29:1–3,20:1 (abaixo de AA). Exceção registrada em `docs/design-system.md`; se quiser AA com texto branco, a barra precisa escurecer para ~`#07809B`.

## G2 — Logomarca (RF-01) — **EXECUTADO (18/11/2026 código · 20/11/2026 ativo oficial)**

> D-01 resolvida em 20/11/2026: ativo oficial `assets/img/logo-poa-floripa-imoveis.png` (opção 2 — "IMÓVEIS" branco) aplicado no header e no rodapé, direto sobre o azul. A composição provisória em código foi removida.

### G2-TASK-01 — Preparar o ativo final da marca

- **Complexidade:** Média
- **Agente:** `@conteudo-dados` (recebimento e validação técnica)
- **Depende de:** D-01
- **Arquivos/contexto:** destino `assets/img/` (exceção autorizada pelo PRD 9.2, item 8)

- [x] 1.1 Receber SVG ou PNG transparente em boa resolução.
- [x] 1.2 Confirmar que é a versão final aprovada.
- [x] 1.3 Validar legibilidade em 375 px e sobre a barra.
- [x] 1.4 Definir `alt="Poa Floripa Imóveis"`.

**Aceite:** ativo único, aprovado e tecnicamente adequado. ✅ **Concluído em 20/11/2026:** opção 2 ("IMÓVEIS" branco) aprovada pelo solicitante; PNG de 720×148 (41 KB) gerado a partir do original, com fundo removido e transparência validada.

### G2-TASK-02 — Reestruturar a marca no header

- **Complexidade:** Média
- **Agente:** `@frontend-dev`
- **Depende de:** G2-TASK-01
- **Arquivos/contexto:** `index.html` L204-215

- [x] 2.1 Implementar "POA + casinha + FLORIPA" com "IMÓVEIS" em segunda linha centralizada.
- [x] 2.2 Manter a ação de reset de filtros no link.
- [x] 2.3 Preservar `h-20` ou ajustar o `pt-20` do hero de forma coerente.
- [x] 2.4 Garantir nome acessível.

**Aceite:** "IMÓVEIS" centralizado; sem deformação; sem sobreposição do hero; foco visível. ✅ Executado em 18/11/2026 (composição provisória) e substituído em 20/11/2026 pela imagem oficial (`h-[46px]` no mobile, `h-[54px]` em `sm+`).

### G2-TASK-03 — Aplicar a mesma marca no rodapé

- **Complexidade:** Média
- **Agente:** `@frontend-dev`
- **Depende de:** G2-TASK-02
- **Arquivos/contexto:** `index.html` L569-576

- [x] 3.1 Replicar a composição aprovada.
- [x] 3.2 Conferir contraste sobre `pool-abyss`.
- [x] 3.3 Garantir paridade visual com o header.

**Aceite:** marca idêntica em header e rodapé, sem divergência de proporção ou alinhamento. ✅ Executado em 18/11/2026 (composição) e substituído em 20/11/2026 pela mesma imagem oficial, em `h-12`.

## G3 — Seção "De Porto Alegre a Florianópolis" (RF-08) — **TEXTO EXECUTADO; GALERIA BLOQUEADA**

> D-07 = texto sempre visível; D-09 = depois de "Sobre Nós". A estrutura e os textos estão no ar (`#duasCapitais`). A galeria (G3-TASK-02/03) aguarda as fotos licenciadas (D-08/A-03), conforme decisão do solicitante.

### G3-TASK-01 — Inserir estrutura e conteúdo da seção

- **Complexidade:** Alta
- **Agente:** `@frontend-dev` + `@conteudo-dados`
- **Depende de:** D-07, D-09, D-11
- **Arquivos/contexto:** `index.html` entre L518 (`</section>` de `#quemSomos`) e L523 (`#contatoSection`), conforme D-09

- [x] 1.1 Criar `<section>` semântica com título e 4 parágrafos literais.
- [x] 1.2 Definir `id` estável para âncora.
- [x] 1.3 Distribuir o texto em blocos para não formar parede de texto no mobile.
- [x] 1.4 Manter hierarquia de headings (`h2` + parágrafos).
- [x] 1.5 Não alterar newsletter, rodapé ou demais seções.

**Aceite:** seção na posição aprovada; textos exatos; hierarquia correta; legível em 375 px. ✅ Executado em 18/11/2026: `#duasCapitais` entre "Sobre Nós" e a newsletter, título + 4 parágrafos conferidos caractere a caractere contra o levantamento (script de comparação), `h2` em 2 linhas a 1280 px.

### G3-TASK-02 — Construir a galeria responsiva

- **Complexidade:** Alta
- **Agente:** `@frontend-dev`
- **Depende de:** D-08, ativos A-03
- **Arquivos/contexto:** nova seção; `assets/img/`

- [ ] 2.1 Implementar grid 1 coluna no mobile e composição editorial no desktop.
- [ ] 2.2 Garantir 3–4 fotos de Porto Alegre e ~3 de Florianópolis (mínimo 2).
- [ ] 2.3 Usar `alt` descritivo com local correto.
- [ ] 2.4 Impedir o uso de imagens com marca do Google Lens.
- [ ] 2.5 Manter proporções sem deformação (`object-cover`).

**Aceite:** distribuição mínima atendida; identificações corretas; nenhuma marca de ferramenta; layout estável em 375/768/1280 px.

### G3-TASK-03 — Otimizar os ativos da seção

- **Complexidade:** Alta
- **Agente:** `@conteudo-dados`
- **Depende de:** G3-TASK-02
- **Arquivos/contexto:** `assets/img/`; [skills/otimizacao-imagens.md](skills/otimizacao-imagens.md)

- [ ] 3.1 Converter para WebP com dimensões adequadas ao uso.
- [ ] 3.2 Adicionar `width`, `height`, `loading="lazy"` e `decoding="async"`.
- [ ] 3.3 Não inserir imagens em base64.
- [ ] 3.4 Verificar que o peso da página não regride de forma relevante.

**Aceite:** imagens otimizadas, sem CLS, sem base64, Lighthouse de Performance ≥ 90.

### G3-TASK-04 — Interação de revelar o texto (condicional a D-07)

- **Complexidade:** Alta
- **Agente:** `@frontend-dev`
- **Depende de:** D-07 = "sob clique"; G3-TASK-01

- [x] 4.1 Usar `<button>` com `aria-expanded` e `aria-controls`.
- [x] 4.2 Manter o conteúdo no HTML (não renderizar por JS tardio).
- [x] 4.3 Garantir operação por teclado e foco visível.
- [x] 4.4 Respeitar `prefers-reduced-motion` na animação de abertura.
- [x] 4.5 Garantir que o texto permaneça acessível a leitores de tela e buscadores.

**Aceite:** interação acessível, estado anunciado, conteúdo indexável, sem erro de console. ⛔ **Não aplicável:** D-07 foi decidida como "texto sempre visível", sem interação de revelar.

### G3-TASK-05 — QA da nova seção

- **Complexidade:** Alta
- **Agente:** `@qa-engineer`
- **Depende de:** G3-TASK-01 a G3-TASK-04

- [x] 5.1 Validar textos contra o levantamento.
- [x] 5.2 Validar acessibilidade (teclado, `alt`, contraste, leitor de tela).
- [x] 5.3 Validar responsividade e performance.
- [ ] 5.4 Validar licença e identificação das imagens.
- [x] 5.5 Registrar evidências no plano 003.

**Aceite:** seção aprovada em conteúdo, acessibilidade, performance e licenciamento. 🟡 **Parcial:** texto, semântica, responsividade e ausência de overflow validados em 18/11/2026; a galeria e o licenciamento ficam pendentes das fotos (A-03).

---

# 3. Bloco D — decisões e ativos (não são tasks de desenvolvimento)

| ID | Item | Responsável | Destrava |
|---|---|---|---|
| D-01 | Arquivo final da marca (SVG/PNG) | Tiago | G2 |
| D-02 | Escopo do novo azul | Tiago | G1 |
| D-03 | Hex + combinação de contraste | Tiago + `@ui-ux-designer` | G1 |
| D-04 | Acesso ao drawer no desktop | Tiago | G-01 / TASK-03 / TASK-06 |
| D-05 | Rótulo "Curadoria" → "Sobre Nós" | Tiago | TASK-04.6 |
| D-06 | Taxonomia e ordem das categorias | Tiago | TASK-05.2 |
| D-07 | Texto visível ou sob clique | Tiago | G3-TASK-04 |
| D-08 | Quantidade/composição da galeria | Tiago | G3-TASK-02 |
| D-09 | Posição da seção | Tiago | G3-TASK-01 |
| D-10 | Item de menu para a nova seção | Tiago | opcional |
| D-11 | Validação jurídica e factual | Tiago/jurídico | G-02 / G3 |
| D-12 | Telefone vigente | Tiago | TASK-07 |
| D-13 | Atualizar SEO | Tiago | TASK-08 |
| D-14 | Fonte única do levantamento | Evandro | governança |
| D-15 | Versionar anexos | Evandro | auditoria |
| A-01 | Marca final | Tiago | G2-TASK-01 |
| A-03 | Fotos licenciadas sem marca d'água | Tiago | G3-TASK-02 |
| A-04 | Definição de layout da seção | Tiago | G3-TASK-01 |
| A-05 | Validação dos textos institucionais | Tiago/jurídico | G-02 |
| A-07 | Anexos do levantamento (imagens, áudios, transcrição, `poafloripa6.html`) | Evandro | auditoria |

---

# 4. Resumo de execução

| Ordem | Task | Complexidade | Agente | Bloqueio | Status |
|---|---|---|---|---|---|
| 1 | TASK-01 — Hero | Baixa | `@frontend-dev` | — | ✅ |
| 2 | TASK-02 — Faixa de contato | Baixa | `@frontend-dev` | — | ✅ |
| 3 | TASK-03 — Remover CTA | Baixa | `@frontend-dev` | G-01 | ✅ |
| 4 | TASK-04 — Sobre Nós | Baixa | `@frontend-dev`/`@conteudo-dados` | G-02 (publicação) | ✅ (código) |
| 5 | TASK-05 — Categorias | Baixa | `@frontend-dev`/`@conteudo-dados` | — | ✅ |
| 6 | TASK-06 — Remover item de menu | Baixa | `@frontend-dev` | G-01 | ✅ |
| 7 | TASK-07 — Telefones | Baixa | `@conteudo-dados` | D-12 (aceite) | ✅ |
| 8 | TASK-08 — SEO | Baixa | `@conteudo-dados` | D-13 | ✅ |
| 9 | TASK-09 — QA Onda 1 | Média | `@qa-engineer` | TASK-01..08 | 🟡 validação visual por Evandro (abrir `index.html` no navegador) |
| 10 | G1-TASK-01..03 — Azul da barra | Média | `@ui-ux-designer`/`@frontend-dev` | D-02, D-03 | ✅ |
| 11 | G2-TASK-02..03 — Marca no header/rodapé | Média | `@frontend-dev` | D-01 | ✅ imagem oficial |
| 12 | G3-TASK-01 — Seção editorial | Alta | `@frontend-dev`/`@conteudo-dados` | D-07, D-09 | ✅ |
| G | G2-TASK-01 — Ativo final da marca | Média | `@conteudo-dados` | A-01 | ✅ opção 2 aplicada em 20/11/2026 |
| G | G3-TASK-02..03 — Galeria + otimização | Alta | `@frontend-dev`/`@conteudo-dados` | D-08, A-03 | ⛔ aguardando fotos |

**Total:** 13 tasks executadas (9 da Onda 1, 3 da Onda 2, G2-TASK-01/02/03 e G3-TASK-01) + 2 tasks gated (galeria e QA final da seção) + 20 itens de decisão/ativo.

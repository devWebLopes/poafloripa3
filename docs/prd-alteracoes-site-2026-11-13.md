# PRD — Alterações do site solicitadas em 13/11/2026

- **Produto:** Poa Floripa Imóveis
- **Versão:** 0.1 (proposta para validação)
- **Status:** Aguardando validação do solicitante
- **Fonte de requisitos:** [levantamento-alteracoes-site-2026-11-13.md](../prds/levantamento-alteracoes-site-2026-11-13.md)
- **Plano relacionado:** [Plano 003](../plans/plan-003-prd-alteracoes-site.md)
- **Escopo do produto:** site estático de imóveis exclusivamente para venda em Porto Alegre e Florianópolis
- **Base técnica analisada:** `index.html` (1.031.758 bytes, 1.483 linhas), `vercel.json`, `docs/`, `agents/`, `skills/`

> Este PRD **não** é um redesenho. Ele converte os 9 pedidos do levantamento em requisitos verificáveis e separa, de forma explícita, o que está **pronto para desenvolvimento**, o que **exige definição do cliente** e o que está **bloqueado ou fora de escopo**. Nenhum dado de imóvel, preço ou contato foi inventado.

---

## 1. Resumo executivo

O site vigente é uma SPA de arquivo único (`index.html`) com HTML, CSS, dados de imóveis (base64) e JavaScript no mesmo arquivo. As solicitações de 13/11/2026 são **ajustes editoriais e de identidade visual**, não uma reestruturação:

| # | Pedido | Natureza | Esforço | Prontidão |
|---|---|---|---|---|
| ALT-01 | Nova logomarca com "IMÓVEIS" centralizado | Identidade visual | Médio | **Bloqueado** (ativo) |
| ALT-02 | Remover "Explorar Imóveis de Luxo" da barra | Navegação | Baixo | Pronto, com 1 decisão |
| ALT-03 | Clarear o azul para "azul piscina" | Design system | Médio | **Requer definição** |
| ALT-04 | 4 novas categorias no filtro | Funcional | Baixo | Pronto |
| ALT-05 | Novo texto de contato + remover CTA | Conteúdo/UI | Baixo | Pronto, com 1 decisão |
| ALT-06 | Novo título e subtítulo do hero | Conteúdo/SEO | Baixo | Pronto |
| ALT-07 | "Quem é Poa Floripa" → "Sobre Nós" | Conteúdo/UI | Baixo | Pronto (publicação condicionada) |
| ALT-08 | Nova seção final POA + Floripa | Feature nova | Alto | **Requer definição** |
| ALT-09 | Manter o telefone atual | Verificação | Baixo | Pronto, com 1 dúvida |

**Achados de engenharia relevantes (não previstos no levantamento):**

1. **A cor solicitada já existe como token.** `pool.DEFAULT = #00B4D8` já é um "azul piscina". O que escurece a barra é o gradiente `#00B4D8 → #0099BA → #007791` e o token `pool-secondary = #007791`. ALT-03 é, na prática, **reduzir o escurecimento do gradiente**, não trocar a cor primária.
2. **O azul claro não sustenta texto branco.** Branco sobre `#00B4D8` tem contraste de **2,46:1** (reprova AA, que exige 4,5:1 para texto normal e 3:1 para texto grande). Clarear mais agrava o problema. Existe um conflito direto entre ALT-03 e o requisito de acessibilidade do projeto.
3. **Após ALT-02 + ALT-05 o drawer do catálogo fica inacessível no desktop.** As únicas entradas via `openCatalogDrawer()` são o item de menu (ALT-02) e o botão "Explorar Acervo Completo" da faixa de contato (ALT-05). O botão "Menu" do header é `lg:hidden`. A decisão precisa ser tomada **antes** de executar as duas tarefas juntas.
4. **A logomarca atual não é imagem**: é uma composição CSS (texto + SVG da casinha + etiqueta "Imóveis" com borda à esquerda), replicada no header (linhas 204-215) e no rodapé (linhas 569-576). ALT-01 exige reestruturação de layout, não apenas troca de arquivo — e nos dois lugares.
5. **Existem dois telefones publicados**: `(51) 99999-0149` (Porto Alegre) e `(48) 99999-0240` (Florianópolis). "Manter o telefone atual" é ambíguo.
6. **Os anexos citados no levantamento não existem no repositório** (`prds/` contém apenas o `.md`). Nenhuma imagem, áudio ou transcrição pode ser conferida nesta análise.

---

## 2. Escopo

### 2.1 Dentro do escopo

- Ajustes de conteúdo textual nos pontos explicitamente citados.
- Ajustes de navegação, filtros e CTAs citados.
- Evolução controlada do design system de cor (token único).
- Nova seção editorial ao final do conteúdo principal.
- Correções derivadas **estritamente necessárias** para não quebrar o que já funciona (SEO técnico, acessibilidade, responsividade, estados vazios).

### 2.2 Fora do escopo

Ver seção 9.2 (lista completa e justificada).

### 2.3 Princípio de não-ampliação

Conforme o levantamento (seção 9, item 3): **não** expandir automaticamente "Porto Alegre e Florianópolis" para "Rio Grande do Sul e Santa Catarina" em outros textos. A alteração geográfica vale apenas para a chamada de contato (ALT-05), salvo aprovação explícita.

---

## 3. Diagnóstico do estado vigente

| Requisito | Componente real | Localização | Observação técnica |
|---|---|---|---|
| ALT-01 | Logo CSS no header e no rodapé | `index.html` L204-215, L569-576 | Duplicação manual; header fixo `h-20`; "Imóveis" hoje é etiqueta lateral, não segunda linha |
| ALT-02 | `<nav>` desktop | L218-234 | 5 links; o item é `<button onclick="openCatalogDrawer()">`; menu mobile inexistente (botão abre drawer) |
| ALT-03 | Tokens `pool.*` + `.header-pool-minimal` | L25-31, L53-57, L68-78 | Gradiente de 3 paradas; `pool-light` para fundos; estados hover/borda derivados |
| ALT-04 | `<select id="filterType">` | L338-344 | Valores internos: `Sobrado`, `Cobertura`, `Apartamento`, `Condomínio`; filtro em `applySearchFilters()` L1210-1235 |
| ALT-05 | Faixa de consultoria | L441-458 | 2 CTAs; botão "Falar com Especialista" abre `openPrivateVisitModal()` |
| ALT-06 | Hero `<h1>` + subtítulo | L286-292 | Um único `<h1>` (correto); altura fixa `h-[500px]` |
| ALT-07 | Seção `#quemSomos` | L464-518 | 2 parágrafos + `<ul>` de 3 pilares; rótulo do menu é "Curadoria" (L228-230) |
| ALT-08 | Inexistente | — | Última seção de conteúdo hoje é `#contatoSection` (L523), seguida do rodapé (L564) |
| ALT-09 | Telefones | L238-240, L585-586, L820-830, L1356 | Header e modal usam 48; rodapé e modal usam 51 e 48; `wa.me` fixo no HTML |

**Dados disponíveis para o filtro:** 6 imóveis — 2 `Sobrado`, 1 `Cobertura`, 1 `Condomínio`, 2 `Apartamento`. **Nenhum** imóvel nas 4 categorias novas.

**Estado vazio:** já implementado em `renderProperties()` L1113-1123 ("Nenhum imóvel encontrado com estes filtros"). Consequência: incluir categorias sem estoque **não gera tela quebrada**.

---

## 4. Premissas e decisões pendentes

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

### 4.2 Decisões pendentes — bloqueiam a decomposição fina em tasks

| ID | Pergunta | Impacta | Bloqueia dev? |
|---|---|---|---|
| **D-01** | Qual é o arquivo final da marca (SVG ou PNG transparente, boa resolução)? O link do Gemini exige autenticação e a foto `WA0039` não serve para produção. | ALT-01 | **Sim** |
| **D-02** | O novo azul vale só para a barra superior ou para todos os elementos azuis (CTAs, links, rodapé, `pool-secondary`)? | ALT-03 | **Sim** | **Resolvido (18/11/2026):** barra superior apenas. |
| **D-03** | Qual o valor final aprovado do azul? Aceita-se texto escuro sobre barra clara (para manter contraste AA), ou a barra permanece com texto branco em tom mais escuro? | ALT-03 | **Sim** | **Resolvido (18/11/2026):** barra clara `#12B8D8` com texto petróleo `#072A36` (6,37:1). |
| **D-04** | O acesso ao catálogo (drawer) deve continuar existindo no desktop após remover o item de menu e o CTA? Se sim, por qual entrada? | ALT-02, ALT-05 | **Sim** (para aceite conjunto) |
| **D-05** | O rótulo "Curadoria" do menu deve virar "Sobre Nós"? | ALT-07 | Não (executável em separado) |
| **D-06** | Taxonomia final: "Casas" convive com "Casas em Condomínio"? "Sala comercial" ou "Salas comerciais"? Ordem das opções? | ALT-04 | Não (valores internos podem ser canônicos) |
| **D-07** | A seção histórica abre com texto sempre visível ou sob clique? | ALT-08 | **Sim** |
| **D-08** | Quantidade e composição final da galeria (mínimo 2 fotos de Florianópolis) e se haverá novas imagens além das 4 enviadas. | ALT-08 | **Sim** |
| **D-09** | A nova seção entra depois de "Sobre Nós" (antes da newsletter) ou depois da newsletter (imediatamente antes do rodapé)? | ALT-08 | **Sim** |
| **D-10** | Haverá item de menu apontando para a nova seção? | ALT-08 | Não |
| **D-11** | Os textos institucionais ("assessoria jurídica de confiança", "segurança patrimonial", "exclusividade", IDH, segurança) foram validados jurídica e factualmente? | ALT-07, ALT-08 | **Sim** (gate de publicação) |
| **D-12** | Qual telefone é "o atual" — o de Porto Alegre (51), o de Florianópolis (48) ou ambos? O header exibe apenas o 48. | ALT-09 | **Sim** (para o aceite de consistência) |
| **D-13** | Autoriza atualizar `<title>`, `meta description` e Open Graph para refletir "Médio e Alto Padrão" / "Curadoria imobiliária"? Hoje eles repetem a redação antiga. | ALT-06 (derivado) | Não |
| **D-14** | O levantamento está duplicado em `prds/` e `docs/` (hash idêntico). Qual é a fonte única de verdade? A cópia em `docs/` pode ser removida? | Governança | Não |
| **D-15** | Onde estão os anexos citados (imagens, áudios, transcrição, `poafloripa6.html`)? Precisam ser versionados para auditoria dos requisitos. | Todos | Não (rastreabilidade) |

---

## 5. Requisitos funcionais

### RF-01 — Logomarca com "IMÓVEIS" centralizado (ALT-01)

**Requisito.** Exibir a marca "POA + ícone de casa + FLORIPA" com "IMÓVEIS" em segunda linha, **visualmente centralizado** em relação ao conjunto superior, no header e no rodapé.

**Regras:**
- Usar o arquivo aprovado (D-01) ou, na ausência dele, reproduzir a composição com o mesmo desenho atual (texto + SVG da casinha + segunda linha).
- Não deformar proporção; manter legibilidade em 375 px.
- Se a marca for `<img>`, `alt="Poa Floripa Imóveis"`; se permanecer composição textual, garantir nome acessível no link.
- Não alterar as cores `brand-red` (`#D62828`) e `pool-deep` sem aprovação.
- Header permanece legível sobre a barra (contraste) e não deve crescer além de `h-20` sem revisão do `pt-20` do hero.

**Aceite:**
- [ ] "IMÓVEIS" centralizado sob o conjunto, no header e no rodapé.
- [ ] Marca legível em 375, 768 e 1280 px, sem corte nem deformação.
- [ ] Nome acessível presente; link da marca continua resetando filtros.
- [ ] Header não sobrepõe o hero (sem regressão de `pt-20`).

**Dependência:** D-01 (bloqueante).

---

### RF-02 — Remover "Explorar Imóveis de Luxo" da navegação (ALT-02)

**Requisito.** Remover o item textual da barra azul e reequilibrar o espaçamento dos quatro itens restantes.

**Regras:**
- Remover apenas o item de navegação; **não** remover o drawer, a função `openCatalogDrawer()` nem os imóveis.
- Não deixar elementos vazios, handlers órfãos ou erros de console.
- Como não existe menu mobile de navegação (o botão "Menu" abre o drawer), não há item equivalente a remover no mobile. Registrar isso como constatação.
- A função `openCatalogDrawer()` deve permanecer utilizável (ver D-04).

**Aceite:**
- [ ] O texto não aparece na navegação em nenhuma largura.
- [ ] `Página inicial`, `Imóveis Selecionados`, `Curadoria`, `Contato` alinhados e funcionais.
- [ ] Console limpo; drawer ainda abre pela entrada remanescente definida em D-04.

---

### RF-03 — Azul piscina mais claro (ALT-03)

**Requisito.** Tornar o azul perceptivelmente mais claro, próximo da referência, aplicando a mudança de forma **sistêmica via tokens**.

**Estado técnico:**
- `pool.DEFAULT` `#00B4D8` já é azul piscina; a percepção de escuro vem do gradiente (`#00B4D8 → #0099BA → #007791`) e de `pool-secondary` `#007791`.
- Amostragem da referência (não aprovada): `#03B1DF`–`#10A2D0`.

**Conflito de acessibilidade (obrigatório tratar):**

| Combinação | Contraste | AA texto normal (4,5:1) | AA texto grande (3:1) |
|---|---|---|---|
| Branco sobre `#00B4D8` (atual) | 2,46:1 | Reprovado | Reprovado |
| Branco sobre `#0099BA` (meio do gradiente) | 3,34:1 | Reprovado | Aprovado |
| Branco sobre `#007791` (`pool-secondary`) | 5,19:1 | Aprovado | Aprovado |
| `#072A36` sobre `#12B8D8` (proposta) | 6,37:1 | Aprovado | Aprovado |

**Regras:**
- Um único valor aprovado (D-03) vira token; proibido hex solto.
- Se a barra ficar mais clara e mantiver texto branco, o requisito de contraste AA será violado — decisão explícita necessária.
- Atualizar também `:root` (`--pool-primary`, `--pool-secondary`, `--pool-deep`) e as classes derivadas (`.header-pool-minimal`, `.scrolled`) de forma coerente.
- Hover/focus/bordas/fundos derivados devem continuar distinguíveis.

**Aceite:**
- [ ] Azul visivelmente mais claro e aderente à referência aprovada.
- [ ] Contraste mínimo AA comprovado nos textos da barra e CTAs.
- [ ] Estados interativos distinguíveis; nenhum hex órfão.
- [ ] `docs/design-system.md` atualizado com o valor final.

**Dependência:** D-02, D-03 (bloqueantes).

---

### RF-04 — Novas categorias no filtro (ALT-04)

**Requisito.** Acrescentar **Casas**, **Terrenos**, **Sala comercial** e **Lojas** ao seletor "Tipos de Imóveis", preservando as opções atuais.

**Regras:**
- Manter `Todas as categorias` (`value="todos"`) como removedor de restrição.
- Usar valor interno estável e igual ao campo `type` do modelo de imóvel (ex.: `Casa`, `Terreno`, `Sala Comercial`, `Loja`), evitando divergência entre rótulo, valor e dados.
- "Casas" e "Casas em Condomínio" são opções **distintas** (`Casa` vs `Condomínio`) — confirmar em D-06 se a distinção é intencional.
- Sem estoque, o resultado é o estado vazio já existente, com "Limpar filtros".
- Funcionar em conjunto com localização, ordenação, busca por código e `resetAllFilters()`.
- Manter o padrão de plural dos rótulos visíveis.

**Aceite:**
- [ ] 4 novas opções visíveis em desktop e mobile.
- [ ] `todos` restaura a lista completa.
- [ ] Combinação categoria + localidade + ordenação correta.
- [ ] Nenhuma duplicidade semântica não documentada.
- [ ] Console limpo.

---

### RF-05 — Chamada de contato (ALT-05)

**Requisito.** Título passa a "Quer encontrar seu próximo imóvel no Rio Grande do Sul ou Santa Catarina?" e o CTA "Explorar Acervo Completo" é removido **daquela seção**.

**Regras:**
- Manter "Falar com Especialista" acionando `openPrivateVisitModal(...)`.
- Não remover `openCatalogDrawer()` do código; remover apenas esta instância visual (ver D-04).
- Reequilibrar o alinhamento com um único botão (o `flex items-center justify-center` deve ficar harmônico em 375 px).
- Não alterar a linha de apoio ("Estamos à disposição...") sem aprovação.

**Aceite:**
- [ ] Novo título exato, sem resquício de "Porto Alegre ou Florianópolis" nessa seção.
- [ ] Apenas um CTA, centralizado e equilibrado.
- [ ] Modal de contato abre corretamente com o assunto atualizado.

---

### RF-06 — Título e subtítulo da abertura (ALT-06)

**Requisito.**
- Título: "Imóveis de Médio e Alto Padrão em Porto Alegre e Florianópolis"
- Subtítulo: "Curadoria imobiliária para quem busca sofisticação, localização privilegiada e qualidade de vida"

**Regras:**
- Remover "exclusiva" do subtítulo (substituído por "imobiliária").
- Manter um único `<h1>`.
- Preservar legibilidade sobre `bg-black/45` e não sobrepor a tag de cidades nem a caixa de busca.
- **Derivado:** alinhar `<title>` e `meta description` (hoje "Alto Padrão" e "Curadoria exclusiva") e Open Graph, se aprovado em D-13.

**Aceite:**
- [ ] Textos exatos no hero.
- [ ] Quebra de linha adequada em 375, 768 e 1280 px, sem corte na altura fixa do hero.
- [ ] Nenhuma ocorrência de "Curadoria exclusiva" no hero.

---

### RF-07 — "Sobre Nós" (ALT-07)

**Requisito.** Trocar o título da seção `#quemSomos`, substituir os dois parágrafos pelo texto aprovado e remover integralmente o bloco `<ul>` de três pilares.

**Regras:**
- Texto integral e literal do levantamento (seção 5.3), sem misturar conteúdo antigo.
- Remover os 3 `<li>`; não deixar `border-t`/espaçamento órfão.
- Reequilibrar a coluna textual frente à coluna de fotos (`lg:grid-cols-12`), mantendo `items-center`.
- Não alterar a imagem editorial nem o card flutuante.
- Rótulo "Curadoria" do menu: alterar apenas se D-05 confirmar; o `id="quemSomos"` pode permanecer (âncoras existentes) ou ser renomeado com redirect interno — decidir na task.
- Publicação condicionada à validação institucional (D-11).

**Aceite:**
- [ ] Título "Sobre Nós"; texto integral; três tópicos ausentes.
- [ ] Layout equilibrado em 375, 768 e 1280 px.
- [ ] Header/nav sem link quebrado.
- [ ] Nenhuma alegação nova além do texto fornecido.

---

### RF-08 — Seção final "De Porto Alegre a Florianópolis" (ALT-08)

**Requisito.** Criar uma seção editorial, com título e quatro parágrafos aprovados e galeria de imagens das duas capitais, posicionada como última seção de conteúdo do site.

**Regras de conteúdo:**
- Título e 4 parágrafos exatos.
- Abordagem de **conexão** entre as capitais, não duas histórias isoladas.
- Galeria com 3–4 fotos de Porto Alegre e ~3 de Florianópolis, mínimo **2** de Florianópolis.
- Toda imagem com `alt` descritivo e identificação correta do local.
- Não publicar imagens com marca do Google Lens (`WA0053`, `WA0060`) ou marcas de interface.

**Regras de experiência e acessibilidade (se D-07 = sob clique):**
- Controle por `<button>` acessível por teclado.
- `aria-expanded` refletindo o estado.
- Conteúdo permanece no HTML (não renderizado por JS tardio) para SEO e leitores de tela.
- Foco visível; `Esc` não é necessário (não é modal), mas o estado deve ser anunciado.
- Se o texto ficar sempre visível, distribuir em blocos para não formar parede de texto no mobile.

**Regras técnicas:**
- Layout responsivo (grid 1 coluna no mobile, composição editorial no desktop).
- Imagens otimizadas (WebP, `width`/`height`, `loading="lazy"`, `decoding="async"`), sem base64.
- Respeitar `prefers-reduced-motion` se houver animação.
- Não adicionar dependências.
- Posição conforme D-09; sem item de menu obrigatório (D-10).

**Aceite:**
- [ ] Seção presente na posição aprovada, com título e 4 parágrafos literais.
- [ ] Galeria com a distribuição mínima acordada e identificação correta.
- [ ] Imagens licenciadas, sem marcas de ferramenta, com `alt`.
- [ ] Interação (se houver) acessível e sem erros de console.
- [ ] Legível em 375 px sem bloco denso.
- [ ] Fatos históricos e alegações validados (D-11).

**Dependências:** D-07, D-08, D-09, D-11 (bloqueantes) + ativos de imagem licenciados.

---

### RF-09 — Manter telefone atual (ALT-09)

**Requisito.** Não substituir os números publicados; garantir consistência entre número exibido e destino do `wa.me`.

**Regras:**
- Nenhuma alteração de número nesta entrega.
- Verificar consistência dos 4 pontos de contato (header, rodapé, modal de cidades, `openPropertyModal`).
- Registrar que a manutenção é **temporária**, não aprovação definitiva.

**Aceite:**
- [ ] Números exibidos iguais aos links `wa.me` correspondentes.
- [ ] Nenhum número novo introduzido.
- [ ] Divergência 51/48 documentada e esclarecida (D-12).

---

### RF-10 — Consistência de SEO (derivado, condicionado a D-13)

**Requisito.** Alinhar `<title>`, `meta description` e Open Graph (se existirem) à nova redação.

**Aceite:**
- [ ] Metadados refletem "Médio e Alto Padrão" e "Curadoria imobiliária", se aprovado.
- [ ] Sem meta description duplicada ou ausente.
- [ ] Nenhuma mudança de URL/estrutura.

---

## 6. Requisitos não funcionais

| ID | Requisito | Critério verificável |
|---|---|---|
| RNF-01 | Acessibilidade AA | Contraste ≥ 4,5:1 (texto normal) e ≥ 3:1 (grande); foco visível; teclado em todos os controles novos |
| RNF-02 | Responsividade | Sem overflow horizontal, corte ou sobreposição em 375, 768 e 1280 px |
| RNF-03 | Performance | Sem novas dependências; novas imagens em WebP com dimensões declaradas e lazy loading; não aumentar o HTML de forma relevante |
| RNF-04 | SEO técnico | Um `<h1>`; `title`/`description` coerentes; conteúdo da nova seção indexável no HTML |
| RNF-05 | Consistência visual | Cores só por tokens; nenhuma alteração nos 6 efeitos assinatura |
| RNF-06 | Sem backend | Nenhuma chamada de API, formulário real ou serviço novo |
| RNF-07 | Rastreabilidade | Cada texto publicado corresponde ao levantamento, sem invenção |
| RNF-08 | Regressão funcional | Filtros, busca por código, modal, lightbox, drawer, formulários e WhatsApp continuam operando |
| RNF-09 | Manutenibilidade | Alterações localizadas e comentadas no padrão do arquivo; sem refatoração ampla (plan-001 fora deste escopo) |
| RNF-10 | Console limpo | Zero erros e zero warnings relevantes |

---

## 7. Matriz de priorização

### 7.1 Por complexidade × prontidão

| Complexidade | Pronto para Dev | Requer Definição | Bloqueado por ativo externo |
|---|---|---|---|
| **Baixa** | RF-02*, RF-04, RF-05*, RF-06, RF-09, RF-10 | — | — |
| **Média** | RF-07 | RF-03 | RF-01 |
| **Alta** | — | RF-08 | — |

`*` Executável isoladamente; o **aceite conjunto** de RF-02 + RF-05 depende de D-04.

### 7.2 Prioridade de negócio × risco técnico

| Ordem | Requisito | Valor para o cliente | Risco técnico | Justificativa da ordem |
|---|---|---|---|---|
| 1 | RF-05 | Alto | Baixo | Texto explícito, mudança isolada |
| 2 | RF-06 | Alto | Baixo | Texto explícito; validar quebra de linha |
| 3 | RF-04 | Alto | Baixo | Funcional, testável, estado vazio já existe |
| 4 | RF-02 | Médio | Baixo | Depende de D-04 para aceite |
| 5 | RF-07 | Alto | Baixo | Texto pronto; gate jurídico na publicação |
| 6 | RF-09 | Médio | Baixo | Verificação, sem alteração |
| 7 | RF-10 | Médio | Baixo | Condicionado a D-13 |
| 8 | RF-03 | Alto | Médio | Exige decisão de escopo + contraste |
| 9 | RF-01 | Alto | Médio | Bloqueado por D-01 |
| 10 | RF-08 | Alto | Alto | Layout, ativos, licenças, fatos |

### 7.3 Ondas sugeridas (após validação)

- **Onda 1 — Conteúdo e filtros (sem dependências):** RF-05, RF-06, RF-04, RF-07, RF-09. ✅ executada em 18/11/2026 (com RF-02, RF-10 e D-04/D-05).
- **Onda 2 — Navegação e cor (após D-02/D-03/D-04):** RF-02, RF-03, RF-10. ✅ executada em 18/11/2026.
- **Onda 3 — Marca (após D-01):** RF-01. ⛔ aguardando o arquivo da marca.
- **Onda 4 — Seção editorial (após D-07/D-08/D-09/D-11 e ativos):** RF-08. ⛔ bloqueada.

---

## 8. Dependências de ativos e informações

| ID | Necessário | Para | Status |
|---|---|---|---|
| A-01 | Marca em SVG ou PNG com transparência, alta resolução, versão final aprovada | RF-01 | **Aguardando envio** (solicitante vai fornecer) |
| A-02 | Confirmação do hex final + escopo de aplicação | RF-03 | **Resolvido** (`#12B8D8`, barra apenas) |
| A-03 | 3–4 fotos de Porto Alegre e ~3 de Florianópolis, licenciadas, sem marca d'água | RF-08 | **Ausente/parcial** (4 referências, 2 com marca do Google Lens e licença desconhecida) |
| A-04 | Definição de layout da seção histórica | RF-08 | **Ausente** |
| A-05 | Validação jurídica e factual dos textos | RF-07, RF-08 | **Ausente** |
| A-06 | Confirmação de qual telefone é o vigente | RF-09 | **Parcial** |
| A-07 | Anexos do levantamento (imagens, áudios, transcrição, `poafloripa6.html`) | Auditoria | **Ausentes no repositório** |
| A-08 | Wireframe ou referência visual da galeria | RF-08 | Opcional |

---

## 9. Limitações, bloqueios e fora de escopo

> **Atenção:** os itens desta seção **não devem** ser convertidos em tasks de desenvolvimento. Eles geram tarefas de decisão, aquisição de ativo ou validação — não de código.

### 9.1 Bloqueios

| ID | Bloqueio | Consequência | Como destravar |
|---|---|---|---|
| B-01 | Marca final inexistente em formato de produção | RF-01 não pode ser concluído com qualidade; a foto `WA0039` não serve | Tiago envia SVG/PNG aprovado |
| B-02 | Imagens da seção histórica com marca do Google Lens e licença não comprovada | Publicação ilegal/visualmente inadequada | Substituir por fotos próprias ou licenciadas |
| B-03 | Conflito entre "clarear o azul" e contraste AA com texto branco | Necessidade de decisão de design, não de código | Aprovar D-03 (texto escuro ou barra mais escura) |
| B-04 | Perda de acesso ao drawer no desktop ao executar RF-02 + RF-05 | Funcionalidade existente deixa de ser alcançável | Definir D-04 |
| B-05 | Alegações institucionais não validadas ("assessoria jurídica", "segurança patrimonial", "exclusividade", IDH, segurança) | Risco jurídico/reputacional | Validação de Tiago/jurídico |
| B-06 | Anexos-fonte ausentes no repositório | Impossível auditar imagens, áudios e o `poafloripa6.html` | Versionar os anexos |
| B-07 | Ambiguidade dos dois telefones publicados | Aceite de RF-09 inconclusivo | Esclarecer D-12 |

### 9.2 Fora de escopo (não implementar)

1. Redesenho completo do site ou mudança de identidade além da marca e do azul.
2. Remoção geral do catálogo, do drawer, do modal ou de imóveis.
3. Troca de número de telefone, e-mail, CRECI ou redes sociais.
4. Expansão automática de "Porto Alegre e Florianópolis" para "Rio Grande do Sul e Santa Catarina" em outros textos.
5. Definição de novo formato de galeria para os imóveis ou do mosaico de 5 fotos.
6. Migração para CMS, banco de dados, API, backend ou formulários reais (tema do `docs/prd-evolucao-producao.md`).
7. Modularização do `index.html` em `assets/css`, `assets/js` (plan-001) — não é pré-requisito desta entrega.
8. Extração das imagens base64 para arquivos, salvo se estritamente necessário para RF-08.
9. Revisão editorial dos textos do cliente (copywriting, gramática, SEO editorial).
10. Novas animações, novos efeitos ou novas dependências (fontes, ícones, bibliotecas).
11. Alterações na newsletter, no rodapé, no modal de contato ou no WhatsApp flutuante não solicitadas.
12. Inclusão das imagens `WA0057`, `WA0059` e `WA0061` (sem vínculo com requisito).
13. Deploy em produção.
14. Aquisição/compra de licenças de imagem pela equipe de desenvolvimento.
15. Publicação de conteúdo com marca d'água de ferramenta de busca.

### 9.3 Limitações técnicas conhecidas

| ID | Limitação | Impacto |
|---|---|---|
| L-01 | Arquivo único de ~1 MB com base64 | Edições exigem cuidado; novas imagens não devem entrar em base64 |
| L-02 | Tailwind CDN sem build | Sem purge/JIT local; tokens dependem do `tailwind.config` inline |
| L-03 | Header fixo `h-20` + hero `h-[500px]` | Textos mais longos podem estourar no mobile |
| L-04 | Logo duplicada manualmente (header e rodapé) | Risco de divergência a cada alteração |
| L-05 | Sem testes automatizados | Validação é manual, via `skills/qa-validacao-web.md` |
| L-06 | Menu mobile não é navegação | Remoção de item no mobile é inaplicável hoje |
| L-07 | Link do Gemini exige autenticação | Referência da marca não é verificável |

---

## 10. Estratégia de validação (QA)

Base: `skills/qa-validacao-web.md`.

1. Servir localmente (`npx serve .`) e abrir no navegador.
2. Console sem erros/warnings.
3. Fluxos: filtros (incluindo as 4 novas categorias + combinações), ordenação, busca por código, modal (mosaico, lightbox, `Esc`), drawer (pela entrada definida em D-04), newsletter, modal de contato, links `wa.me`.
4. Responsivo em 375 / 768 / 1280 px, com checagem de sobreposição no hero e na nova seção.
5. Contraste medido nos textos sobre a barra e nos CTAs.
6. Navegação por teclado na nova seção e nos controles alterados.
7. Lighthouse ≥ 90 em Performance, SEO, A11y e Best Practices.
8. Regressão visual dos 6 efeitos assinatura.
9. Conferência literal dos textos contra o levantamento (seção 5).
10. Registrar o resultado no plano 003.

---

## 11. Rastreabilidade

| Origem | Requisito | Decisões | Ativos | Bloqueio |
|---|---|---|---|---|
| ALT-01 | RF-01 | D-01 | A-01 | B-01 |
| ALT-02 | RF-02 | D-04 | — | B-04 |
| ALT-03 | RF-03 | D-02, D-03 | A-02 | B-03 |
| ALT-04 | RF-04 | D-06 | — | — |
| ALT-05 | RF-05 | D-04 | — | B-04 |
| ALT-06 | RF-06, RF-10 | D-13 | — | — |
| ALT-07 | RF-07 | D-05, D-11 | A-05 | B-05 |
| ALT-08 | RF-08 | D-07, D-08, D-09, D-10, D-11 | A-03, A-04, A-08 | B-02, B-05 |
| ALT-09 | RF-09 | D-12 | A-06 | B-07 |
| Governança | — | D-14, D-15 | A-07 | B-06 |

---

## 12. Próximos passos

1. ~~Tiago/Evandro respondem D-01 a D-04 (bloqueantes)~~ — D-02, D-03 e D-04 respondidas em 18/11/2026; **D-01 pendente** (arquivo da marca).
2. Aprovação ou ajuste deste PRD.
3. Execução de [tasks.md](../tasks.md) — Onda 1 e Onda 2 concluídas; 8 tasks gated restantes (G2, G3).
4. Execução por ondas, com validação QA ao final de cada uma.
5. Deploy somente após aprovação explícita (regra 8 do `agents.md`).

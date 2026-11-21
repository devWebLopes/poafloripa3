# PRD — Ajuste visual da seção “Porto Alegre & Florianópolis”

- **Produto:** Poa Floripa Imóveis
- **Versão:** 1.0
- **Data:** 20/11/2026
- **Status:** Implementado, ajustado e validado em 21/11/2026 (local/preview; deploy não executado)
- **Seção afetada:** `section#duasCapitais`
- **Plano relacionado:** [Plano 004](../plans/plan-004-prd-secao-duas-capitais.md)

## 1. Resumo executivo

A seção “De Porto Alegre a Florianópolis: Duas Capitais, uma História de Qualidade de Vida” deve deixar de ser um bloco branco predominantemente textual e passar a funcionar como uma experiência editorial imersiva. A solução usa quatro fotografias existentes como fundo integral, alternadas entre as duas cidades, com crossfade e movimento Ken Burns suave inspirados no hero da página.

O conteúdo atual será preservado sem reescrita. A harmonia virá da reorganização da hierarquia, da largura de leitura, dos espaçamentos, do contraste e do ritmo entre os parágrafos. A solução continuará minimalista, sem bibliotecas novas e com controles acessíveis para pausar ou selecionar os fundos.

## 2. Contexto e problema

### 2.1 Estado atual

- A seção está entre `#quemSomos` e `#contatoSection`.
- O título e os quatro parágrafos ficam sobre fundo branco.
- O primeiro parágrafo tem destaque; os dois centrais usam duas colunas no desktop; o fechamento possui barra lateral azul.
- Há um comentário no HTML reservando uma futura galeria, mas nenhuma imagem é exibida.
- O hero já estabelece a linguagem visual desejada: imagens sobrepostas, véu escuro, crossfade e `.motion-canvas`.

### 2.2 Problema percebido

O texto está correto e hierarquizado, porém a seção ainda parece desconectada do caráter aspiracional das duas cidades. Acrescentar uma galeria abaixo do texto aumentaria a altura e criaria dois blocos concorrentes. Usar as imagens como cenário unifica narrativa e fotografia, desde que a leitura continue sendo a prioridade.

## 3. Objetivos

1. Tornar a seção mais harmônica, sofisticada e conectada visualmente a Porto Alegre e Florianópolis.
2. Reaproveitar a linguagem de movimento do hero sem duplicar sua composição.
3. Preservar literalmente o título e os quatro parágrafos vigentes.
4. Garantir leitura confortável em celular, tablet e desktop.
5. Aplicar movimento discreto, controlável e compatível com redução de movimento.
6. Evitar regressão relevante de performance com imagens otimizadas e carregamento tardio.

### 3.1 Não objetivos

- Reescrever ou resumir os textos.
- Alterar fatos históricos, dados comerciais, contatos ou imóveis.
- Modificar o hero, a seção “Sobre Nós” ou a newsletter.
- Criar galeria, lightbox, vídeo ou nova dependência.
- Buscar imagens externas ou publicar sem confirmação de licença.

## 4. Direção de experiência e composição

### 4.1 Conceito

**Duas capitais, uma paisagem em movimento.** A seção será um painel editorial de fundo integral. As cidades alternam silenciosamente enquanto o texto permanece estável, comunicando conexão sem exigir interação.

### 4.2 Estrutura visual

1. `section#duasCapitais` relativa, com `overflow: hidden` e fallback em `pool-abyss`.
2. Quatro camadas fotográficas absolutas, uma visível por vez.
3. Véu escuro constante em petróleo e gradiente adicional atrás do conteúdo.
4. Conteúdo em primeiro plano, alinhado à esquerda no desktop e sem painel opaco pesado.
5. Controles discretos no rodapé da seção: quatro indicadores selecionáveis e botão pausar/reproduzir.

### 4.3 Hierarquia do texto

- **Eyebrow:** mantém “Porto Alegre & Florianópolis”, em caixa-alta e azul claro/branco.
- **Título:** largura aproximada de 18–22 caracteres por linha visual, `font-serif`, branco e com respiro inferior maior.
- **Introdução:** até 70 caracteres por linha, corpo maior e branco com alta opacidade.
- **Parágrafos centrais:** uma coluna até 1023 px; duas colunas a partir de 1024 px, com separação por espaço e borda sutil no segundo bloco.
- **Fechamento:** bloco próprio com borda `pool`, fundo petróleo translúcido e largura menor que a grade central.

O texto não deve ficar centralizado: a leitura longa permanece alinhada à esquerda. Nenhuma palavra será embutida nas fotografias.

### 4.4 Dimensões e responsividade

| Faixa | Comportamento |
|---|---|
| 320–639 px | Altura automática; `padding` vertical mínimo de 72 px; título 36–40 px; corpo em uma coluna; controles após o texto |
| 640–1023 px | `padding` de 88–104 px; título 44–52 px; largura de conteúdo limitada; uma coluna |
| ≥ 1024 px | `padding` de 112–128 px; título 52–60 px; parágrafos centrais em duas colunas; conteúdo máximo de 1120 px |

Não usar altura fixa. A seção precisa crescer com o texto, zoom do navegador e fontes carregadas, sem corte ou sobreposição.

## 5. Curadoria de imagens

### 5.1 Sequência selecionada

| Ordem | Origem | Dimensões/peso atuais | Papel visual | Tratamento esperado |
|---:|---|---:|---|---|
| 1 | `assets/img/img-poa-01.jpg` | 5554×3117; 15,1 MB | Porto Alegre noturna; abertura de maior impacto | WebP até 1600 px; foco central; escurecimento moderado |
| 2 | `assets/img/img-floripa-01.jpg` | 1057×1280; 166,9 KB | Praia de Florianópolis; contraste de luz e natureza | WebP sem ampliar; crop responsivo com foco no barco e na água |
| 3 | `assets/img/img-poa-03.jpg` | 1072×1181; 109,5 KB | Usina do Gasômetro ao entardecer; referência histórica | WebP sem ampliar; validar crop para preservar edifício e chaminé |
| 4 | `assets/img/img-floripa-03.jpg` | 1125×740; 95,8 KB | Ponte Hercílio Luz noturna; encerramento icônico | WebP sem ampliar; foco central ligeiramente abaixo do eixo |

**Ordem narrativa:** metrópole → natureza → patrimônio → conexão. A sequência alterna as cidades e evita duas imagens noturnas consecutivas.

### 5.2 Nomes dos derivados

- `duas-capitais-poa-noturna.webp`
- `duas-capitais-floripa-praia.webp`
- `duas-capitais-poa-gasometro.webp`
- `duas-capitais-floripa-ponte.webp`

Os JPGs originais não devem ser sobrescritos. Nenhum derivado pode ampliar uma imagem menor que o tamanho de saída.

### 5.3 Ativos não selecionados

| Arquivo | Motivo |
|---|---|
| `img-poa-054.jpg` | Possui marca visível de ferramenta no canto inferior esquerdo; proibido publicar |
| `img-floripa-02.jpg` | Possui marca visível de ferramenta no canto inferior esquerdo; proibido publicar |
| `img-poa-02.jpg` | Cena diurna válida, mas menos expressiva e redundante com o Gasômetro selecionado |
| `img-poa-04.jpg` | Proporção adequada, porém menor impacto visual para a narrativa principal |
| `img-floripa-04.jpg` | Repete a Ponte Hercílio Luz com menor definição e composição menos equilibrada |

### 5.4 Gate de publicação

A presença dos arquivos no repositório não comprova licença. Antes de publicar, o responsável pelo negócio deve confirmar por escrito que os quatro selecionados podem ser usados comercialmente. Sem essa confirmação, a implementação pode existir apenas em ambiente local/preview.

## 6. Movimento e transições

### 6.1 Alternância

- Permanência de cada slide: **9 segundos** (ajustado de 12s em 21/11/2026; ver nota de revisão abaixo).
- Crossfade: **1,4 segundo**, usando opacidade e curva `ease-in-out`.
- A próxima imagem só entra após estar carregada e decodificada; não pode ocorrer flash branco.
- A rotação pausa quando a aba fica oculta e retoma sem avançar várias imagens de uma vez.
- Seleção manual reinicia a contagem a partir do slide escolhido.

### 6.2 Movimento de câmera

- Ken Burns de **9 segundos** por imagem — igual à permanência do slide (ajustado de 28–32s; ver nota de revisão abaixo).
- Escala máxima de **1.12** e deslocamento máximo de **2,4%** por eixo (ajustado de 1.06 / 1%).
- Direções alternadas para evitar repetição mecânica.
- Somente `transform` e `opacity`, sem animar dimensões ou posição de layout.

### 6.3 Nota de revisão (21/11/2026 — correção de percepção de movimento)

A primeira implementação usava Ken Burns de 30s com permanência de slide de 12s: a troca de imagem acontecia com a animação em ~40% do percurso, numa curva `ease-in-out` que começa devagar — o zoom nunca chegava perto da escala máxima antes de sumir, e o usuário percebia a seção como estática. A correção alinha a duração do Ken Burns ao tempo de exibição do slide (zoom completo e visível em cada ciclo) e amplia a escala/deslocamento para reforçar a percepção, mantendo o efeito discreto e dentro do espírito minimalista do site. `prefers-reduced-motion`, pausa e seleção manual permanecem com o mesmo comportamento.

### 6.3 Controle e redução de movimento

- Botão com alvo mínimo de 44×44 px e rótulos acessíveis “Pausar imagens de fundo” / “Reproduzir imagens de fundo”.
- Indicadores permitem escolher qualquer uma das quatro imagens por teclado e toque.
- Com `prefers-reduced-motion: reduce`, usar apenas a primeira imagem, sem autoplay, crossfade ou Ken Burns; o controle de reprodução não deve iniciar animação contra a preferência do sistema.
- As imagens são decorativas: `alt=""` e `aria-hidden="true"`; mudanças não usam `aria-live`.

## 7. Requisitos funcionais

| ID | Requisito |
|---|---|
| RF-01 | Converter a seção atual em composição de fundo integral sem mudar seu `id`, posição ou hierarquia `h2` |
| RF-02 | Manter literalmente o eyebrow, o título e os quatro parágrafos atuais |
| RF-03 | Alternar os quatro ativos selecionados na ordem definida, com crossfade e movimento suave |
| RF-04 | Disponibilizar seleção manual e pausa/reprodução com estado visual e nome acessível |
| RF-05 | Manter texto e fallback petróleo funcionais se JavaScript ou alguma imagem falhar |
| RF-06 | Carregar e decodificar a próxima imagem antes de torná-la visível |
| RF-07 | Suspender timers quando a página não estiver visível |
| RF-08 | Remover o comentário da galeria pendente após a nova composição substituir essa necessidade |

## 8. Requisitos não funcionais

### 8.1 Legibilidade e acessibilidade

- Contraste mínimo WCAG AA: 4,5:1 para corpo e 3:1 para título grande, medido em cada um dos quatro fundos.
- O véu pode variar por ativo entre 65% e 78%, mas a troca não pode causar pulsação visual forte.
- Corpo mínimo de 16 px no mobile; largura recomendada de 50–75 caracteres por linha.
- Foco visível nos controles; ordem de tabulação previsível; nenhum conteúdo essencial depende da cor ou do movimento.
- Texto íntegro e selecionável, nunca convertido em imagem.

### 8.2 Performance

- WebP com qualidade inicial aproximada de 80 e inspeção visual obrigatória.
- `img-poa-01.jpg` deve ser reduzida para no máximo 1600 px de largura; os demais arquivos não serão ampliados.
- Meta de até **220 KB por derivado** e **700 KB no conjunto**; exceção somente após comparação visual documentada.
- A seção abaixo da dobra não pode competir com o LCP do hero: iniciar carregamento próximo ao viewport e carregar os slides seguintes progressivamente.
- Definir dimensões/cobertura por CSS para manter CLS igual a zero.
- Sem bibliotecas novas; usar CSS e JavaScript puro.

### 8.3 Compatibilidade e resiliência

- Funcionar nos navegadores modernos já atendidos pelo site.
- Sem JavaScript, exibir a primeira imagem estática, o véu e todo o texto.
- Em falha de imagem, o fundo `pool-abyss` mantém contraste e leitura.
- Nenhum overflow horizontal em 375, 768, 1280 e 1920 px.

## 9. Critérios de aceite

### 9.1 Visual e conteúdo

- [x] A seção usa apenas os quatro arquivos selecionados, na ordem POA → Floripa → POA → Floripa.
- [x] Nenhum ativo com marca de ferramenta aparece na página.
- [x] Título e quatro parágrafos permanecem idênticos ao conteúdo vigente.
- [x] Texto não encobre os principais pontos focais após validação dos crops em 375, 768, 1280 e 1920 px.
- [x] Leitura confortável e contraste AA comprovado nos quatro fundos.
- [x] A seção mantém identidade própria e não parece uma cópia literal do hero.

### 9.2 Movimento e interação

- [x] Crossfade sem flash, salto ou slide lateral; permanência e duração conforme especificação.
- [x] Movimento discreto, sem tremor ou perda visível de nitidez.
- [x] Pausa, reprodução e seleção manual funcionam por mouse, toque e teclado.
- [x] A aba oculta não mantém timers ativos.
- [x] `prefers-reduced-motion` apresenta composição estática.

### 9.3 Técnica e regressão

- [x] Derivados respeitam orçamento, nomes e limite de dimensões.
- [x] Console sem novos erros ou avisos relevantes.
- [x] CLS da seção igual a zero e LCP do hero no mesmo elemento/tamanho com e sem a seção (mediana 168 ms vs 156 ms em 3 execuções), sem regressão atribuível.
- [x] Fluxos existentes de filtros, modais, drawer, formulários e WhatsApp permanecem funcionando.
- [x] Efeitos assinatura existentes continuam intactos.
- [x] Nenhuma dependência ou deploy de produção é realizado sem aprovação explícita.

## 10. Plano de implementação proposto

1. Confirmar licença e aprovar os crops dos quatro ativos.
2. Gerar os quatro WebP sem alterar os originais.
3. Criar as camadas, véus, layout editorial e controles no `index.html`.
4. Implementar rotação, pré-carregamento, pausa, visibilidade da aba e seleção manual em JavaScript puro.
5. Adicionar regras de `prefers-reduced-motion` e fallback sem JavaScript.
6. Executar `skills/qa-validacao-web.md`, registrar evidências no plano e atualizar a documentação afetada.

### 10.1 Arquivos previstos para a futura implementação

- `index.html`
- `assets/img/duas-capitais-*.webp`
- `docs/design-system.md` se o padrão de slideshow editorial for incorporado aos efeitos assinatura
- `docs/architecture.md` se o comportamento for extraído para `assets/js/effects.js`
- `plans/plan-004-prd-secao-duas-capitais.md`

## 11. Dependências e decisões

| ID | Decisão | Responsável | Status | Bloqueia publicação em produção? |
|---|---|---|---|---|
| D-DC-01 | Confirmar licença comercial dos quatro ativos selecionados | Negócio | **Confirmado em 21/11/2026** | Resolvido |
| D-DC-02 | Aprovar os crops de praia e Gasômetro em desktop | Negócio/design | **Confirmado em 21/11/2026** | Resolvido |
| D-DC-03 | Validar juridicamente/factualmente o texto institucional já publicado | Negócio/jurídico | **Confirmado em 21/11/2026** | Resolvido |
| D-DC-04 | Aprovar visualmente o nível final do véu escuro | Negócio/design | **Confirmado em 21/11/2026** | Resolvido |

## 12. Status de implementação e fora de escopo

A implementação descrita neste PRD foi executada em `index.html` e validada em ambiente local (ver evidências em [plan-004](../plans/plan-004-prd-secao-duas-capitais.md)). As quatro decisões (D-DC-01 a D-DC-04) foram confirmadas pelo solicitante em 21/11/2026, incluindo a correção de percepção de movimento registrada em 6.3. **Nenhum deploy em produção foi realizado**; a mudança segue apenas commitada/local até autorização explícita de publicação.

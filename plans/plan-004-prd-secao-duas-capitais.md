# Plano 004 — PRD do ajuste da seção Duas Capitais

- **Status:** Implementado, ajustado e validado em 21/11/2026 (local/preview; sem deploy em produção)
- **Agente líder:** Arquiteto ([agents/arquiteto.md](../agents/arquiteto.md))
- **Apoio:** Frontend, Conteúdo & Dados, QA & Deploy
- **Skills:** html-semantico-seo, tailwind-design-system, vanilla-js-modular, otimizacao-imagens, qa-validacao-web, UX Designer
- **Fonte do pedido:** solicitação de 20/11/2026 para harmonizar a seção `#duasCapitais`, aplicar imagens de fundo alternadas e movimentos suaves

## Objetivo

Documentar uma solução visual e técnica implementável para a seção “Porto Alegre & Florianópolis”, preservando o texto aprovado, a identidade minimalista, a acessibilidade e a performance do site.

## Entregáveis

- PRD em [docs/prd-secao-duas-capitais.md](../docs/prd-secao-duas-capitais.md).
- Curadoria justificada dos arquivos existentes em `assets/img/`.
- Especificação do layout, transições, movimento, responsividade e acessibilidade.
- Implementação no `index.html` e quatro derivados WebP em `assets/img/`.
- Evidências de QA em navegador (desktop, mobile e movimento reduzido).

## Etapas

- [x] Ler regras, arquitetura, padrões, design system, agentes e skills aplicáveis.
- [x] Inspecionar a seção vigente e o comportamento do hero usado como referência.
- [x] Avaliar visualmente as imagens disponíveis e levantar dimensões/peso.
- [x] Redigir o PRD e registrar ativos selecionados, descartes e bloqueios.
- [x] Atualizar o índice de documentação.
- [x] Validar links, escopo e aderência às regras do projeto.
- [x] Confirmar a licença comercial dos quatro ativos com o solicitante.
- [x] Gerar os derivados WebP sem sobrescrever os JPGs originais.
- [x] Implementar fundo, véu, layout editorial, controles e movimento no `index.html`.
- [x] Executar a skill `qa-validacao-web` e registrar as evidências.
- [x] Diagnosticar e corrigir a percepção de "seção estática" reportada em 21/11/2026.
- [x] Confirmar com o solicitante D-DC-02, D-DC-03 e D-DC-04.

## Critérios de aceite do PRD
- O PRD define quais imagens usar e quais não usar, sem pressupor licença não comprovada.
- O texto vigente não é reescrito nem recebe alegações novas.
- Movimento e alternância respeitam `prefers-reduced-motion` e oferecem pausa.
- A especificação preserva contraste, leitura, responsividade e carregamento tardio das imagens.
- Nenhuma dependência, alteração de código da página ou deploy faz parte desta fase.

## Validação do PRD

- [x] PRD e plano com links locais válidos.
- [x] Nenhum dado comercial, histórico ou de imóvel inventado.
- [x] Nenhum arquivo de código alterado.
- [x] Nenhuma dependência adicionada e nenhum deploy executado.

## Riscos

| Risco | Mitigação |
|---|---|
| Texto longo perder legibilidade sobre fotografias | Véu escuro constante, painel translúcido, largura de linha limitada e teste de contraste por slide |
| Animações competirem com a leitura | Movimento lento, crossfade sem deslocamento, controle de pausa e modo reduzido estático |
| Imagens pesadas piorarem a performance | Derivados WebP, largura máxima de 1600 px, lazy-load e orçamento por arquivo |
| Publicar imagem sem licença ou com marca de ferramenta | Gate de licença e exclusão dos arquivos com marca visível |
| Duplicar visualmente o hero | Reutilizar a linguagem de movimento, mas com composição editorial e ritmo próprios |

## Execução (21/11/2026)

- Licença comercial dos quatro ativos confirmada pelo solicitante em 21/11/2026 (D-DC-01).
- Derivados gerados por `ffmpeg` (WebP, qualidade 74–80, `compression_level 6`), sem sobrescrever os JPGs:

| Arquivo | Dimensões | Peso |
|---|---:|---:|
| `duas-capitais-poa-noturna.webp` | 1440×808 | 211 KB |
| `duas-capitais-floripa-praia.webp` | 1057×1280 | 117 KB |
| `duas-capitais-poa-gasometro.webp` | 1072×1181 | 63 KB |
| `duas-capitais-floripa-ponte.webp` | 1125×740 | 54 KB |
| **Total** | — | **445 KB** |

- `img-poa-01.jpg` foi reduzida para 1440 px e recebeu leve ajuste de exposição (gamma 1.3, brilho +0,05, saturação +8%) para permanecer perceptível sob o véu noturno.
- `index.html`: quatro camadas absolutas, crossfade de 1,4 s, Ken Burns de 30 s (escala máxima 1,06 e deslocamento máximo de 1%), véu responsivo, indicadores, pausa/reprodução, pausa em aba oculta, carregamento decodificado antes da troca e `prefers-reduced-motion`.
- Nenhuma dependência, biblioteca ou alteração no hero foi adicionada.

## Validação da implementação

- [x] Texto, título e hierarquia preservados; nenhuma reescrita.
- [x] Ordem POA → Floripa → POA → Floripa e apenas os quatro ativos aprovados.
- [x] Desktop 1440 px: seção com 1219 px, título 56 px, corpo 18 px e `scrollWidth` 1425 px (sem overflow).
- [x] Mobile 375 px: seção com 1518 px, título 36 px, corpo 16 px e `scrollWidth` 375 px (sem overflow).
- [x] Rotação observada de 0 → 1 após 12,8 s; crossfade de 1,4 s.
- [x] Pausa: `aria-pressed="true"`, rótulo “Reproduzir imagens de fundo”, ícone de play visível e movimento congelado.
- [x] Seleção manual: terceiro indicador ativa o slide 2, atualiza `aria-pressed` e mantém o estado de pausa.
- [x] `prefers-reduced-motion`: slide 0 permanece estático após 13 s, sem classe de animação, controles ocultos e transição de 0 s.
- [x] Contraste mínimo medido nos quatro fundos (pior pixel sob cada bloco de texto): corpo 8,10:1 no desktop e 9,03:1 no mobile; título 9,09:1 e 10,20:1 — acima de AA.
- [x] CLS da seção igual a zero (camadas absolutas com `width`/`height`); LCP do hero no mesmo elemento e tamanho em 3 execuções com e sem a seção (mediana 168 ms vs 156 ms), sem regressão atribuível.
- [x] Sem overflow horizontal em 375, 768, 1280 e 1920 px.
- [x] Console sem erros ou avisos da implementação (permanece apenas o aviso pré-existente do Tailwind CDN).
- [x] Regressão: 6 cards renderizados, modal e drawer abrem/fecham, filtros reaplicam 6 cards, hero alterna e 4 links de WhatsApp permanecem.
- [x] Orçamento: 445 KB no conjunto e 211 KB no maior derivado.
- [x] Nenhum deploy em produção executado.

## Correção de percepção de movimento (21/11/2026, continuação)

**Relato do solicitante:** ao abrir o `index.html` direto no navegador (`file://`), a seção pareceu fixa, com uma imagem só e sem movimento perceptível.

**Diagnóstico:** reproduzido com Playwright (Chromium), tanto via `http://localhost` quanto via `file://`. A rotação de slides e o carregamento das 4 imagens funcionavam sem erros de console em ambos os casos (slide 0 → 1 confirmado após ~12,8 s). A causa raiz não era um bug funcional, e sim de calibração: o Ken Burns durava 30 s enquanto cada slide ficava visível só 12 s, então a troca ocorria com a animação em ~40% do percurso (dentro da fase lenta inicial do `ease-in-out`), tornando o zoom quase imperceptível antes da imagem sumir no crossfade.

**Correção aplicada em `index.html`:**
- Duração do Ken Burns alinhada à permanência do slide: 30s → **9s** (igual à nova permanência).
- Permanência do slide: 12s → **9s**.
- Escala máxima: 1.06 → **1.12**; deslocamento máximo: 1% → **2,4%** por eixo.
- Crossfade (1,4 s), pausa, seleção manual, pausa em aba oculta e `prefers-reduced-motion` mantidos sem alteração.

**Validação (Playwright, Chromium):**
- [x] Transform do slide ativo evolui de `scale(1)` em t=0,2s para `scale(1,1156)` em t=8,2s (zoom quase completo visível antes da troca) — antes da correção, a mesma leitura ficaria perto de `scale(1,02)`.
- [x] Prints em t=0s e t=8s mostram deslocamento/zoom perceptível no enquadramento da cidade.
- [x] `prefers-reduced-motion: reduce`: `dc-animating` ausente, controles ocultos (`display: none`), slide permanece em 0 após 10 s.
- [x] Regressão: 6 cards de imóveis renderizados; sem erros de console em `http://localhost` nem em `file://`.
- [x] Rotação confirmada também via `file://` (cenário relatado pelo solicitante), sem diferença de comportamento frente ao servidor local.

**Decisões confirmadas pelo solicitante em 21/11/2026:** D-DC-02 (crops), D-DC-03 (texto institucional) e D-DC-04 (nível do véu) — ver atualização em [docs/prd-secao-duas-capitais.md](../docs/prd-secao-duas-capitais.md#11-dependências-e-decisões).

**Pendência remanescente:** nenhuma decisão de negócio pendente. Falta apenas o commit das alterações e, se autorizado, o deploy em produção (ambos fora desta etapa até confirmação explícita).

## Correção do recorte extremo no mobile (21/11/2026, segunda continuação)

**Relato do solicitante:** após a correção de movimento, a imagem de fundo apareceu "gigante, estourando a tela" (print em zoom anexado).

**Diagnóstico (Playwright, viewports 375/390/768/1280/1920):** confirmado com medições reais. No mobile a seção tem ~1517 px de altura para 375 px de largura (proporção ~0,25), enquanto as quatro fotos são paisagem (proporção 0,83–1,78). O `object-fit: cover` cobrindo a seção inteira exigia uma escala de até 1,88×, deixando visível menos de 14% da largura da foto `duas-capitais-poa-noturna.webp` — na prática, uma faixa vertical irreconhecível, agravada pelo zoom do Ken Burns (6.2). Tablet (768 px) e desktop (1280/1920 px) já ficavam legíveis e não apresentavam o problema.

**Correção aplicada em `index.html`:**
- A camada fotográfica (`div` com as 4 `.dc-slide`) passou a usar a classe `.dc-photo-band` em vez de `absolute inset-0`.
- Em telas ≥ 640 px o comportamento não muda (faixa cobre a seção inteira, `inset: 0`).
- Em telas < 640 px a faixa passa a ter **proporção própria 4:5** (não mais a altura inteira da seção) e um degradê inferior para `rgba(4,27,36,…)` (`pool-abyss`, a cor de fundo da seção), para que o restante do texto repouse sobre a cor sólida sem corte abrupto.
- Nenhuma alteração em tablet/desktop, no JS de rotação/Ken Burns ou nos critérios de acessibilidade.

**Validação (Playwright, Chromium):**
- [x] Mobile 375 px: faixa fotográfica com 468,75 px de altura (antes: 1517,5 px/seção inteira); largura visível da foto por imagem entre ~45% e ~95%, a depender da orientação (antes: ~14% no pior caso).
- [x] Mobile 390 px: comportamento equivalente (487,6 px de faixa).
- [x] Tablet 768 px e desktop 1280/1920 px: faixa continua cobrindo a seção inteira, sem diferença visual em relação à validação anterior.
- [x] Sem overflow horizontal em nenhum dos 5 viewports (`docScrollWidth === docClientWidth`).
- [x] Rotação de slides e Ken Burns continuam funcionando no mobile (slide 0 → 1 após ~8–10 s; `transform: scale` evolui de 1,0 para ~1,117 antes da troca).
- [x] `prefers-reduced-motion` no mobile: `dc-animating` ausente, slide permanece em 0.
- [x] Prints antes/depois confirmam a foto legível (skyline reconhecível) no lugar da mancha escura ampliada, com transição suave para a cor sólida no restante da seção.
- [x] Sem erros de console.

**Pendência:** aguardando o solicitante revisar os prints antes do commit desta rodada.

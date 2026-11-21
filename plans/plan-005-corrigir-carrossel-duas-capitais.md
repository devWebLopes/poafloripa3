# Plano 005 — Correção do carrossel Duas Capitais

- **Status:** Implementado e validado em 21/11/2026 (local; sem deploy)
- **Agente líder:** Frontend ([agents/frontend.md](../agents/frontend.md))
- **Apoio:** QA & Deploy
- **Skills:** html-semantico-seo, tailwind-design-system, vanilla-js-modular, qa-validacao-web
- **Escopo:** somente `section#duasCapitais`, sem alterar o texto ou outras seções

## Objetivo

Estabilizar o carrossel fotográfico da seção `#duasCapitais`, contendo imagens e movimento dentro da seção, controlando sua altura no desktop e preservando responsividade, acessibilidade e os quatro controles manuais.

## Implementação

- [x] Fazer o wrapper e os quatro slides ocuparem a seção por posicionamento absoluto, sem participação no fluxo.
- [x] Aplicar `object-fit: cover`, enquadramento central e clipping em todas as camadas.
- [x] Reduzir o zoom para no máximo `scale(1.03)` e o crossfade para 800 ms.
- [x] Manter somente o slide ativo visível e interativo.
- [x] Ajustar o conteúdo para altura visual de 680–800 px no desktop e altura automática em telas menores.
- [x] Manter seleção pelos quatro indicadores, autoplay de 6 s e pausa/reprodução.
- [x] Preservar o modo `prefers-reduced-motion` sem zoom nem autoplay.
- [x] Atualizar a documentação técnica da seção.

## Validação

- [x] Testar em 1280 px, 768 px e 375 px.
- [x] Confirmar ausência de overflow horizontal.
- [x] Confirmar que só um slide está visível por vez e que os quatro indicadores funcionam.
- [x] Confirmar autoplay, pausa/reprodução e transição suave.
- [x] Confirmar enquadramento, clipping e legibilidade nas quatro imagens.
- [x] Confirmar modo de movimento reduzido.
- [x] Verificar console e regressão básica das demais áreas.
- [x] Não realizar deploy em produção.

## Evidências de QA

- Playwright/Chromium: 6 cenários aprovados (layout e controles em 1280/768/375 px, movimento reduzido, autoplay/pausa/retomada e regressão básica).
- Alturas medidas: 811,5 px em 1280; 1231 px em 768; 1517,5 px em 375. Tablet e mobile permanecem automáticos por necessidade do texto.
- `documentElement.scrollWidth === clientWidth` nos três viewports; sem overflow horizontal.
- Quatro slides testados manualmente pelos indicadores; após 800 ms, exatamente um tinha opacidade 1 e os outros três opacidade 0 com `pointer-events: none`.
- Zoom medido durante a animação dentro do limite 1,03; no modo reduzido, `animation: none`, `transform: none` e sem autoplay.
- Inspeção visual das quatro fotos em desktop e da composição em tablet/mobile: clipping correto e texto legível.
- Console sem erros; 6 cards, hero, modal de imóvel e drawer móvel preservados.
- Lighthouse local: Acessibilidade 96, Boas Práticas 100, SEO 100 e CLS 0. Performance 56 por FCP/LCP de 9,3 s no carregamento local com recursos CDN existentes; não houve alteração fora da seção para mascarar essa pendência preexistente.

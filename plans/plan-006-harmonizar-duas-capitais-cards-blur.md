# Plano 006 — Harmonização Editorial, Slideshow Contido e Cards Glassmorphism na Seção Duas Capitais

- **Status:** Implementado e validado em 21/11/2026 (local; sem deploy em produção)
- **Agente líder:** Frontend ([agents/frontend.md](../agents/frontend.md))
- **Apoio:** Arquiteto, QA & Deploy
- **Skills:** html-semantico-seo, tailwind-design-system, vanilla-js-modular, qa-validacao-web
- **Escopo:** `section#duasCapitais` em `index.html`, estilos CSS associados, lógica JS do carrossel e atualização documental (`docs/design-system.md`, `docs/prd-secao-duas-capitais.md`)

## Objetivo

Corrigir definitivamente a troca de slides e o enquadramento horizontal das imagens na seção `#duasCapitais` (“De Porto Alegre a Florianópolis: Duas Capitais, uma História de Qualidade de Vida”), harmonizando imagens e textos no mesmo padrão visual do Hero no início da página, e estruturando os textos em blocos/molduras translúcidas com leve desfoque (`backdrop-blur`), efeito flutuante sutil e efeito de hover elegante.

## Diagnóstico das Causas Raiz

1. **Slides travados na 1ª imagem:**
   - As imagens 2, 3 e 4 tinham `loading="lazy"` dentro de `.dc-slide` com `opacity: 0`, e o JS aguardava `waitForImage()` antes de ativar o slide — causando impasse de carregamento em navegadores Chromium/Edge.
   - A configuração `prefers-reduced-motion: reduce` do sistema operacional (comum no Windows quando animações de janela estão desativadas) bloqueava completamente o timer do carrossel e ocultava `.dc-controls` com `display: none`.
   - O `IntersectionObserver` exigia `threshold: 0.15` para iniciar o ciclo em uma seção alta.
2. **Imagem estourando na horizontal e aparência fixa:**
   - As fotos 2 (`1057×1280`) e 3 (`1072×1181`) são verticais, enquanto a 1 (`1440×808`) e a 4 (`1125×740`) são horizontais. Em uma seção muito alta com `object-fit: cover` puro, ou a foto horizontal sofria zoom vertical exagerado cortando as laterais, ou a foto vertical sofria zoom horizontal exagerado no desktop.
   - O efeito Ken Burns estava restrito a `scale(1.03)` sem deslocamento (`translate3d`), parecendo estático.

## Solução Planejada

1. **Carrossel confiável como o Hero:**
   - Remover `loading="lazy"` das 4 imagens da seção e pré-carregá-las em memória para troca instantânea sem bloqueio.
   - Usar a mesma mecânica de transição suave do Hero (`opacity` + `.motion-canvas` Ken Burns contínuo) com ciclo automático de 6,5 s, pílula seletora flutuante no topo e indicadores/pausa sempre visíveis e funcionais.
   - Em `prefers-reduced-motion: reduce`, apenas suavizar a escala do Ken Burns, sem travar a troca de slides nem esconder os controles.
2. **Enquadramento harmônico sem estourar na horizontal:**
   - Adicionar camada de ambientação desfocada (`dc-backdrop-blur`) + imagem principal com enquadramento calibrado e contido na altura controlada da seção, evitando cortes extremos tanto em fotos paisagem quanto retrato e garantindo zero overflow horizontal.
3. **Textos em blocos/molduras com blur, flutuação e hover:**
   - Organizar os 4 parágrafos originais (preservando 100% do texto literal) em blocos com moldura translúcida (`backdrop-blur-md`, fundo petróleo/vidro leve e borda fina):
     - **Bloco 1 (Introdução):** card glassmorphism em destaque com efeito flutuante e hover.
     - **Bloco 2 (Porto Alegre) e Bloco 3 (Florianópolis):** dois cards lado a lado no desktop com badge da cidade, efeito flutuante alternado (`.dc-float-card` / `.dc-float-card-delayed`), `lag-item` e elevação suave no hover (`.dc-glass-card:hover` com borda `pool` `#00B4D8` e sombra suave).
     - **Bloco 4 (Fechamento):** moldura editorial com destaque lateral azul piscina (`border-l-2 border-pool`), blur e hover elegante.

## Checklist de Validação (QA)

- [x] Texto original (título, eyebrow e 4 parágrafos) 100% preservado sem alterações.
- [x] Os 4 slides alternam automaticamente e manualmente pelos indicadores e botões.
- [x] Movimento Ken Burns suave como no Hero e sem estouro horizontal (`scrollWidth === clientWidth`).
- [x] Textos em molduras com leve blur (`backdrop-filter: blur`), efeitos flutuantes e hover responsivo.
- [x] Sem novas dependências e sem deploy em produção.

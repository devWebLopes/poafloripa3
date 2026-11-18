# Levantamento estruturado das alterações do site — Poa Floripa Imóveis

## 1. Identificação do levantamento

- **Data das solicitações:** 13/11/2026
- **Solicitante:** Tiago Rosin
- **Destinatário:** Evandro
- **Origem:** conversa de WhatsApp, imagens e áudios enviados na mesma data
- **Objetivo deste documento:** registrar, organizar e detalhar o que foi solicitado para que um agente de IA com acesso ao projeto do site possa, posteriormente, elaborar um PRD de implementação.
- **Natureza do documento:** levantamento de requisitos de origem; **não é ainda o PRD final**.

## 2. Fontes analisadas

### 2.1 Fonte principal

- [`Conversa do WhatsApp com Tiago Rosin.txt`](./Conversa%20do%20WhatsApp%20com%20Tiago%20Rosin.txt), especialmente as mensagens de **13/11/2026, entre 19:27 e 22:33**.

### 2.2 Áudios relacionados

- [`PTT-20261113-WA0043.opus`](./PTT-20261113-WA0043.opus) — orientação sobre manter o telefone atual e enviar outras pequenas alterações posteriormente.
- [`PTT-20261113-WA0054.opus`](./PTT-20261113-WA0054.opus) — explicação do formato imaginado para a nova seção sobre Porto Alegre e Florianópolis.
- Transcrição automática de apoio: [`transcricao-audios-2026-11-13.txt`](./transcricao-audios-2026-11-13.txt).

> A transcrição automática contém pequenas imprecisões de reconhecimento. Para os requisitos abaixo, ela foi interpretada junto com a sequência das mensagens, as legendas escritas e as imagens enviadas.

### 2.3 Referência local do site

O arquivo [`poafloripa6.html`](./poafloripa6.html) foi consultado apenas para identificar os textos e componentes atualmente existentes que correspondem às capturas de tela. O agente responsável pelo PRD deve confirmar qual arquivo, branch ou versão representa o site efetivamente vigente.

---

## 3. Resumo executivo das alterações solicitadas

1. Substituir/ajustar a logomarca e centralizar a palavra **“IMÓVEIS”**.
2. Remover da barra de navegação azul o item **“Explorar Imóveis de Luxo”**.
3. Clarear o azul do site, adotando um **azul piscina** próximo ao da referência enviada.
4. Acrescentar quatro tipos no filtro **“Todas as categorias”**: casas, terrenos, sala comercial e lojas.
5. Alterar a chamada de contato para mencionar **Rio Grande do Sul ou Santa Catarina** e remover o botão **“Explorar Acervo Completo”** dessa chamada.
6. Atualizar o título e o subtítulo de abertura para incluir imóveis de **médio e alto padrão** e a expressão **“Curadoria imobiliária”**.
7. Transformar a seção **“Quem é Poa Floripa Imóveis”** em **“Sobre Nós”**, substituir o conteúdo e remover o bloco de três tópicos.
8. Criar, como última seção de conteúdo do site, uma seção sobre a conexão histórica e a qualidade de vida em Porto Alegre e Florianópolis, com texto e galeria de imagens.
9. Manter, por enquanto, o número de telefone que já está no site.

---

## 4. Requisitos detalhados

## ALT-01 — Atualizar a logomarca

### Solicitação de origem

- Às **19:27**, Tiago informou: **“1- logomarca”** e enviou a imagem de referência.
- Às **19:29**, complementou: **“O imóveis teria que centralizar”**.
- Às **19:35**, enviou um link do Gemini e informou que aquele seria o original da logomarca feita por IA, com a orientação **“utilizar esse”**.

### Alteração esperada

- Utilizar a nova identidade visual/logomarca indicada por Tiago.
- A composição visual deve conter:
  - “POA”;
  - ícone de casa vermelho entre as duas palavras;
  - “FLORIPA”;
  - “IMÓVEIS” em uma segunda linha.
- A palavra **“IMÓVEIS” deve ficar visualmente centralizada** em relação ao conjunto principal da marca, e não deslocada para um dos lados.

### Referências

- Imagem enviada: [`IMG-20261113-WA0039.jpg`](./IMG-20261113-WA0039.jpg) — fotografia da aplicação da marca, resolução 1088 × 485.
- Original indicado por Tiago: <https://gemini.google.com/share/ae11da612339>

![Referência da logomarca](./IMG-20261113-WA0039.jpg)

### Critérios de aceitação sugeridos para o futuro PRD

- A marca usada no site corresponde ao arquivo/original aprovado por Tiago.
- “IMÓVEIS” está centralizado sob o conjunto superior.
- A marca permanece legível em desktop e celular.
- A proporção da marca não é deformada.
- Existe texto alternativo adequado, por exemplo, **“Poa Floripa Imóveis”**.
- O resultado funciona sobre o fundo da barra sem perda de contraste.

### Pendência antes da implementação

- A imagem `WA0039` é uma fotografia e não um arquivo de marca adequado para produção. O link compartilhado do Gemini exige autenticação no ambiente consultado. É necessário obter o arquivo original em boa resolução, preferencialmente **SVG** ou **PNG com transparência**, e confirmar que essa é a versão final aprovada.

---

## ALT-02 — Remover “Explorar Imóveis de Luxo” da barra azul

### Solicitação de origem

- Às **19:31**, Tiago solicitou: **“excluir na barra azul o item explorar imóveis de luxo”**.

### Alteração esperada

- Remover da navegação principal, localizada na barra azul do topo, o item textual **“Explorar Imóveis de Luxo”**.
- Reorganizar o espaçamento dos itens restantes para não deixar uma lacuna visual.

### Referência

- [`IMG-20261113-WA0040.jpg`](./IMG-20261113-WA0040.jpg) — o item aparece entre “Página inicial” e “Imóveis Selecionados”.

![Item de navegação a remover](./IMG-20261113-WA0040.jpg)

### Limite da solicitação

- A mensagem menciona especificamente o item **da barra azul**. Ela não determina, por si só, que todo o catálogo, drawer ou outras formas de acessar os imóveis devam ser removidos.

### Critérios de aceitação sugeridos

- O texto não aparece mais na navegação principal em desktop.
- O menu responsivo/mobile não mantém inadvertidamente o mesmo item, caso represente a mesma navegação.
- Os demais itens continuam alinhados e funcionais.
- A remoção não deixa chamadas JavaScript inacessíveis, elementos vazios ou erros no console.

### Ponto a confirmar no PRD

- Confirmar se a remoção vale apenas para a barra de desktop ou também para qualquer item equivalente no menu mobile.

---

## ALT-03 — Clarear a cor azul para um “azul piscina”

### Solicitação de origem

- Às **19:32**, Tiago solicitou: **“deixar o azul um tom mais claro (azul piscina), tipo esse”**.

### Alteração esperada

- Substituir o azul atual por um tom mais claro, com aparência de **azul piscina**, usando a imagem enviada como referência visual.
- Preservar legibilidade e contraste dos textos, ícones, botões, bordas e estados interativos aplicados sobre essa cor.

### Referência

- [`IMG-20261113-WA0042.jpg`](./IMG-20261113-WA0042.jpg) — carro azul usado como referência cromática.

![Referência de azul piscina](./IMG-20261113-WA0042.jpg)

### Observação cromática

- A imagem não define um código oficial. Uma amostragem aproximada da carroceria produziu valores na faixa de **`#03B1DF` a `#10A2D0`**, mas esses valores são apenas ponto de partida e **não constituem aprovação de cor**.
- O futuro PRD deve transformar a cor aprovada em token reutilizável do design system, evitando substituições isoladas e inconsistentes.

### Critérios de aceitação sugeridos

- O azul principal é perceptivelmente mais claro e próximo à referência.
- Texto branco sobre o novo azul atende ao contraste mínimo aplicável.
- Estados hover, focus, bordas e fundos derivados continuam distinguíveis.
- A aplicação é consistente nos componentes que fazem parte do escopo aprovado.

### Ponto a confirmar no PRD

- Tiago não especificou se o novo tom deve ser aplicado somente à barra superior ou a **todos os elementos azuis da identidade do site**. Confirmar o alcance antes de estimar a implementação.

---

## ALT-04 — Acrescentar categorias de imóveis ao filtro

### Solicitação de origem

- Às **19:38**, Tiago solicitou: **“no item Todas as categorias acrescentar: casas, terrenos, sala comercial, lojas.”**

### Estado atual identificado

O filtro exibido na referência possui:

- Todas as categorias;
- Sobrados;
- Coberturas;
- Apartamentos;
- Casas em Condomínio.

### Alteração esperada

Preservar as opções existentes e acrescentar:

1. **Casas**;
2. **Terrenos**;
3. **Sala comercial**;
4. **Lojas**.

### Referência

- [`IMG-20261113-WA0044.jpg`](./IMG-20261113-WA0044.jpg)

![Filtro Todas as categorias](./IMG-20261113-WA0044.jpg)

### Requisitos funcionais derivados

- Cada nova opção deve ter um valor interno estável e compatível com o modelo de dados dos imóveis.
- Selecionar uma opção deve filtrar corretamente os imóveis correspondentes.
- O filtro deve continuar funcionando em conjunto com localização, ordenação e demais filtros.
- O estado “Todas as categorias” deve continuar removendo a restrição por tipo.
- Se ainda não houver imóveis de uma categoria, definir no PRD se o resultado será uma lista vazia com mensagem apropriada ou se a opção ficará temporariamente oculta.

### Critérios de aceitação sugeridos

- As quatro novas opções aparecem no seletor em desktop e mobile.
- Não há duplicidade entre **“Casas”** e **“Casas em Condomínio”**.
- Os rótulos, valores internos, dados e lógica de filtragem usam a mesma taxonomia.

### Pontos a confirmar no PRD

- Ordem final das categorias.
- Padronização singular/plural, especialmente **“Sala comercial”** versus **“Salas comerciais”**.
- Existência das novas categorias no backend, CMS, API ou base de imóveis.

---

## ALT-05 — Alterar a chamada de contato e remover um CTA

### Solicitação de origem

- Às **19:58**, Tiago pediu para excluir, dessa seção, o item **“Explorar Acervo Completo”**.
- Às **20:09**, pediu para substituir a referência a **“Porto Alegre ou Florianópolis”** por **“no Rio Grande do Sul ou Santa Catarina”**.

### Texto atual identificado

> Quer encontrar seu próximo imóvel em Porto Alegre ou Florianópolis?

### Texto final solicitado

> **Quer encontrar seu próximo imóvel no Rio Grande do Sul ou Santa Catarina?**

### Alterações de interface

- Manter o CTA **“Falar com Especialista”**.
- Remover o CTA **“Explorar Acervo Completo”** apenas dessa faixa/seção.
- Reequilibrar o alinhamento da seção para um único botão.

### Referência

- [`IMG-20261113-WA0045.jpg`](./IMG-20261113-WA0045.jpg)

![Chamada e CTA a alterar](./IMG-20261113-WA0045.jpg)

### Critérios de aceitação sugeridos

- O título usa exatamente o novo recorte geográfico.
- “Explorar Acervo Completo” não aparece mais nessa seção.
- “Falar com Especialista” continua acionando corretamente o contato/modal previsto.
- A seção permanece visualmente equilibrada em diferentes larguras de tela.

---

## ALT-06 — Atualizar título e subtítulo da abertura

### Solicitação de origem

- Às **20:17**, Tiago pediu para acrescentar **“médio”** à frase inicial de abertura.
- Às **20:20**, pediu para acrescentar a palavra **“imobiliária”** à frase de curadoria e forneceu a redação desejada.

### Título final solicitado

> **Imóveis de Médio e Alto Padrão em Porto Alegre e Florianópolis**

### Subtítulo final solicitado

> **Curadoria imobiliária para quem busca sofisticação, localização privilegiada e qualidade de vida**

### Observação editorial

- A redação fornecida por Tiago usa **“Curadoria imobiliária”**, substituindo na prática a expressão atual **“Curadoria exclusiva”**.
- O agente não deve manter “exclusiva” por conta própria, a menos que isso seja confirmado no PRD.

### Critérios de aceitação sugeridos

- O título visível contém “Médio e Alto Padrão”.
- O subtítulo visível começa com “Curadoria imobiliária”.
- A quebra de linha continua adequada em desktop e mobile.
- Não ocorre sobreposição com imagens, seletor de cidades ou caixa de busca.

### Consideração para o futuro PRD

- Verificar se `<title>`, meta description, Open Graph e outros textos de SEO repetem a redação antiga. Atualizá-los pode ser necessário por consistência, mas isso não foi solicitado explicitamente por Tiago e deve constar separadamente no PRD.

---

## ALT-07 — Substituir “Quem é Poa Floripa” por “Sobre Nós”

### Solicitação de origem

- Às **20:49**, Tiago solicitou: **“No item do ‘quem é Poa Floripa’ alterar para ‘Sobre nós’”**.
- Às **21:04–21:05**, enviou o novo texto.
- Às **21:06**, pediu para retirar a parte exibida na captura enviada às **21:07**.

### Novo título da seção

> **Sobre Nós**

### Novo texto fornecido por Tiago

> A Poa Floripa Imóveis é uma assessoria especializada em imóveis de médio e alto padrão, com atuação focada em Porto Alegre, Florianópolis e abrangência em todo o Rio Grande do Sul e Santa Catarina. Nosso trabalho vai além da intermediação tradicional: unimos uma curadoria rigorosa das melhores oportunidades do mercado à total transparência e ao respaldo de uma assessoria jurídica de confiança em cada etapa. Oferecemos um atendimento personalizado, desenhado para entender o estilo de vida e os objetivos de investimento de cada cliente, garantindo tranquilidade, segurança patrimonial e exclusividade do primeiro contato à entrega das chaves.

### Conteúdo a remover

A captura indica a remoção completa do bloco de três tópicos atualmente exibido:

1. “Atendimento 100% consultivo em Porto Alegre e Florianópolis”;
2. “Foco em imóveis selecionados com apresentação fotográfica detalhada”;
3. “Experiência comprovada no mercado de médio e alto padrão”.

### Referência

- [`IMG-20261113-WA0051.jpg`](./IMG-20261113-WA0051.jpg)

![Bloco de tópicos a remover](./IMG-20261113-WA0051.jpg)

### Critérios de aceitação sugeridos

- O título anterior não aparece mais como título dessa seção.
- O novo texto é exibido integralmente, sem misturar parágrafos antigos.
- O bloco de três tópicos foi removido.
- O espaço deixado pelo bloco removido é reequilibrado no layout.
- A seção continua legível e bem distribuída em telas menores.

### Pontos a confirmar no PRD

- Confirmar se o item **“Curadoria”** do menu superior também deve ser renomeado para **“Sobre Nós”**. A solicitação cita o item/seção “Quem é Poa Floripa”, mas não menciona explicitamente o rótulo atual do menu.
- Validar institucionalmente as afirmações **“assessoria jurídica de confiança”**, **“segurança patrimonial”** e **“exclusividade”** antes da publicação.

---

## ALT-08 — Criar seção final sobre Porto Alegre e Florianópolis

### Solicitação de origem

- Às **22:05**, Tiago pediu a criação de mais um item, definido como **“o último item do site”**, sobre a história das duas capitais.
- Às **22:06**, enviou o título e quatro parágrafos.
- Às **22:07**, informou que pensou em acrescentar fotos das duas cidades.
- No áudio `WA0054`, explicou que prefere abordar a **conexão entre as duas cidades**, em vez de contar cada história separadamente.

### Posicionamento esperado

- Criar uma nova seção como **última seção de conteúdo do site**, antes do rodapé e de elementos puramente globais.

### Título fornecido

> **De Porto Alegre a Florianópolis: Duas Capitais, uma História de Qualidade de Vida**

### Texto integral fornecido por Tiago

> A conexão entre Porto Alegre e Florianópolis vai muito além da proximidade geográfica — ela está escrita na própria origem das duas cidades. Ambas foram moldadas pelo espírito pioneiro e acolhedor dos colonizadores açorianos no século XVIII, que encontraram nas águas do Lago Guaíba e nas baías da Ilha de Santa Catarina o cenário perfeito para construir comunidades prósperas, vibrantes e intimamente ligadas à natureza.
>
> Com o passar dos séculos, cada capital desenvolveu sua própria vocação, criando uma complementaridade única no Sul do Brasil. Porto Alegre, fundada oficialmente em 1772 como o histórico Porto dos Casais, consolidou-se como uma metrópole dinâmica, referência em negócios, cultura, gastronomia e infraestrutura urbana. Seus bairros tradicionais, parques arborizados e a renovada Orla do Guaíba oferecem o equilíbrio ideal entre o ritmo cosmopolita e o bem-estar.
>
> Florianópolis, por sua vez, transformou sua herança açoriana em um dos destinos mais desejados do país para viver e investir. Conhecida como a Ilha da Magia, une praias paradisíacas, segurança e alto índice de desenvolvimento humano a um polo tecnológico e de inovação em constante expansão, atraindo famílias e investidores em busca de qualidade de vida junto ao mar.
>
> Hoje, o fluxo entre gaúchos e catarinenses é mais forte do que nunca — seja para morar, veranear ou diversificar investimentos imobiliários. Na Poa Floripa Imóveis, conhecemos profundamente a essência e as oportunidades desses dois mercados. Conectamos você às melhores opções de imóveis nas duas capitais para que você possa viver ou investir exatamente onde a sua história pedir.

### Direção de conteúdo e experiência descrita no áudio

- A seção deve apresentar a **conexão entre as capitais**, não duas histórias isoladas.
- Tiago cogitou duas formas e deixou a decisão de layout em aberto:
  1. mostrar o texto diretamente na página junto das imagens; ou
  2. mostrar inicialmente título e fotos, permitindo clicar para revelar/abrir o texto completo.
- Ele imaginou aproximadamente:
  - **3 a 4 fotos de Porto Alegre**;
  - aproximadamente **3 fotos de Florianópolis/praias**;
  - como requisito mínimo verbalizado, **pelo menos 2 fotos de Florianópolis**.
- O layout pode distribuir o texto para evitar que pareça excessivamente longo.

### Imagens enviadas para esta seção

| Arquivo | Identificação dada na conversa | Cidade/região | Observação |
|---|---|---|---|
| [`IMG-20261113-WA0052.jpg`](./IMG-20261113-WA0052.jpg) | Viaduto Otávio Rocha | Porto Alegre | Referência urbana/histórica. |
| [`IMG-20261113-WA0053.jpg`](./IMG-20261113-WA0053.jpg) | Ilha do Campeche | Florianópolis | Praia e embarcações; arquivo contém marca visual do Google Lens no canto. |
| [`IMG-20261113-WA0055.jpg`](./IMG-20261113-WA0055.jpg) | Trapiche de Jurerê Internacional | Florianópolis | A legenda de origem identifica o local; validar se a imagem escolhida representa claramente o trapiche. |
| [`IMG-20261113-WA0060.jpg`](./IMG-20261113-WA0060.jpg) | Parque Farroupilha (Redenção) | Porto Alegre | Arquivo contém marca visual do Google Lens no canto. |

#### Viaduto Otávio Rocha

![Viaduto Otávio Rocha](./IMG-20261113-WA0052.jpg)

#### Ilha do Campeche

![Ilha do Campeche](./IMG-20261113-WA0053.jpg)

#### Trapiche de Jurerê Internacional

![Referência indicada como Trapiche de Jurerê Internacional](./IMG-20261113-WA0055.jpg)

#### Parque Farroupilha (Redenção)

![Parque Farroupilha - Redenção](./IMG-20261113-WA0060.jpg)

### Requisitos de implementação a considerar no PRD

- Definir uma composição editorial responsiva para texto e galeria.
- Se houver abertura do texto por clique:
  - o controle deve ser acessível por teclado;
  - deve indicar estado aberto/fechado;
  - o conteúdo não pode ficar inacessível a leitores de tela ou mecanismos de busca.
- Criar textos alternativos descritivos para as imagens.
- Otimizar as imagens para web, com dimensões responsivas e carregamento que não prejudique a performance.
- Não publicar imagens com ícone do Google Lens ou outras marcas de interface.
- Confirmar autoria e licença de uso. Se não houver autorização, substituir por imagens próprias ou licenciadas dos mesmos locais.
- Verificar os fatos históricos e afirmações sobre segurança, IDH e mercado antes da publicação.

### Critérios de aceitação sugeridos

- A seção aparece no final do conteúdo principal.
- O título e os quatro parágrafos aprovados estão presentes.
- Há imagens representando as duas cidades, respeitando ao menos o mínimo mencionado para Florianópolis.
- As imagens possuem identificação correta, boa resolução, licença adequada e não exibem marcas de ferramenta de busca.
- O conteúdo é legível e não forma um bloco excessivamente denso no celular.
- Eventual interação para revelar o texto é acessível e funcional sem erros.

### Pontos a decidir no PRD

- Texto sempre visível ou aberto sob demanda.
- Quantidade final de imagens e formato da galeria.
- Necessidade de novas imagens além das quatro enviadas.
- Localização exata em relação às seções de contato, newsletter e rodapé.
- Inclusão ou não de um item no menu que leve diretamente a essa nova seção.

---

## ALT-09 — Manter temporariamente o telefone atual

### Solicitação de origem

No áudio enviado às **19:36**, Tiago explicou que ainda não conseguiu comprar o chip de telefone e que esperaria mais um pouco. Por isso, orientou que **o número permanecesse o mesmo por enquanto**.

### Alteração esperada

- Não substituir o telefone atualmente publicado até que Tiago envie o novo número.
- Não tratar essa permanência como aprovação definitiva do número; trata-se de uma decisão temporária.

### Critérios de aceitação sugeridos

- O número visível e o destino do link de WhatsApp continuam correspondendo ao telefone atual.
- Não há divergência entre o número exibido e o número configurado no link.

### Observação

- No protótipo local consultado, o telefone aparece como **(48) 99999-0240**, mas o agente deve conferir o valor da versão real do site antes de criar o PRD ou implementar qualquer alteração.

---

## 5. Conteúdos finais consolidados

Esta seção reúne os textos fornecidos por Tiago para reduzir ambiguidades durante a criação do PRD.

### 5.1 Abertura

**Título:**

> Imóveis de Médio e Alto Padrão em Porto Alegre e Florianópolis

**Subtítulo:**

> Curadoria imobiliária para quem busca sofisticação, localização privilegiada e qualidade de vida

### 5.2 Chamada de contato

**Título:**

> Quer encontrar seu próximo imóvel no Rio Grande do Sul ou Santa Catarina?

**CTA que permanece:**

> Falar com Especialista

**CTA a remover dessa seção:**

> Explorar Acervo Completo

### 5.3 Sobre Nós

**Título:**

> Sobre Nós

**Corpo:**

> A Poa Floripa Imóveis é uma assessoria especializada em imóveis de médio e alto padrão, com atuação focada em Porto Alegre, Florianópolis e abrangência em todo o Rio Grande do Sul e Santa Catarina. Nosso trabalho vai além da intermediação tradicional: unimos uma curadoria rigorosa das melhores oportunidades do mercado à total transparência e ao respaldo de uma assessoria jurídica de confiança em cada etapa. Oferecemos um atendimento personalizado, desenhado para entender o estilo de vida e os objetivos de investimento de cada cliente, garantindo tranquilidade, segurança patrimonial e exclusividade do primeiro contato à entrega das chaves.

### 5.4 Seção histórica

Usar o título e os quatro parágrafos registrados integralmente em **ALT-08**.

---

## 6. Inventário dos anexos de 13/11/2026

### 6.1 Anexos diretamente relacionados aos requisitos

| Arquivo | Uso no levantamento |
|---|---|
| `IMG-20261113-WA0039.jpg` | Referência da logomarca. |
| `IMG-20261113-WA0040.jpg` | Item de navegação “Explorar Imóveis de Luxo”. |
| `IMG-20261113-WA0042.jpg` | Referência do azul piscina. |
| `PTT-20261113-WA0043.opus` | Manutenção temporária do telefone atual. |
| `IMG-20261113-WA0044.jpg` | Filtro “Todas as categorias”. |
| `IMG-20261113-WA0045.jpg` | Chamada de contato e CTAs. |
| `IMG-20261113-WA0051.jpg` | Bloco de três tópicos a remover de “Sobre Nós”. |
| `IMG-20261113-WA0052.jpg` | Viaduto Otávio Rocha. |
| `IMG-20261113-WA0053.jpg` | Ilha do Campeche. |
| `PTT-20261113-WA0054.opus` | Explicação de layout/conteúdo da nova seção. |
| `IMG-20261113-WA0055.jpg` | Referência indicada como Trapiche de Jurerê Internacional. |
| `IMG-20261113-WA0060.jpg` | Parque Farroupilha (Redenção). |

### 6.2 Anexos aparentemente casuais, sem requisito claro para o site

Os arquivos abaixo foram trocados durante a continuação da conversa, mas não receberam legenda ou instrução que os vincule ao site:

| Arquivo | Conteúdo observado | Tratamento recomendado |
|---|---|---|
| `IMG-20261113-WA0057.jpg` | Pessoa andando de skate, fotografada de cima. | Não incluir no PRD como ativo do site sem nova confirmação. |
| `IMG-20261113-WA0059.jpg` | Caminho gramado/muro à noite. | Não incluir no PRD como ativo do site sem nova confirmação. |
| `IMG-20261113-WA0061.jpg` | Ave pousada em uma árvore à noite. | Não incluir no PRD como ativo do site sem nova confirmação. |

---

## 7. Dependências e questões abertas para a criação do PRD

O agente que elaborar o PRD deve resolver ou registrar explicitamente os seguintes pontos:

1. **Arquivo final da marca:** obter o original aprovado em formato apropriado para web.
2. **Escopo da nova cor:** barra superior apenas ou identidade azul completa.
3. **Código da cor:** definir e aprovar o valor final; a amostragem deste documento não é aprovação.
4. **Menu responsivo:** confirmar se “Explorar Imóveis de Luxo” também sai do menu mobile.
5. **Acesso ao catálogo:** definir se outras entradas para o catálogo/drawer continuam disponíveis.
6. **Taxonomia:** mapear as quatro novas categorias para backend/CMS/API e dados existentes.
7. **Menu “Sobre Nós”:** decidir se o rótulo “Curadoria” do menu também será alterado.
8. **Formato da seção histórica:** texto sempre aberto ou revelado por interação.
9. **Galeria:** confirmar quantidade, proporções e imagens finais de cada cidade.
10. **Direitos de imagem:** obter licença ou substituir arquivos sem origem comprovada.
11. **Validação factual e jurídica:** revisar texto histórico e alegações institucionais.
12. **Telefone:** confirmar o número que está publicado na versão real e mantê-lo até nova orientação.
13. **Consistência geográfica:** não expandir automaticamente todos os textos de “Porto Alegre e Florianópolis” para “Rio Grande do Sul e Santa Catarina”; alterar apenas o que foi solicitado ou o que for aprovado no PRD.

---

## 8. Fora do escopo deste levantamento

- Não foi solicitado redesenho completo do site.
- Não foi solicitada remoção geral do catálogo de imóveis.
- Não foi solicitado novo número de telefone.
- Não foi definida uma cor hexadecimal final.
- Não foi aprovado um formato definitivo para a galeria/seção histórica.
- Não foram fornecidas comprovações de licença das imagens.
- Pequenas alterações futuras mencionadas no primeiro áudio não fazem parte deste escopo enquanto não forem enviadas e descritas.

---

## 9. Orientação para o agente que criará o PRD

Ao transformar este levantamento em PRD:

1. Inspecione a versão vigente do site e mapeie cada requisito aos componentes, dados e rotas reais.
2. Preserve a distinção entre **pedido confirmado**, **interpretação de implementação** e **questão pendente**.
3. Não amplie o escopo com alterações editoriais ou visuais não aprovadas.
4. Inclua critérios de aceitação responsivos, acessibilidade, SEO técnico quando afetado, testes funcionais dos filtros e verificação de links/CTAs.
5. Inclua no plano a otimização e regularização dos ativos visuais.
6. Apresente decisões pendentes a Tiago antes de transformar suposições em requisitos definitivos.

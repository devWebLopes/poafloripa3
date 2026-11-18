# PRD — Evolução do site de demonstração para produção

- **Produto:** Poa Floripa Imóveis
- **Versão:** 0.1
- **Status:** Proposta para validação
- **Escopo:** catálogo de imóveis exclusivamente para venda em Porto Alegre e Florianópolis
- **Plano relacionado:** [Plano 002](../plans/plan-002-prd-evolucao-producao.md)

## 1. Resumo executivo

O site atual valida a identidade visual e a navegação, mas ainda não possui os componentes operacionais necessários para produção. Os imóveis, textos e imagens estão dentro de um único `index.html`; as fotos estão em base64; o detalhe abre somente em modal; e os formulários apenas simulam o envio.

A evolução recomendada é:

1. manter a Vercel como plataforma do site público;
2. adotar um **CMS gerenciado com biblioteca de mídia** para que a equipe cadastre imóveis e envie fotos sem editar código;
3. guardar fotos originais no storage/CDN do CMS, nunca em base64 ou no repositório;
4. criar uma URL pública e indexável para cada imóvel;
5. usar publicação por rascunho, revisão e aprovação;
6. integrar formulários a um destino real, com proteção antispam e requisitos de LGPD.

**Opção técnica recomendada para o MVP:** frontend em Next.js na Vercel e catálogo/mídia no Sanity. Essa opção reduz o tempo para disponibilizar um painel editorial confiável. Uma solução com Supabase e painel próprio oferece mais controle, mas exige construir e manter upload, formulários, permissões, revisão e biblioteca de mídia.

> A escolha de novas tecnologias e dependências precisa ser aprovada antes da implementação, conforme as regras do repositório.

## 2. Diagnóstico do repositório

### 2.1 Estado atual

| Área | Situação encontrada | Impacto em produção |
|---|---|---|
| Frontend | SPA em um único `index.html`, com HTML, CSS, dados e JavaScript | Alto acoplamento e manutenção arriscada |
| Catálogo | `PROPERTIES` está fixo no JavaScript | Novo imóvel exige alteração de código e novo deploy |
| Fotos | Imagens JPEG em base64 no HTML | Arquivo de aproximadamente 1 MB, sem pipeline de mídia e sem upload operacional |
| Página de imóvel | Detalhes exibidos em modal | Não há URL compartilhável/indexável por imóvel |
| Busca | Filtros e busca executados no navegador | Adequado para poucos imóveis, sem paginação ou consulta persistente |
| Formulários | Visita e newsletter só exibem mensagem de sucesso | Leads podem ser perdidos; não há entrega, histórico nem consentimento registrado |
| SEO | Uma página para todo o catálogo | Cada imóvel não possui metadados, sitemap e conteúdo indexável próprios |
| Administração | Inexistente | Usuário precisa editar JavaScript para alimentar o site |
| Segurança | Sem área autenticada ou API | Ainda não há controle de acesso, auditoria ou proteção de endpoints |
| Deploy | Vercel estática, sem processo de preview editorial | Publicação depende do repositório |

### 2.2 Dados atualmente exibidos

O modelo atual já contém código, finalidade, tipo, cidade, UF, bairro, título, preço, condomínio, IPTU, áreas total e privativa, dormitórios, suítes, vagas, imagem principal, cinco fotos com legendas, descrição em parágrafos e características. Esses campos formam o núcleo do novo modelo editorial, mas valores financeiros, endereço, status e SEO precisam ser normalizados.

### 2.3 Problemas que o produto deve resolver

- Cadastrar, revisar, publicar, atualizar e retirar imóveis sem editar código.
- Enviar várias fotos com progresso, reordená-las e escolher a capa.
- Preencher todos os textos da página de imóvel em um formulário organizado.
- Evitar fotos pesadas, duplicadas, sem legenda ou com proporção inadequada.
- Manter uma única fonte de verdade para o catálogo.
- Garantir que alterações só apareçam publicamente após aprovação.
- Gerar páginas rápidas, compartilháveis e encontráveis em buscadores.
- Entregar e registrar solicitações reais de contato com segurança.

## 3. Objetivos e indicadores

### 3.1 Objetivos do MVP

1. Permitir que um editor publique um imóvel completo sem apoio de desenvolvedor.
2. Centralizar dados e fotos em um CMS autenticado.
3. Criar catálogo e página individual de cada imóvel a partir da mesma fonte de dados.
4. Automatizar tratamento e entrega responsiva das imagens.
5. Colocar no ar um fluxo real de contato e visita.
6. Preservar a marca, os efeitos visuais e a regra de somente venda.

### 3.2 Indicadores de sucesso

| Indicador | Meta do MVP |
|---|---|
| Cadastro operacional | 100% dos campos e fotos preenchidos sem alterar código |
| Tempo editorial | Imóvel pronto publicado em até 10 minutos, sem contar produção de texto/fotos |
| Integridade | Nenhum imóvel publicado sem os campos obrigatórios e o mínimo de 5 fotos |
| Atualização pública | Conteúdo publicado disponível no site em até 5 minutos |
| Performance | Lighthouse ≥ 90 e Core Web Vitals dentro da faixa “boa” no percentil 75 |
| Conversão | Todo formulário válido gera confirmação e chega ao destino definido |
| Rastreabilidade | Publicações e alterações identificam autor e data |

## 4. Usuários e papéis

| Papel | Necessidade | Permissões propostas |
|---|---|---|
| Administrador | Configurar usuários, integrações e regras | Acesso total |
| Editor | Cadastrar dados, textos e fotos | Criar e editar rascunhos; enviar para revisão |
| Revisor/Publicador | Conferir conteúdo antes de expor ao público | Aprovar, publicar, despublicar e arquivar |
| Visitante | Pesquisar e avaliar imóveis | Consultar catálogo, compartilhar e entrar em contato |

No MVP, uma pessoa pode acumular os papéis de administrador e publicador. Contas devem ser individuais; não usar login compartilhado.

## 5. Escopo funcional

### 5.1 Gestão do catálogo

- **RF-CAT-01:** listar imóveis no painel por status, cidade, bairro, tipo e código.
- **RF-CAT-02:** criar imóvel como rascunho e salvar parcialmente.
- **RF-CAT-03:** impedir código duplicado e gerar `slug` único a partir do código e título.
- **RF-CAT-04:** validar campos obrigatórios antes de enviar para revisão ou publicar.
- **RF-CAT-05:** duplicar um imóvel como novo rascunho sem reutilizar código.
- **RF-CAT-06:** visualizar um preview privado idêntico à página pública.
- **RF-CAT-07:** publicar, despublicar, marcar como vendido/indisponível e arquivar.
- **RF-CAT-08:** registrar autor e datas de criação, alteração e publicação.
- **RF-CAT-09:** permitir destaque editorial e ordenação sem usar `createdOrder` manual.
- **RF-CAT-10:** manter a finalidade fixa em venda no MVP.

### 5.2 Gestão de fotos

- **RF-MID-01:** upload múltiplo por arrastar e soltar ou seletor de arquivos.
- **RF-MID-02:** mostrar progresso individual, sucesso e motivo de falha por arquivo.
- **RF-MID-03:** aceitar JPG, PNG e WebP; suporte a HEIC fica condicionado à validação do fornecedor escolhido.
- **RF-MID-04:** validar tamanho, dimensões mínimas e tipo antes da publicação; limites finais serão configuráveis.
- **RF-MID-05:** permitir reordenar fotos por arrastar e soltar.
- **RF-MID-06:** definir exatamente uma foto de capa.
- **RF-MID-07:** exigir texto alternativo e permitir legenda em cada foto.
- **RF-MID-08:** permitir indicar o ambiente da foto, como fachada, living, cozinha, dormitório e área externa.
- **RF-MID-09:** gerar automaticamente variações otimizadas para card, mosaico e tela ampliada.
- **RF-MID-10:** preservar o arquivo original para novo processamento, sem entregá-lo diretamente ao visitante.
- **RF-MID-11:** impedir exclusão definitiva de uma imagem usada por imóvel publicado; primeiro remover a referência e publicar a alteração.
- **RF-MID-12:** alertar sobre arquivo potencialmente duplicado.

### 5.3 Edição dos textos da página do imóvel

O painel deve apresentar um formulário dividido em etapas curtas:

1. identificação e status;
2. localização;
3. valores e áreas;
4. dormitórios e vagas;
5. título, resumo e descrição;
6. características;
7. fotos;
8. SEO e preview;
9. revisão e publicação.

Requisitos:

- contador e orientação de tamanho para título, resumo e metadescrição;
- descrição com parágrafos, subtítulos e listas, sem permitir HTML arbitrário;
- características como lista repetível e reordenável;
- autosave e aviso de alterações não salvas;
- mensagens de erro junto ao campo e resumo dos erros;
- preview desktop e mobile antes da publicação;
- todos os textos públicos editáveis no CMS, sem duplicação no código.

### 5.4 Site público

- **RF-WEB-01:** catálogo alimentado pelo CMS, com filtros atuais preservados.
- **RF-WEB-02:** página individual em `/imoveis/{slug}` com URL permanente.
- **RF-WEB-03:** cards e página individual usam a mesma entidade e a mesma foto de capa.
- **RF-WEB-04:** galeria suporta mais de cinco fotos; o mosaico inicial mantém cinco e oferece “ver todas”.
- **RF-WEB-05:** páginas indisponíveis não aparecem no catálogo e apresentam tratamento definido quando acessadas por URL antiga.
- **RF-WEB-06:** WhatsApp recebe código e título do imóvel e é direcionado conforme a cidade.
- **RF-WEB-07:** preço “sob consulta” e taxas isentas/ausentes devem ser tratados sem valores fictícios.
- **RF-WEB-08:** filtros e contadores são derivados dos dados publicados.
- **RF-WEB-09:** compartilhar link de imóvel deve gerar título, descrição e imagem corretos.
- **RF-WEB-10:** preservar design system, responsividade e efeitos assinatura existentes.

### 5.5 Contato e leads

- formulário de visita com imóvel, nome, telefone/WhatsApp, e-mail opcional e consentimento;
- newsletter com consentimento separado e comprovável;
- validação no servidor, rate limit, honeypot e/ou solução antispam;
- confirmação visual somente após aceite real do servidor;
- notificação ao canal comercial e registro no destino aprovado;
- identificadores de origem, página e imóvel para mensuração;
- política de retenção e exclusão de dados pessoais.

O destino dos leads — CRM, e-mail transacional ou banco próprio — é uma decisão de negócio pendente. O site não deve simular sucesso em caso de falha.

## 6. Modelo de conteúdo proposto

### 6.1 Entidade `property`

| Grupo | Campo | Tipo | Regra proposta |
|---|---|---|---|
| Identificação | `code` | texto curto | Obrigatório e único; manter zeros à esquerda se existirem |
| Identificação | `slug` | texto | Único; gerado e editável com proteção após publicação |
| Workflow | `status` | enum | `draft`, `in_review`, `published`, `unavailable`, `sold`, `archived` |
| Workflow | `featured` | booleano | Controla seleção editorial |
| Negócio | `purpose` | enum | Somente `sale` no MVP |
| Negócio | `propertyType` | referência/enum | Tipos aprovados pelo negócio |
| Localização pública | `city`, `state`, `neighborhood` | texto/enum | Obrigatórios |
| Localização privada | `street`, `number`, `complement`, `postalCode` | texto | Acesso restrito; publicação configurável |
| Conteúdo | `title` | texto curto | Obrigatório |
| Conteúdo | `summary` | texto curto | Usado em card, compartilhamento e SEO |
| Conteúdo | `description` | conteúdo estruturado | Parágrafos, subtítulos e listas |
| Conteúdo | `features` | lista ordenável | Características e infraestrutura |
| Valores | `salePrice` | número + visibilidade | Valor em centavos ou decimal validado; permite “sob consulta” |
| Valores | `condoFee` | número + situação | Valor, isento ou não informado |
| Valores | `propertyTax` | número + período + situação | Mensal/anual a confirmar; isento ou não informado |
| Áreas | `totalArea`, `privateArea`, `landArea` | decimal em m² | Campos aplicáveis por tipo de imóvel |
| Cômodos | `bedrooms`, `suites`, `bathrooms`, `parkingSpaces` | inteiro | Não negativo; banheiros é acréscimo ao modelo atual |
| Mídia | `photos` | lista de `propertyPhoto` | Mínimo de 5 para publicar |
| Contato | `serviceRegion` | referência/enum | Define responsável/WhatsApp sem número espalhado no código |
| SEO | `seoTitle`, `metaDescription`, `shareImage` | texto/mídia | Preview e validação antes de publicar |
| Auditoria | autor e timestamps | sistema | Não editáveis pelo editor |

### 6.2 Entidade `propertyPhoto`

| Campo | Regra |
|---|---|
| `asset` | Referência ao original no storage do CMS |
| `order` | Ordem da galeria |
| `isCover` | Exatamente uma por imóvel |
| `altText` | Obrigatório, objetivo e descritivo |
| `caption` | Texto editorial mostrado na galeria, opcional conforme regra final |
| `roomType` | Categoria para organização e futura filtragem |
| `focalPoint` | Ponto principal para recortes responsivos |
| `rightsConfirmed` | Confirmação de autorização de uso, se exigida pelo negócio |

### 6.3 Conteúdos globais

Contatos, WhatsApps por região, e-mail, CRECI, textos institucionais, links de rodapé, hero e dados de SEO global devem existir em uma configuração única do site. Alterações críticas de contato devem exigir perfil de administrador ou revisão.

## 7. Armazenamento e entrega das fotos

### 7.1 Regra de armazenamento

- O navegador envia o arquivo diretamente ao serviço de mídia por URL assinada ou SDK seguro.
- O CMS guarda a referência do asset; o banco não guarda base64.
- O repositório guarda apenas código e arquivos visuais permanentes da marca.
- O CDN entrega derivados no tamanho e formato adequados ao dispositivo.
- URLs de mídia não devem conter segredos nem depender de sessão para conteúdo público.

### 7.2 Pipeline de processamento

1. validar formato, tamanho e dimensões;
2. corrigir orientação por metadados;
3. remover metadados sensíveis, especialmente GPS, das versões públicas;
4. gerar largura e altura, hash e placeholder de baixa qualidade;
5. disponibilizar AVIF/WebP com fallback compatível;
6. produzir tamanhos aproximados para thumbnail, card, mosaico e ampliação;
7. servir com `srcset`, `sizes`, cache longo e dimensões explícitas;
8. aplicar lazy loading, exceto na imagem principal acima da dobra.

O CMS/CDN deve fazer as transformações sob demanda ou no upload. Não serão geradas manualmente várias cópias por imóvel.

### 7.3 Política editorial inicial

- mínimo de 5 fotos para publicação, preservando a regra atual;
- a quantidade máxima, o peso máximo e a resolução mínima serão definidos após avaliar o padrão real das fotos;
- a capa deve funcionar em proporções horizontal de card e compartilhamento;
- imagens com marca d’água de terceiros, baixa resolução ou sem autorização devem ser bloqueadas no processo de revisão;
- a remoção definitiva de arquivos órfãos deve ocorrer por rotina controlada, nunca no mesmo clique de retirada da galeria.

## 8. Arquitetura alvo

```text
Editor autenticado
      |
      v
CMS / Studio ---------> Banco de conteúdo
      |                         |
      +-----------------> Storage + CDN de imagens
      |
      +---- webhook de publicação
                         |
Visitante ---> Vercel / Site público ---> páginas e catálogo
                         |
                         +---- API server-side de leads ---> destino comercial
```

### 8.1 Recomendação: Next.js + Sanity + Vercel

| Componente | Responsabilidade |
|---|---|
| Next.js | Catálogo, páginas individuais, SEO, preview e renderização responsiva |
| Sanity Studio | Formulários editoriais, usuários, validações, rascunhos e publicação |
| Sanity Content Lake | Fonte de verdade do catálogo e conteúdos globais |
| Sanity Asset CDN | Originais, recortes e formatos otimizados das fotos |
| Vercel | Deploy, previews, cache e funções server-side |
| Destino de leads a definir | CRM, banco ou serviço transacional aprovado |

**Por que é a recomendação:** o painel e a biblioteca de mídia já existem, schemas e validações são customizáveis, há preview editorial e a integração com CDN reduz trabalho de infraestrutura.

**Limitações:** dependência de fornecedor, custos conforme uso, necessidade de migração do frontend e serviço separado para leads/CRM.

### 8.2 Alternativas consideradas

| Opção | Vantagens | Desvantagens | Quando escolher |
|---|---|---|---|
| Supabase + painel próprio | Banco SQL, storage e autenticação sob maior controle | Painel, upload, revisão e preview precisam ser construídos e mantidos | Quando houver requisitos específicos de operação ou integração e orçamento de desenvolvimento contínuo |
| CMS baseado em Git | Simples e próximo do repositório | Ruim para muitas fotos, usuários não técnicos e workflow editorial | Catálogo muito pequeno e poucas alterações |
| WordPress/Directus gerenciado | Painel conhecido ou completo e APIs disponíveis | Mais manutenção, segurança e/ou custo operacional | Equipe já domina a ferramenta e há infraestrutura responsável |

### 8.3 Decisão sobre o frontend atual

Manter JavaScript puro consumindo uma API é possível, mas não é a recomendação para o estado alvo: páginas individuais, preview, metadados por imóvel, regeneração e tratamento de indisponibilidade ficam mais complexos. O visual atual deve ser migrado gradualmente, sem redesenho.

O [Plano 001](../plans/plan-001-modularizar-index.md) deve ser reavaliado antes da execução completa. Se Next.js for aprovado, a extração de dados e imagens continua útil, mas modularizar toda a SPA atual pode virar trabalho descartável.

## 9. Workflow editorial

```text
Rascunho -> Em revisão -> Publicado -> Indisponível/Vendido -> Arquivado
    ^            |
    +------------+ (ajustes solicitados)
```

### Critérios para publicar

- código único, tipo e localização pública preenchidos;
- título, resumo e descrição revisados;
- valores/situações financeiras válidos;
- áreas e quantidades coerentes e não negativas;
- no mínimo cinco fotos, uma capa e textos alternativos;
- contato regional configurado;
- preview conferido em desktop e mobile;
- metadados de SEO válidos.

Publicar deve invalidar/regenerar apenas catálogo, imóvel alterado, sitemap e páginas relacionadas. Despublicar deve removê-lo imediatamente de listagens e impedir indexação futura.

## 10. SEO, compartilhamento e analytics

- URL canônica por imóvel e redirecionamento quando o `slug` mudar;
- `title`, metadescrição, Open Graph e imagem social próprios;
- sitemap derivado somente de imóveis publicados;
- dados estruturados adequados ao conteúdo imobiliário, validados antes do lançamento;
- robots e canonicals corretos para preview, filtros e imóveis retirados;
- eventos mínimos: visualização de imóvel, abertura de galeria, clique em WhatsApp, envio de formulário e uso dos filtros;
- nenhuma ferramenta de analytics deve ser ativada sem avaliar consentimento e política de privacidade.

## 11. Requisitos não funcionais

### Performance

- LCP ≤ 2,5 s, INP ≤ 200 ms e CLS ≤ 0,1 no percentil 75 quando houver dados reais suficientes;
- Lighthouse ≥ 90 em Performance, SEO, Acessibilidade e Boas Práticas nas páginas principais;
- nenhuma imagem de imóvel em base64 no HTML;
- cache e revalidação documentados.

### Acessibilidade

- WCAG 2.2 AA como referência;
- operação por teclado, foco visível e modais/galeria acessíveis;
- texto alternativo obrigatório e contraste preservado;
- formulários com rótulos, instruções e erros anunciados.

### Segurança e LGPD

- autenticação gerenciada, menor privilégio e MFA para administradores quando disponível;
- segredos somente em variáveis de ambiente server-side;
- validação e sanitização no cliente e no servidor;
- logs sem conteúdo sensível desnecessário;
- consentimento, finalidade, retenção e canal de exclusão para leads e newsletter;
- backup/exportação periódica do conteúdo e procedimento de restauração testado;
- ambientes de preview e produção separados.

### Operação

- monitoramento de erros do frontend e das APIs de formulário;
- alerta para falha de webhook/publicação;
- documentação curta de cadastro para editores;
- possibilidade de exportar catálogo e referências das mídias.

## 12. Critérios de aceite do MVP

1. Um editor cria um imóvel completo, envia pelo menos cinco fotos, escolhe capa, reordena a galeria e envia para revisão.
2. O sistema bloqueia publicação quando código, conteúdo obrigatório, capa, alt text ou fotos mínimas estiverem ausentes.
3. Um publicador visualiza preview e publica sem acessar o repositório ou a Vercel.
4. O imóvel aparece no catálogo e em URL própria dentro do prazo definido.
5. A edição do preço, texto ou foto aparece após nova publicação e mantém histórico de autor/data.
6. Marcar como indisponível remove o imóvel dos resultados e trata a URL antiga conforme a política aprovada.
7. Fotos são entregues responsivamente, sem base64, sem GPS público e sem layout shift relevante.
8. Filtros, busca por código, WhatsApp e compartilhamento usam os dados do CMS.
9. Formulário válido chega ao destino real; falha de entrega gera erro e pode ser monitorada.
10. Testes em 375, 768 e 1280 px, console, acessibilidade e Lighthouse atendem ao checklist do projeto.

## 13. Fora do escopo inicial

- aluguel;
- portal para proprietários ou compradores;
- CRM imobiliário completo;
- sincronização automática com portais externos;
- assinatura eletrônica e gestão de contratos;
- recomendação por inteligência artificial;
- aplicativo móvel nativo;
- edição profissional de fotos dentro do painel;
- múltiplos idiomas.

Esses itens podem ser fases futuras, mas não devem atrasar o catálogo operacional.

## 14. Roadmap proposto

### Fase 0 — Decisões e inventário

- validar orçamento, usuários, volume de imóveis/fotos e destino de leads;
- confirmar a stack recomendada;
- revisar contatos, CRECI, política de privacidade e dados atuais;
- definir política de URL para imóveis vendidos/indisponíveis.

### Fase 1 — Fundação de conteúdo e mídia

- criar schemas, papéis, validações e configurações globais;
- configurar biblioteca de mídia e regras de upload;
- criar Studio, preview e ambientes;
- testar o fluxo completo com conteúdo de homologação aprovado.

### Fase 2 — Site público

- migrar design atual para componentes;
- implementar catálogo, filtros e página individual;
- implementar imagens responsivas, SEO, sitemap e compartilhamento;
- preservar efeitos visuais com `prefers-reduced-motion`.

### Fase 3 — Leads e conformidade

- integrar destino comercial;
- implementar validação server-side, antispam, consentimento e monitoramento;
- publicar política de privacidade e retenção.

### Fase 4 — Migração e lançamento

- importar imóveis e mídias aprovados;
- revisão editorial e conferência de contatos;
- QA funcional, visual, acessibilidade, segurança e performance;
- preview aprovado pelo usuário;
- plano de rollback e lançamento gradual.

### Fase 5 — Evolução pós-MVP

- importação por planilha;
- integração com CRM e portais;
- busca avançada, mapa e favoritos;
- dashboards de conversão e qualidade editorial.

## 15. Riscos e mitigação

| Risco | Mitigação |
|---|---|
| Fotos elevam custo e pioram performance | CDN, derivados automáticos, limites configuráveis e orçamento de mídia |
| Conteúdo incompleto é publicado | Schema obrigatório, checklist e papel de publicador |
| Endereço privado é exposto | Separar endereço público/privado e restringir permissões |
| Código do imóvel muda e quebra links | Código único e estável; slug com redirecionamento |
| Dependência do CMS | Exportação periódica, documentação do schema e abstração da consulta |
| Formulários perdem leads | Resposta transacional real, logs, alertas e retentativa quando aplicável |
| Migração altera o visual | Baseline por screenshots e regressão nas três larguras obrigatórias |
| Escopo cresce para um CRM | Respeitar “fora de escopo” e usar fases posteriores |

## 16. Decisões pendentes para aprovação

1. Aprovar **Next.js + Sanity + Vercel** ou escolher a alternativa com Supabase/painel próprio.
2. Quantos usuários editarão e quem poderá publicar?
3. Quantos imóveis ativos e quantas fotos por imóvel são esperados no primeiro ano?
4. Qual é o peso e a resolução típicos das fotos recebidas?
5. O endereço completo pode aparecer publicamente ou deve permanecer privado?
6. IPTU será informado por mês ou por ano? Há outros valores obrigatórios?
7. Qual será o destino dos leads: CRM, e-mail, WhatsApp, banco ou combinação?
8. Qual política usar para URL de imóvel vendido/indisponível: manter página informativa, redirecionar ou retornar 410?
9. Newsletter fará parte do MVP? Em qual plataforma e com qual processo de consentimento?
10. Há necessidade de importar imóveis por planilha já no lançamento?
11. Qual orçamento mensal aceitável para CMS, mídia, e-mail, monitoramento e analytics?
12. Quem fornecerá e validará textos, fotos, direitos de uso, contatos e dados legais reais?

## 17. Próxima decisão recomendada

Realizar uma reunião curta de descoberta para responder às decisões pendentes e, em seguida, produzir a especificação técnica da Fase 1 com custos, ambientes, schemas definitivos, wireframe do formulário editorial e plano de migração dos seis registros de demonstração. Nenhum dado demonstrativo deve ser promovido para produção sem validação explícita do negócio.

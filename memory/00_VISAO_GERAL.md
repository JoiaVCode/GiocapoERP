# Giocapo ERP — visão geral

## Regra vigente de memory e acesso ao GitHub — 09/11/2026

Esta regra substitui as orientações anteriores de manter documentação somente nos anexos/contexto e de exigir branch temporária para atualizar Markdown.

### Gatilhos e autorização permanente

- Ao usuário dizer **“versão aprovada”** para a implementação atual, atualizar automaticamente os Markdown afetados em `JoiaVCode/GiocapoERP/memory/`, registrando versão, data, mudanças aprovadas, regras, arquitetura/banco quando afetados, evidências de testes, pendências e commit correspondente quando efetivamente conhecido.
- Pedidos com o sentido de **incluir na memory** também autorizam atualizar os Markdown necessários: “coloca na memory”, “inclua na memory”, “registre a correção no memory” e expressões equivalentes. Não exigir frase exata nesses pedidos.
- Um pedido de registro na memory não transforma implementação provisória em aprovada: manter explícita a distinção entre planejado, em desenvolvimento, testado e aprovado.
- Ler os arquivos atuais do repositório antes de editar. Atualizar somente os documentos pertinentes, preservar decisões históricas relevantes e resolver divergências sem inventar informações.
- Fazer commits diretamente na `main`, sem criar branch ou PR, para essas atualizações de documentação. Não pedir confirmação adicional para ações já autorizadas por esses gatilhos.
- Incluir título e descrição nos commits. Ao concluir, informar documentos atualizados, principais registros e link(s) dos commits; confirmar persistência somente após sucesso e verificação.
- A pasta `memory/` no GitHub é a referência persistente dessas instruções e do contexto. Cópias locais, Library ou anexos do projeto podem estar desatualizadas; não afirmar que anexos foram substituídos automaticamente.
- Não registrar senhas, tokens ou dados sensíveis. Não alterar código ou banco apenas para documentar.

### Capacidades técnicas verificadas e limites de autorização

| Operação | Evidência e regra |
|---|---|
| Ler arquivos e diretórios | Funcionou no repositório. |
| Atualizar arquivo existente diretamente na main | Confirmado em `memory/05_ESTADO_ATUAL.md`, commit `4486f1aaf7009a503fefdb43cbf69257311f6546`. |
| Criar arquivo novo diretamente na main | Confirmado nos outros cinco Markdown de memory, sem arquivos-base. |
| Criar branch | A tentativa anterior retornou HTTP 403, `Resource not accessible by integration`. Esse erro não significa ausência geral de escrita em arquivos; não presumir que criar branches funciona. |
| Criar PR, excluir arquivos, administrar repositório ou reescrever histórico | Não validados por esses testes; não presumir capacidade ou autorização. |
| Substituir anexos nas configurações do projeto ChatGPT | Não disponível nas ferramentas usadas; atualização do GitHub não substitui esses anexos. |

A instalação exibida pelo usuário permite leitura/escrita em código e acesso a todos os repositórios, mas a capacidade efetiva depende da operação e da conexão. Não recomendar reconexão ou ampliação de permissões como solução comprovada quando não houver diagnóstico.

A liberdade permanente concedida aqui cobre os Markdown necessários em `memory/` e os commits diretos de documentação. Não equivale a autorização irrestrita para alterar/publicar código do ERP, banco, outros repositórios, excluir conteúdo ou reescrever histórico. Essas ações seguem o escopo solicitado pelo usuário e o protocolo de aprovação do projeto. Uma nova instrução explícita do usuário pode alterar esse escopo.

**Versão atual aprovada: v6.18.5 — aprovação explícita em 10/11/2026.**

Base: `v6.18.4` aprovada; entrega aprovada é a revisão de `v6.18.5.html` com carregamento discreto e mensagens específicas. O usuário informou funcionamento geral e aprovou a revisão. Isso não comprova individualmente todos os testes físicos ou de dispositivos.

A migração `giocapo_v6_18_5_require_active_approved_access` foi aplicada em 09/11/2026; o ajuste visual de 10/11 não exigiu nova alteração no banco. Commit de publicação do HTML v6.18.5 não conferido nesta aprovação; não presumir publicação por este registro.

## Arquitetura e segurança vigentes

Mantidos HTML único, Supabase Auth e estado operacional JSONB versão 3 com revisão otimista. O acesso operacional agora exige simultaneamente conta ativa e aprovada no HTML e nas verificações pertinentes do servidor. O perfil próprio continua consultável para informar status e permitir aprovação/reativação.

O navegador acompanha o próprio perfil por Realtime e consultas periódicas. Ao bloquear, remove dados operacionais da memória, cache e interface, interrompe sincronização/presença/histórico e descarta respostas antigas por geração de acesso. A recuperação usa dados novos do servidor.

Verificação de sessão usa o carregamento discreto da v6.18.4. Telas maiores são destinadas a criação pendente, rejeição e conta desativada/removida; erros de conexão usam apresentação compacta. A arquitetura de isolamento de leitura por módulo continua planejada, não implementada nesta etapa.

## Histórico preservado — estado anterior à aprovação da v6.18.5

As seções seguintes descrevem versões e decisões anteriores. O estado vigente é o registrado acima; referências a v6.18.5 como futura são históricas.

**Versão atual aprovada: v6.18.4 — aprovação explícita em 09/11/2026.**

Aprovação registrada após o usuário confirmar, pelo Console do site com conta limitada, a rejeição das oito tentativas independentes: `location`, `series`, `type`, `hce`, `balance`, `code`, `codeId` e `productId`. O servidor respondeu “Alteração incompatível com a ação autorizada: products.edit”.

Base de desenvolvimento: arquivo único `v6.18.4.html` entregue nesta conversa. Commit correspondente à v6.18.4 não consultado nem confirmado; não presumir publicação no GitHub. A aprovação original foi documentada no contexto; a autorização vigente acima determina manutenção automática dos Markdown pertinentes na pasta `memory/`.

## Arquitetura vigente

Mantidos HTML único, Supabase Auth, estado JSONB versão 3 e revisão otimista. A v6.18.4 restringe a função SQL de comparação de alterações: `products.edit` só admite o equipamento original ou a normalização exata decorrente da mudança de categoria. A simples edição de nome/nome de exibição não modifica equipamentos. A prevenção de XSS da v6.18.3 permanece implementada.

Próxima fase planejada: v6.18.5, padronizar acesso operacional para usuário ativo e aprovado, preservando fluxos pendentes e de aprovação. CSP/SRI, senhas e isolamento de leitura por módulo continuam pendentes.

## Histórico preservado — estado aprovado anterior, v6.18.3

O conteúdo seguinte descreve o estado anterior; as seções acima definem o estado vigente da v6.18.4.

**Versão atual aprovada: v6.18.3 — aprovação explícita em 09/11/2026.**

Commit confirmado no `main`: `96da47f756cfe52abe5b15a19d61808d342651a3` (`v6.18.3`, de 06/11/2026). O blob do HTML entregue coincide com o `index.html` desse commit: `a3c2943bd89498acd6534aa69719f56a01ae71f4`.

## Objetivos, tecnologias e arquitetura atuais

Mantidos o HTML único com CSS/JavaScript embutidos, Supabase Auth, PostgreSQL e o estado operacional JSONB versão 3 com revisão otimista e RPC de escrita.

A v6.18.3 acrescenta prevenção de XSS: 39 handlers que interpolavam dados foram substituídos por delegação de eventos em `click`, `change` e `mousedown`. `safeEventAttrs` serializa argumentos JSON com escape HTML; `dispatchSafeEvent` usa uma lista fixa de ações, sem eval. IDs são validados no navegador e no banco. A renderização revisada escapa atributos de IDs/opções e mantém os escapes de texto existentes.

Continuam pendentes CSP/SRI, correção da autorização de `products.edit`, padronização ativo/aprovado, limpeza de cache no logout e isolamento de leitura por módulo. A aprovação não representa implementação dessas etapas.

## Histórico preservado — fotografia de 06/11/2026 anterior à implementação

As informações abaixo descrevem a v6.18.2 e o planejamento daquele momento. Afirmações como “atual”, “não aplicado” ou “próxima etapa” nesse registro são históricas; o estado vigente é o registrado acima.


**Contexto consolidado em:** 06/11/2026  
**Versão atual aprovada:** v6.18.2  
**Repositório:** JoiaVCode/GiocapoERP, branch `main`  
**Estado desta documentação:** retrato do sistema e planejamento; não representa implementação das correções de segurança.

## Objetivo

O Giocapo é um ERP web para organizar o cadastro e o controle de equipamentos topográficos, produtos, códigos, kits e rotinas relacionadas. Também oferece gestão de usuários, permissões, histórico, importação/exportação e impressão de etiquetas.

## Tecnologias verificadas

| Camada | Estado observado |
|---|---|
| Interface e aplicação | Aplicação estática em um único arquivo HTML, com CSS e JavaScript embutidos. |
| Hospedagem do código | Repositório GitHub `JoiaVCode/GiocapoERP`; a aplicação é entregue como site estático. O mecanismo e os cabeçalhos HTTP efetivamente servidos não foram revalidados nesta consolidação. |
| Autenticação e sessão | Supabase Auth. |
| Banco | Supabase/PostgreSQL 17.6, projeto `GiocapoERP`, região `sa-east-1`. |
| Cliente Supabase | `supabase-js` UMD 2.117.2 carregado de CDN jsDelivr no HTML. |
| Estado operacional | Um documento JSONB compartilhado na tabela `public.app_state`, versão de dados 3. |
| Presença | Supabase Realtime Presence é usado para refletir usuários on-line. |
| Impressão | Geração de PDFs no navegador para etiquetas e outros impressos do ERP. |

Não foram incluídas URLs, chaves ou outros valores de configuração que não sejam necessários à documentação.

## Arquitetura atual

O front-end monolítico mantém os módulos e as regras de interface em um só HTML. Os dados operacionais são mantidos em um objeto de estado que contém `products`, `codes`, `equipments`, `kits`, `nextKitNumber` e `dataVersion`.

O navegador lê o estado de `public.app_state`. Para gravar, chama `public.save_giocapo_state`, informando a ação, a revisão esperada e o novo estado. A função valida autenticação, permissão, estrutura e diferenças permitidas; a atualização usa revisão para evitar sobrescrever mudanças concorrentes. A tabela também registra auditoria das mudanças de estado por trigger.

Dados de usuário, permissões, pedidos de alteração de nome e histórico administrativo ficam em tabelas próprias. Algumas regras de autorização são aplicadas no servidor por funções no schema `app_private` e por RLS; outras decisões de interface são refletidas no HTML.

## Limites arquiteturais conhecidos

- O documento operacional agrega vários módulos em um único JSONB. A política atual de leitura permite que qualquer usuário ativo autenticado leia o estado completo; ela não filtra os arrays por permissão de módulo.
- O HTML é monolítico e ainda usa eventos inline e renderização dinâmica por HTML. Isso torna uma CSP estrita incompatível com o estado atual sem refatoração e testes.
- A chave `controle_kits_v2` guarda uma cópia local do estado. A auditoria da v6.18.2 relatou que o logout encerra a sessão sem limpar essa cópia.
- Uma permissão de interface não deve ser tratada como isolamento de dados. O servidor precisa aplicar a autorização nas leituras e gravações.

## Fontes e grau de confiança

**Verificado diretamente nesta consolidação:** arquivo v6.18.2 anexado, commit atual do `main` consultado anteriormente e estrutura/políticas/funções do Supabase consultadas em modo somente leitura em 06/11/2026.

**Recuperado da transcrição de segurança:** riscos observados em testes isolados, recomendações, métricas de busca de código e roteiro de correções. Esses números são evidência da auditoria registrada, não uma nova medição de cada trecho nesta edição.

**Não verificado aqui:** resposta HTTP efetiva da hospedagem, configuração dos cabeçalhos do site, estado de todos os navegadores/dispositivos, restauração de backup e homologação de impressão física.


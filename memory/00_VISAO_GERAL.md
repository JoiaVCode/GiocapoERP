# Giocapo ERP — visão geral

## Regra de atualização do contexto — 09/11/2026

Por instrução explícita do usuário, atualizar somente os arquivos Markdown de contexto deste projeto. Após “versão aprovada”, registrar as alterações aprovadas nesses documentos e confirmar sua persistência aqui. Não tentar criar branches, commits, pull requests ou alterar arquivos diretamente no GitHub para atualizar a documentação, salvo solicitação explícita futura do usuário.

Esta regra substitui a preferência anterior de persistir a documentação no repositório. A recusa HTTP 403 anterior permanece apenas como histórico; não é motivo para tentar novamente. Nenhum envio manual ao GitHub é obrigatório para concluir a atualização do contexto.

**Versão atual aprovada: v6.18.4 — aprovação explícita em 09/11/2026.**

Aprovação registrada após o usuário confirmar, pelo Console do site com conta limitada, a rejeição das oito tentativas independentes: `location`, `series`, `type`, `hce`, `balance`, `code`, `codeId` e `productId`. O servidor respondeu “Alteração incompatível com a ação autorizada: products.edit”.

Base de desenvolvimento: arquivo único `v6.18.4.html` entregue nesta conversa. Commit correspondente à v6.18.4 não consultado nem confirmado; não presumir publicação no GitHub. A aprovação original atualizou somente o contexto. Em solicitação posterior de 09/11/2026, o usuário autorizou explicitamente criar este Markdown atualizado em `memory/` por commit direto na `main`, sem criar branch. Esta autorização não se estende automaticamente a futuras alterações.

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


# Giocapo ERP — estado atual

## Regra de atualização do contexto — 09/11/2026

Por instrução explícita do usuário, atualizar somente os arquivos Markdown de contexto deste projeto. Após “versão aprovada”, registrar as alterações aprovadas nesses documentos e confirmar sua persistência aqui. Não tentar criar branches, commits, pull requests ou alterar arquivos diretamente no GitHub para atualizar a documentação, salvo solicitação explícita futura do usuário.

Esta regra substitui a preferência anterior de persistir a documentação no repositório. A recusa HTTP 403 anterior permanece apenas como histórico; não é motivo para tentar novamente. Nenhum envio manual ao GitHub é obrigatório para concluir a atualização do contexto.

**Versão atual aprovada: v6.18.4 — aprovação explícita em 09/11/2026.**

Aprovação registrada após o usuário confirmar, pelo Console do site com conta limitada, a rejeição das oito tentativas independentes: `location`, `series`, `type`, `hce`, `balance`, `code`, `codeId` e `productId`. O servidor respondeu “Alteração incompatível com a ação autorizada: products.edit”.

Base de desenvolvimento: arquivo único `v6.18.4.html` entregue nesta conversa. Commit correspondente à v6.18.4 não consultado nem confirmado; não presumir publicação no GitHub. A aprovação original atualizou apenas o contexto. Posteriormente, em 09/11/2026, o usuário autorizou explicitamente atualizar este arquivo em `memory/05_ESTADO_ATUAL.md` por commit direto na `main`, sem criar branch, com título e descrição de commit.

## Estado atual e próximos passos

A v6.18.4 está oficialmente aprovada e passa a ser a base de desenvolvimento. Correção HTML entregue e migração SQL aplicada. A v6.18.3 permanece como etapa anterior aprovada de prevenção de XSS.

Verificação: 76 casos HTML/SQL, 27 verificações de regressão e 39 testes de eventos, sem erros de página no conjunto final. Teste manual reportado: todas as oito tentativas independentes pela conta limitada foram recusadas. Não foi relatado resultado individual dos testes manuais de categorias, impressão física, dispositivos móveis ou sincronização em duas sessões; aprovação não deve ser convertida em alegação desses testes.

Próxima implementação planejada: v6.18.5, padronizar ativo/aprovado nas verificações operacionais, preservando consulta do próprio cadastro pendente e aprovação administrativa. Permanecem planejados SRI/senhas, CSP progressiva e isolamento de leitura por módulo; também pendem limpeza do cache no logout, revisão de grants e remoção de sankhya.view.

A aprovação foi registrada nos seis Markdown de contexto. Esta cópia em `memory/05_ESTADO_ATUAL.md` é atualizada por solicitação explícita posterior do usuário; não implica autorização geral para futuras escritas no GitHub. Não alterar código ou banco apenas para documentação.

## Histórico preservado — estado aprovado anterior, v6.18.3

O conteúdo seguinte descreve o estado anterior; as seções acima definem o estado vigente da v6.18.4.

**Versão atual aprovada: v6.18.3 — aprovação explícita em 09/11/2026.**

Commit confirmado no `main`: `96da47f756cfe52abe5b15a19d61808d342651a3` (`v6.18.3`, de 06/11/2026). O blob do HTML entregue coincide com o `index.html` desse commit: `a3c2943bd89498acd6534aa69719f56a01ae71f4`.

## Estado atual e próxima implementação

A v6.18.3 está oficialmente aprovada. O HTML foi entregue, o main contém o commit correspondente e a validação de IDs do Supabase foi aplicada em 06/11/2026. Não houve modificação de código ou banco apenas para atualizar esta documentação.

Concluído: 39 handlers dinâmicos convertidos, escape de atributos, validação de IDs nas entradas de estado, restauração em falhas e validação SQL reforçada.

Validação registrada: 27 verificações isoladas no Chromium, 39 testes de despacho de eventos e verificações SQL após migração, sem erros de página no conjunto final. O usuário confirmou cadastro de Local/Série com marcação exibida literalmente e sincronizado na v6.18.3. Não há relato detalhado de homologação física Zebra, de todas as contas ou de dispositivos móveis; a aprovação não é evidência da execução individual desses testes.

Próxima implementação planejada: v6.18.4, restringir `products.edit` aos efeitos legítimos de categoria, preservando a normalização necessária dos equipamentos. Depois: ativo/aprovado, SRI/senhas, CSP progressiva e isolamento de leitura por módulo. Permanecem os demais riscos da auditoria fora do escopo da v6.18.3 e a remoção pendente de `sankhya.view`.

Documentação: seis arquivos atualizados; escrita no GitHub impedida por HTTP 403 da integração. A instrução posterior do usuário dispensa inclusão no repositório; a documentação deve ser mantida somente no contexto. A aprovação e esta atualização não fazem merge automático.

## Histórico preservado — fotografia de 06/11/2026 anterior à implementação

As informações abaixo descrevem a v6.18.2 e o planejamento daquele momento. Afirmações como “atual”, “não aplicado” ou “próxima etapa” nesse registro são históricas; o estado vigente é o registrado acima.


**Fotografia em:** 06/11/2026  
**Versão atual aprovada:** v6.18.2  
**Estado:** preparação documental para iniciar correções de segurança; nenhuma delas foi aplicada.

## Código e repositório

- Repositório: `JoiaVCode/GiocapoERP`, branch `main`.
- Commit consultado: `2a6b14e93430211ea838590f1b0cb267c426e13d`, mensagem `v6.18.2`.
- O HTML anexado pelo usuário é um arquivo único com 390.224 bytes e 6.659 quebras de linha; seu Git blob SHA é `9f93435fc47022bbad1516af1c756ee943555f84`, coincidente com o blob informado para o `index.html` do `main`.
- O front-end contém CSS e JavaScript inline, além da biblioteca `supabase-js` 2.117.2 servida por CDN. O levantamento anterior encontrou 159 manipuladores inline e 39 chamadas de `innerHTML`; esses totais são métricas da auditoria registrada, não uma recontagem feita para este documento.
- Não foi encontrada referência a Sankhya no HTML atual.
- A ausência de CSP/SRI foi observada no HTML. Cabeçalhos efetivamente retornados pela hospedagem ainda não foram verificados nesta consolidação.

## Supabase

- Projeto ativo em PostgreSQL 17.6, região `sa-east-1`.
- Cinco tabelas públicas, todas com RLS habilitada: `app_state`, `app_users`, `role_permissions`, `user_change_requests`, `erp_audit_history`.
- Dados operacionais: estado versão 3, revisão 293, 56 produtos, 66 códigos, 119 equipamentos, 1 kit (242 registros com ID); estado atualizado em `2026-11-05T16:46:00.397917+00:00`.
- Cinco perfis registrados, todos ativos e aprovados; composição consultada anteriormente: um admin, três operators e um viewer. Nenhum e-mail/nome é incluído aqui.
- Há 14 migrações listadas, última `20261030010647_giocapo_admin_audit_history`.
- Achados principais: leitura de `app_state` não isola por módulo; a validação de IDs não restringe formato; `products.edit` aceita alterações em equipamentos ligados ao produto; há diferença entre condição `active` da policy de leitura e condição `active + approved` da função de autorização.
- `save_giocapo_state` é `SECURITY DEFINER`, exige auth, ação válida e permissão, valida JSON e diff, trava a linha e confere a revisão antes da gravação. Advisor alerta sobre a exposição a authenticated, exigindo revisão de ACL/função; a classificação não é prova isolada de exploit.
- A auditoria anterior registrou proteção de Auth contra senhas vazadas desativada, três avisos de initplan RLS e dois índices sem uso.

## Correções: estado e próxima etapa

**Nenhuma correção de segurança foi iniciada ou aplicada.** O planejamento disponível prevê:

1. **v6.18.3 — XSS e IDs:** reforçar validação no banco e entradas locais/importadas; remover handlers com dados dinâmicos; revisar renderização HTML; manter CSP inalterada. É a próxima etapa planejada, não uma versão já criada.
2. **Depois:** corrigir `products.edit`, padronizar ativo/aprovado, avaliar SRI e proteção de senha, refatorar e implantar CSP progressivamente.
3. **Etapa arquitetural posterior:** restringir leitura por módulo.

## Riscos que devem guiar a implementação

- A mudança de eventos/renderização tem impacto alto no HTML; exige regressão de edição, duplicação, exclusão, filtros, grupos, montagem/edição de kits, gestão de usuários, importação e etiquetas.
- O servidor precisa rejeitar IDs inválidos mesmo quando a requisição não passa pelo HTML.
- A normalização de equipamentos durante edição de categorias de produto é uma exceção legítima que não pode ser quebrada na correção de `products.edit`.
- CSP estrita prematura pode bloquear eventos, estilos, Auth/Realtime, downloads/blob e impressão; só ativar depois de homologar e confirmar suporte a cabeçalhos HTTP.
- Separar leituras por módulo pode afetar sincronização, importação/exportação, montagem de kits e versões antigas abertas em outros dispositivos.

## Critérios de teste já propostos

- ID válido aceito; ID com aspas/marcação rejeitado pela API/banco.
- Texto contendo markup aparece como texto, sem executar script.
- Edição, duplicação, exclusão e agrupamentos de equipamentos continuam funcionando.
- Montagem, edição e impressão de kits continuam funcionando.
- Importação válida preserva relações; importação com ID inválido é bloqueada com mensagem clara.
- Operações de usuário/permissão, login, recuperação de senha e sincronização entre sessões continuam funcionando.
- Impressão simples, dupla e Ctrl/Cmd+clique deve ser testada; impressão física Zebra ainda exige teste real.
- Testes devem usar contas descartáveis e dados sintéticos. Não declarar teste real de contas, dispositivos ou impressora sem execução correspondente.

## Confirmações ainda necessárias antes de mudanças

- Confirmar backup restaurável e ambiente de teste isolado; a auditoria não demonstrou ensaio de restauração.
- Confirmar o cabeçalho de segurança e o mecanismo de publicação atualmente servidos pelo domínio.
- Verificar migração/backup de dados antigos e todos os geradores de IDs antes de adotar regex.
- Definir como homologar CSP e como reverter eventual mudança estrutural de banco.
- Revalidar grants excessivos, ACL e exposição do schema `app_private` por meio das configurações reais de API.
- Confirmar testes físicos da Zebra e testes em dispositivos móveis.


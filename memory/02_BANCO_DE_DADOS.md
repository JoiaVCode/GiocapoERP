# Giocapo ERP — banco de dados

## Regra de atualização do contexto — 09/11/2026

Por instrução explícita do usuário, atualizar somente os arquivos Markdown de contexto deste projeto. Após “versão aprovada”, registrar as alterações aprovadas nesses documentos e confirmar sua persistência aqui. Não tentar criar branches, commits, pull requests ou alterar arquivos diretamente no GitHub para atualizar a documentação, salvo solicitação explícita futura do usuário.

Esta regra substitui a preferência anterior de persistir a documentação no repositório. A recusa HTTP 403 anterior permanece apenas como histórico; não é motivo para tentar novamente. Nenhum envio manual ao GitHub é obrigatório para concluir a atualização do contexto.

**Versão atual aprovada: v6.18.4 — aprovação explícita em 09/11/2026.**

Aprovação registrada após o usuário confirmar, pelo Console do site com conta limitada, a rejeição das oito tentativas independentes: `location`, `series`, `type`, `hce`, `balance`, `code`, `codeId` e `productId`. O servidor respondeu “Alteração incompatível com a ação autorizada: products.edit”.

Base de desenvolvimento: arquivo único `v6.18.4.html` entregue nesta conversa. Commit correspondente à v6.18.4 não consultado nem confirmado; não presumir publicação no GitHub. A aprovação original atualizou somente o contexto. Em solicitação posterior de 09/11/2026, o usuário autorizou explicitamente criar este Markdown atualizado em `memory/` por commit direto na `main`, sem criar branch. Esta autorização não se estende automaticamente a futuras alterações.

## Migração aprovada da v6.18.4

Em 09/11/2026 foi aplicada `giocapo_v6_18_4_restrict_product_equipment_changes`, substituindo somente `app_private.giocapo_state_change_allowed(jsonb,jsonb,text)`. Preservados atributos, demais ramos de ação, tabelas, grants e RLS.

O ramo `products.edit` mantém uma única edição de produto, sem adições/exclusões de equipamentos e sem alterações de códigos/kits/sequência. Calcula o equipamento esperado a partir do anterior e da nova categoria, comparando o objeto inteiro: campos fora da normalização, vínculos e equipamentos de outros produtos devem permanecer idênticos. Categoria alterada exige um array com exatamente uma categoria reconhecida pelo formulário.

Migração executada com 76 assertions transacionais baseadas em estados produzidos pelo HTML. A primeira tentativa tinha erro de separação de instruções e foi recusada; a seguinte concluiu. Revisão antes/depois: 329; hash MD5 do JSON antes/depois: c2c8556eb9542673744edee7eb5c0c50; estado válido. Esses valores descrevem o momento da implantação, não um snapshot atual após testes do usuário.

A falha de `products.edit` descrita nos registros históricos abaixo foi corrigida. Leituras por módulo, ativo/aprovado, cache e alertas anteriores fora do escopo continuam pendentes. SQL anterior e novo foram preservados no pacote v6.18.4_suporte.zip; rollback reabre a falha e exige avaliação técnica.

## Histórico preservado — estado aprovado anterior, v6.18.3

O conteúdo seguinte descreve o estado anterior; as seções acima definem o estado vigente da v6.18.4.

**Versão atual aprovada: v6.18.3 — aprovação explícita em 09/11/2026.**

Commit confirmado no `main`: `96da47f756cfe52abe5b15a19d61808d342651a3` (`v6.18.3`, de 06/11/2026). O blob do HTML entregue coincide com o `index.html` desse commit: `a3c2943bd89498acd6534aa69719f56a01ae71f4`.

## Banco: mudança aplicada e aprovada

Em 06/11/2026 foi aplicada a migração `giocapo_v6_18_3_validate_identifiers`, aprovada oficialmente em 09/11/2026.

A função `app_private.giocapo_json_array_has_unique_ids(jsonb)` mantém linguagem SQL, IMMUTABLE e `search_path` vazio. Agora retorna false para entrada que não seja array, elementos que não sejam objetos, ID que não seja string ou que não atenda a `^[A-Za-z0-9_-]{1,64}$`, além de IDs repetidos. A validação geral de estado usa essa função; referências continuam sujeitas às regras de integridade existentes.

A migração inclui uma verificação do estado existente, cancelando a aplicação se houver incompatibilidade. Não houve alteração de tabelas, relações, RLS ou permissões nesta entrega. A revisão permaneceu 293 imediatamente após a aplicação; isso é evidência de 06/11, não uma contagem atual de 09/11.

Testes SQL após aplicação confirmaram estado válido e rejeição de aspas, markup, números, NULL, entrada não array, duplicação, comprimento excessivo e quebra de linha. Os testes não gravaram dados sintéticos na produção. SQL de migração e rollback foram preservados no pacote de suporte entregue.

A falha de formato dos IDs descrita no snapshot abaixo foi corrigida. Os outros achados permanecem pendentes; não houve nova auditoria integral do banco nesta aprovação.

## Histórico preservado — fotografia de 06/11/2026 anterior à implementação

As informações abaixo descrevem a v6.18.2 e o planejamento daquele momento. Afirmações como “atual”, “não aplicado” ou “próxima etapa” nesse registro são históricas; o estado vigente é o registrado acima.


**Consulta somente leitura em:** 06/11/2026  
**Projeto Supabase:** `GiocapoERP` (`dqmntzvnmfnlyjqbhffz`), PostgreSQL 17.6, `sa-east-1`.  
**Aviso:** este arquivo registra o estado observado nesta data; confirme novamente antes de qualquer DDL ou mudança de política.

## Tabelas observadas

Todas as cinco tabelas do schema `public` consultadas têm RLS habilitada. Não foi observado `FORCE ROW LEVEL SECURITY`.

| Tabela | Finalidade e estrutura principal | Relacionamentos observados |
|---|---|---|
| `public.app_state` | Estado operacional global: `id`, `data` JSONB, `data_version`, `revision`, `updated_at`, `updated_by`. Há uma linha (`id = main`), versão 3, revisão 293 na consulta. | `updated_by` → `auth.users.id`. |
| `public.app_users` | Perfil do ERP: `user_id`, `display_name`, `role`, `active`, `created_at`, `email`, `permissions` JSONB, estado e dados de aprovação, `last_seen_at`, `permission_mode`. Papéis permitidos: `admin`, `operator`, `viewer`; aprovação: `pending`, `approved`, `rejected`. | `user_id` → `auth.users.id`; `approval_reviewed_by` → `auth.users.id`. |
| `public.role_permissions` | JSONB de permissões padrão por papel, com `updated_at` e `updated_by`. Chave primária `role`. Há três papéis. | `updated_by` → `auth.users.id`. |
| `public.user_change_requests` | Pedidos de alteração de nome: usuário, tipo/valor solicitado, estado, datas, revisor, valor aprovado e nota. | `user_id` e `reviewed_by` → `auth.users.id`. |
| `public.erp_audit_history` | Histórico de produtos/equipamentos, com ator, operação, entidade, estado antes/depois, contexto, origem e lista de alterações. Operações permitidas no constraint: `created`, `updated`, `deleted`, `duplicated`. | Não foi observada FK em `actor_user_id`; IDs de entidade são texto. |

### Estrutura do estado operacional

O JSONB contém seis chaves: `dataVersion`, `products`, `codes`, `equipments`, `kits` e `nextKitNumber`. A versão aceita no banco é 3. Cada array de entidade exige objeto com ID não vazio e único; o banco também valida referências de equipamento para produto/código e de kit para equipamento.

Snapshot do conteúdo em `app_state` na consulta: 56 produtos, 66 códigos, 119 equipamentos e 1 kit: **242 registros com ID**. Revisão 293; última atualização registrada `2026-11-05T16:46:00.397917+00:00`.

## RLS e autorização observadas

| Tabela | Políticas observadas |
|---|---|
| `app_state` | `active_users_can_read_state`: SELECT para `authenticated` se o perfil correspondente tiver `active = true`. Não verifica `approval_status` nem permissões por módulo. O acesso de escrita da aplicação passa pela RPC privilegiada, além das regras e privilégios SQL existentes. |
| `app_users` | Leitura do próprio perfil ou por administrador/permissões de gestão, consulta ou aprovação. UPDATE por admin ou permissões `users.manage`/`permissions.manage`; trigger adicional protege atualização delegada. |
| `role_permissions` | Leitura do próprio papel ou por perfis com poderes de gestão/administração. UPDATE por admin, com restrição para não atualizar o papel `admin`; há trigger de proteção. |
| `user_change_requests` | SELECT do próprio pedido ou por quem tem `approvals.name`. Solicitações e revisões também passam por funções RPC. |
| `erp_audit_history` | SELECT condicionado a `app_private.has_permission('history.view')`. |

O banco também possui privilégios SQL mais amplos que o necessário em algumas tabelas/roles, incluindo operações administrativas que devem ser revisadas. A transcrição confirma as concessões excessivas, mas não demonstrou uma rota REST explorável para `TRUNCATE` com apenas a chave pública.

## Funções relevantes

| Função | Papel observado |
|---|---|
| `public.save_giocapo_state(action_key, expected_revision, new_data, new_data_version)` | `SECURITY DEFINER`. Exige usuário autenticado, valida ação/versão/estrutura, confere `has_permission`, trava a linha principal, rejeita revisão incompatível e verifica as diferenças permitidas antes de gravar. O Supabase marca a exposição a authenticated para revisão manual; isso, isoladamente, não comprova uma vulnerabilidade. |
| `app_private.has_permission(permission_key)` | Resolve admin, permissões personalizadas ou matriz por papel; exige `active = true` e `approval_status = 'approved'`. |
| `app_private.giocapo_state_is_valid(data, version)` | Valida versão 3, conjunto de chaves, IDs únicos não vazios e referências entre entidades. Não restringe os caracteres/formato do ID. |
| `app_private.giocapo_json_array_has_unique_ids(array)` | Confere tipo array, IDs não vazios e unicidade; não valida expressão regular/alfabeto seguro. |
| `app_private.giocapo_state_change_allowed(old, new, action)` | Compara alterações e limita cada ação. A regra atual de `products.edit` permite que equipamentos ligados ao produto editado também sejam alterados, desde que continuem associados ao mesmo produto; a auditoria identificou alterações indevidas de campos de equipamento por essa via. |
| `app_private.giocapo_log_state_changes()` | Trigger de auditoria para mudança de `app_state.data`. |
| `app_private.is_admin()` | Verifica papel administrativo. |
| `app_private.protect_delegated_user_update()` e `protect_admin_permissions()` | Protegem alterações delegadas em perfis e permissões administrativas. |
| `app_private.protect_last_admin()` | Trigger para proteger o último administrador ativo. |
| `app_private.handle_new_auth_user()` | Cria perfil do ERP após inserção de usuário em Auth. |
| `app_private.guard_auth_user_deletion()` | Bloqueia condições proibidas de exclusão de conta. |
| `app_private.request_display_name_change()` / `review_user_change_request()` | Solicitação e aprovação/rejeição de alteração de nome. |
| `app_private.review_user_activation()` | Fluxo administrativo de ativação/aprovação. |
| `app_private.touch_user_last_seen()` | Atualiza último acesso/presença. |

Há wrappers públicos para alguns fluxos de identidade/aprovação e para `save_giocapo_state`. As funções internas observadas usam `search_path` vazio. As funções `SECURITY DEFINER` precisam continuar sendo revisadas por origem, ACL e autorização; não as tratar como falha automática nem presumir que são inofensivas.

## Triggers observados

- `auth.users`: `on_auth_user_created_erpsp` chama `app_private.handle_new_auth_user()`; `guard_erp_auth_user_deletion` chama `app_private.guard_auth_user_deletion()`.
- `public.app_state`: `trg_giocapo_state_audit` registra alterações do JSONB.
- `public.app_users`: `protect_delegated_user_update` e `protect_last_admin_update`.
- `public.role_permissions`: `protect_admin_permissions_update`.

O nome `on_auth_user_created_erpsp` preserva uma referência legada, embora a função chame Giocapo.

## Migrações e serviços

Foram listadas 14 migrações. A mais recente é `20261030010647_giocapo_admin_audit_history`. Não apareceu migração posterior à versão v6.18.2 na lista consultada; o estado pode conter mudanças feitas por outra via, portanto a lista não prova por si só ausência de alterações.

Serviços observados anteriormente na auditoria: Edge Function `giocapo-delete-user` ativa, com verificação JWT e controles administrativos; `temporary-print` ativa, mas retorna 410 Gone; bucket `temporary-labels` privado, limite de 5 MB, sem objetos na consulta anterior.

## Alertas registrados

- Leitura do estado inteiro para qualquer usuário ativo autenticado, sem isolamento por permissão de módulo.
- Falta de restrição de caracteres dos IDs no banco.
- Regra `products.edit` permissiva em relação a alterações concomitantes de equipamentos.
- Inconsistência entre políticas que usam apenas `active = true` e funções que exigem ativo e aprovado.
- Proteção contra senhas vazadas desativada no Auth, segundo o diagnóstico registrado.
- Alerta de advisors para `save_giocapo_state` como `SECURITY DEFINER` disponível a authenticated; exige revisão da implementação e grants.
- Três alertas de performance para initplans de RLS e dois índices sem uso foram relatados; não são, por si, vulnerabilidades.


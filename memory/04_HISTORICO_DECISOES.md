# Giocapo ERP — histórico de decisões

## Regra de atualização do contexto — 09/11/2026

Por instrução explícita do usuário, atualizar somente os arquivos Markdown de contexto deste projeto. Após “versão aprovada”, registrar as alterações aprovadas nesses documentos e confirmar sua persistência aqui. Não tentar criar branches, commits, pull requests ou alterar arquivos diretamente no GitHub para atualizar a documentação, salvo solicitação explícita futura do usuário.

Esta regra substitui a preferência anterior de persistir a documentação no repositório. A recusa HTTP 403 anterior permanece apenas como histórico; não é motivo para tentar novamente. Nenhum envio manual ao GitHub é obrigatório para concluir a atualização do contexto.

**Versão atual aprovada: v6.18.4 — aprovação explícita em 09/11/2026.**

Aprovação registrada após o usuário confirmar, pelo Console do site com conta limitada, a rejeição das oito tentativas independentes: `location`, `series`, `type`, `hce`, `balance`, `code`, `codeId` e `productId`. O servidor respondeu “Alteração incompatível com a ação autorizada: products.edit”.

Base de desenvolvimento: arquivo único `v6.18.4.html` entregue nesta conversa. Commit correspondente à v6.18.4 não consultado nem confirmado; não presumir publicação no GitHub. A aprovação original atualizou somente o contexto. Em solicitação posterior de 09/11/2026, o usuário autorizou explicitamente criar este Markdown atualizado em `memory/` por commit direto na `main`, sem criar branch. Esta autorização não se estende automaticamente a futuras alterações.

## Decisão e aprovação — 09/11/2026, v6.18.4

O teste anterior do usuário confirmou gravação indevida de sete campos de equipamento usando `products.edit`; somente `productId` já era bloqueado. Após a correção, o usuário repetiu o teste no site e confirmou as oito recusas pela regra de autorização, com HTTP 400 e mensagem específica.

O usuário declarou “versão aprovada” para a v6.18.4. Decisão: comparar o equipamento inteiro com a normalização determinística, em vez de liberar qualquer alteração nos campos série/tipo/HCE/saldo. Motivo: permitir somente consequências legítimas da categoria e impedir que a mesma operação esconda alterações independentes.

O HTML passou a normalizar somente quando a categoria muda e alinhou saldo/tipo/HCE ao resultado esperado pelo banco. Não houve escrita no GitHub. Histórico e decisões anteriores ficam preservados abaixo.

## Histórico preservado — estado aprovado anterior, v6.18.3

O conteúdo seguinte descreve o estado anterior; as seções acima definem o estado vigente da v6.18.4.

**Versão atual aprovada: v6.18.3 — aprovação explícita em 09/11/2026.**

Commit confirmado no `main`: `96da47f756cfe52abe5b15a19d61808d342651a3` (`v6.18.3`, de 06/11/2026). O blob do HTML entregue coincide com o `index.html` desse commit: `a3c2943bd89498acd6534aa69719f56a01ae71f4`.

## Decisão aprovada em 09/11/2026

O usuário utilizou a expressão exata “versão aprovada” para a v6.18.3. A prevenção de XSS e a validação de identificadores passam de provisórias a aprovadas.

A implementação converteu 39 handlers dinâmicos para delegação, revisou escapes de atributos, validou entradas de estado e garantiu restauração do estado anterior em falhas. A migração de validação de IDs foi aplicada ao Supabase em 06/11/2026. CSP foi deliberadamente mantida para etapa posterior; autenticação, permissões, `products.edit` e leitura por módulo não foram corrigidas nesta versão.

O commit v6.18.3 já estava no main em 06/11/2026 e foi confirmado na aprovação. As fases v6.18.4 em diante continuam propostas, sem implementação nesta aprovação.

Em 09/11/2026 a criação da branch `docs/v6.18.3-aprovada` foi recusada com HTTP 403, `Resource not accessible by integration`. Nenhum documento foi escrito no GitHub por esta operação. Os seis Markdown foram atualizados de forma persistente no contexto; por instrução posterior do usuário, não há pendência de inclusão no repositório.

O resultado do teste manual de ID sugerido no console não foi informado; não registrar sua execução como comprovada. O erro transitório de sincronização na v6.18.2 não foi reproduzido pelo usuário e sua causa não foi determinada.

## Histórico preservado — fotografia de 06/11/2026 anterior à implementação

As informações abaixo descrevem a v6.18.2 e o planejamento daquele momento. Afirmações como “atual”, “não aplicado” ou “próxima etapa” nesse registro são históricas; o estado vigente é o registrado acima.


Este registro preserva motivos e estado das decisões. **“Planejada” não significa implementada.** Datas referem-se às informações disponíveis nas conversas e consultas recuperadas.

## Base atual e fluxo de trabalho

| Data/contexto | Decisão ou fato | Estado |
|---|---|---|
| 06/11/2026 | O usuário confirmou `v6.18.2` como versão atual aprovada. A leitura do GitHub apontou o commit `2a6b14e93430211ea838590f1b0cb267c426e13d`, mensagem `v6.18.2`; o blob do `index.html` anexado coincide com `9f93435fc47022bbad1516af1c756ee943555f84`. | Base de referência confirmada. |
| Histórico do projeto | O ERP foi consolidado em aplicação monolítica de HTML único com CSS/JS embutidos, usando Supabase Auth e sincronização do estado operacional. | Implementado na base. |
| Histórico do projeto | Alterações devem ser isoladas em branch temporária; o usuário revisa e faz o merge manual após aprovação. Não alterar `main` por conta própria. | Regra de trabalho recuperada; verificar acesso atual antes de qualquer ação. |
| Histórico do projeto | O fluxo de escrita pelo conector GitHub já encontrou erro 403. | Limitação anterior; não foi revalidada nesta etapa. |

## Decisões e funcionalidades de produto registradas

- Navegação atual inclui Equipamentos, Produtos, Montar Kit, Kits Ativos, Calculadora de Diárias, Usuários, Permissões, Histórico e Dados; área Conta também existe. O módulo Sankhya não está no HTML v6.18.2.
- A sincronização usa um estado JSON versão 3, revisão otimista e RPC de escrita que valida ações no servidor.
- Foram incorporados autenticação, níveis de acesso, perfis customizados, aprovações, presença e histórico administrativo.
- Impressões, importação/exportação, regras de cadastro e apresentação visual são parte do comportamento aprovado da v6.18.2; devem ser preservadas ao corrigir segurança.

## Auditoria de segurança e roteiro

| Ordem proposta | Mudança | Motivo/risco | Estado |
|---|---|---|---|
| v6.18.3 | Prevenção de XSS: validar IDs, remover dados dinâmicos de handlers inline e revisar renderização HTML. | Maior risco confirmado: ID aceito pelo banco pode alcançar atributo executável; os testes da transcrição mostraram interpretação de markup. Mudanças no HTML têm impacto alto e regressões possíveis em listas, kits e impressão. | Próxima implementação planejada; ainda não iniciada. |
| v6.18.4 proposta | Corrigir a autorização de `products.edit`, preservando normalizações legítimas ligadas à categoria. | Evitar que permissão de produto modifique campos independentes de equipamento. Risco de rejeitar normalização legítima. | Planejada, não implementada. |
| v6.18.5 proposta | Padronizar as verificações de usuário ativo e aprovado. | Impedir acesso operacional por usuário pendente/inativo sem quebrar a tela de espera e aprovação. | Planejada, não implementada. |
| v6.18.6 proposta | Adicionar SRI ao script Supabase e revisar proteção contra senhas vazadas/configuração de Auth; preparar CSP. | Reduzir risco de cadeia/CDN e credenciais. SRI incompatível pode impedir login; política de senha pode dificultar cadastros. | Planejada, não implementada. |
| v6.18.7 proposta | Aplicar CSP efetiva após modo de relatório, refatoração dos eventos e homologação. | CSP estrita pode bloquear scripts, estilos, WebSocket, PDFs/blob, exportações e impressão. | Planejada, não implementada. |
| Etapa arquitetural | Restringir leituras do estado por módulo, possivelmente separando dados ou criando API seletiva. | A leitura atual expõe o JSON completo a qualquer usuário ativo; alteração arriscada para sincronização e relações entre módulos. | Planejada para depois das refatorações anteriores. |

Os números v6.18.3–v6.18.7 são uma proposta de organização registrada na conversa; não são tags, arquivos de versão ou commits existentes.

## Decisão sobre CSP

A CSP não deve ser ativada estritamente na primeira entrega. A transcrição registrou que permitir scripts por hashes não mantém os handlers `onclick` funcionando. A ordem escolhida foi: remover dependências inline, testar configuração em ambiente de relatório/homologação e só então aplicar política efetiva por cabeçalhos HTTP. A configuração real da hospedagem ainda precisa ser confirmada.

## Decisão sobre Sankhya

O usuário informou que a permissão `sankhya.view` pode ser removida. A consulta no banco mostrou a chave em `role_permissions` para `operator` (`true`) e `viewer` (`false`), sem perfis customizados contendo a chave; o HTML atual não possui módulo Sankhya. **A decisão está registrada, mas a remoção não foi executada.**

## Divergência de contagem resolvida

A transcrição cita 236 IDs numa passagem e 242 em outra. A consulta atual ao estado no Supabase encontrou 242 registros: 56 produtos, 66 códigos, 119 equipamentos e 1 kit. Para a fotografia desta documentação, usa-se o total medido de 242; a divergência textual da transcrição fica preservada como observação histórica.


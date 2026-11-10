# Giocapo ERP — histórico de decisões

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

## Aprovação e decisões — 10/11/2026, v6.18.5

O relatório diagnostico.docx mostrou tela branca para pendentes/inativos/rejeitados, dados e ações residuais após desativação, cloudReady ainda true e interface desatualizada após exclusão. As leituras operacionais das contas desativadas foram negadas no diagnóstico; dados já carregados não comprovavam novas leituras autorizadas.

Decidiu-se corrigir o fluxo de inicialização, tratar perfil ausente, exigir ativo + aprovado, limpar dados no bloqueio e manter monitor independente para recuperação. O usuário também autorizou bloquear quando não for possível confirmar acesso, com impacto no uso offline.

Em 09/11 foi aplicada a migração. Os testes SQL usaram contas sintéticas em subtransação revertida; a primeira tentativa foi cancelada porque a fixture administrativa contrariava constraint existente, depois corrigida sem mudança de regra de produção.

Na revisão de 10/11 o usuário pediu o loader discreto da v6.18.4 durante verificação, telas maiores só para estados da conta e textos individualizados. A versão permaneceu v6.18.5 por estar em homologação.

O usuário declarou “versão aprovada” em 10/11/2026. Essa aprovação cobre a revisão final entregue e a implementação descrita acima. Mantidas as decisões das v6.18.3 e v6.18.4. Próximas fases permanecem planejadas.

## Histórico preservado — estado anterior à aprovação da v6.18.5

As seções seguintes descrevem versões e decisões anteriores. O estado vigente é o registrado acima; referências a v6.18.5 como futura são históricas.

**Versão atual aprovada: v6.18.4 — aprovação explícita em 09/11/2026.**

Aprovação registrada após o usuário confirmar, pelo Console do site com conta limitada, a rejeição das oito tentativas independentes: `location`, `series`, `type`, `hce`, `balance`, `code`, `codeId` e `productId`. O servidor respondeu “Alteração incompatível com a ação autorizada: products.edit”.

Base de desenvolvimento: arquivo único `v6.18.4.html` entregue nesta conversa. Commit correspondente à v6.18.4 não consultado nem confirmado; não presumir publicação no GitHub. A aprovação original foi documentada no contexto; a autorização vigente acima determina manutenção automática dos Markdown pertinentes na pasta `memory/`.

## Decisão sobre persistência — 09/11/2026

Após confirmar escrita e criação de arquivos na main, o usuário autorizou permanentemente atualizar os Markdown pertinentes de memory por aprovação de versão ou pedido equivalente de registro. A restrição anterior de atualizar apenas cópias no contexto foi superada. A falha de criação de branch foi distinguida do acesso funcional a arquivos. Os limites técnicos e de escopo constam na regra vigente acima.

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


# Giocapo ERP — módulos

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

## Recursos aprovados na v6.18.5

- Autenticação/acesso: corrigida tela branca; mensagens próprias para criação pendente, rejeição, desativação e conta não encontrada.
- Sessão: logo e moldura amarela nas telas de status, ações Verificar novamente e Voltar ao login; verificação normal usa loader discreto.
- Operação: permissões exigem ativo + aprovado; bloqueio fecha modais, limpa tabelas, campos, estado, permissões e caches operacionais.
- Sincronização/presença/histórico: interrompidos no bloqueio; respostas de operações antigas são descartadas. Aprovação/reativação recarrega dados do servidor.
- Recuperação de senha: mantém tela separada visível. Calculadora pública permanece no fluxo sem login.
- PDFs ainda controlados pela página são removidos/fechados e URLs revogadas no bloqueio, sem possibilidade de recolher cópias já salvas.

Próxima etapa planejada: v6.18.6, integridade dos scripts/SRI, avaliação de proteção de senhas e preparação da CSP. Não confundir com ativação de CSP efetiva, prevista para fase posterior e dependente de homologação.

## Histórico preservado — estado anterior à aprovação da v6.18.5

As seções seguintes descrevem versões e decisões anteriores. O estado vigente é o registrado acima; referências a v6.18.5 como futura são históricas.

**Versão atual aprovada: v6.18.4 — aprovação explícita em 09/11/2026.**

Aprovação registrada após o usuário confirmar, pelo Console do site com conta limitada, a rejeição das oito tentativas independentes: `location`, `series`, `type`, `hce`, `balance`, `code`, `codeId` e `productId`. O servidor respondeu “Alteração incompatível com a ação autorizada: products.edit”.

Base de desenvolvimento: arquivo único `v6.18.4.html` entregue nesta conversa. Commit correspondente à v6.18.4 não consultado nem confirmado; não presumir publicação no GitHub. A aprovação original foi documentada no contexto; a autorização vigente acima determina manutenção automática dos Markdown pertinentes na pasta `memory/`.

## Módulos e alterações aprovadas na v6.18.4

Produtos: renomeação mantém equipamentos intactos; mudança de categoria aplica normalização específica. Equipamentos: bloqueadas mudanças independentes por `products.edit`, inclusive nos campos confirmados pelo teste manual. Edição pelo fluxo `equipment.edit` foi preservada nos testes automatizados.

Não foram implementadas novas permissões, telas ou alterações de autenticação. Próxima entrega planejada: v6.18.5, ativo/aprovado.

## Histórico preservado — estado aprovado anterior, v6.18.3

O conteúdo seguinte descreve o estado anterior; as seções acima definem o estado vigente da v6.18.4.

**Versão atual aprovada: v6.18.3 — aprovação explícita em 09/11/2026.**

Commit confirmado no `main`: `96da47f756cfe52abe5b15a19d61808d342651a3` (`v6.18.3`, de 06/11/2026). O blob do HTML entregue coincide com o `index.html` desse commit: `a3c2943bd89498acd6534aa69719f56a01ae71f4`.

## Funcionalidades aprovadas na v6.18.3

- Eventos seguros em produtos, equipamentos, códigos, agrupamentos, kits, impressão, usuários e aprovações; 39 handlers dinâmicos convertidos.
- Escape de atributos usados por campos de usuários, produtos e equipamentos.
- Validação de IDs e referências recebidos por importação, cache e sincronização.
- `prepareState` restaura o estado anterior quando migração, normalização ou validação falha; importação recusada informa o motivo.
- Formatos legados continuam podendo gerar IDs ausentes de equipamentos/kits; IDs explicitamente incompatíveis são rejeitados.

Próxima etapa planejada: v6.18.4, corrigir `products.edit` preservando as normalizações legítimas de categoria. Demais módulos permanecem conforme a base histórica abaixo.

## Histórico preservado — fotografia de 06/11/2026 anterior à implementação

As informações abaixo descrevem a v6.18.2 e o planejamento daquele momento. Afirmações como “atual”, “não aplicado” ou “próxima etapa” nesse registro são históricas; o estado vigente é o registrado acima.


**Base documentada:** v6.18.2 aprovada pelo usuário, conferida com o HTML anexado.  
**Distinção:** “implementado” descreve o que existe na base; “planejado” não significa que já foi codificado ou publicado.

## Módulos implementados

| Módulo | Funcionalidades observadas na base |
|---|---|
| Equipamentos | Listagem e consulta, cadastro, edição, duplicação e exclusão; agrupamento de códigos e estoque; associação com produto e código; dados de série, tipo, HCE e local; ajuste de saldo; impressão de etiquetas. As ações dependem de permissões como `equipment.view`, `equipment.create`, `equipment.edit`, `equipment.delete` e `equipment.print`. |
| Produtos | Cadastro, edição e exclusão; nome e nome de exibição; seleção de categorias/variáveis. A edição normaliza alguns campos dos equipamentos associados quando categorias como Acessório, Receptor e Coletora mudam. |
| Montar Kit | Seleção de equipamentos e montagem de kits; validações de compatibilidade, inclusive para equipamentos laser/HCE. |
| Kits Ativos | Consulta, impressão, edição e desmonte de kits; kits mantêm IDs dos equipamentos e número sequencial. |
| Calculadora de Diárias | Ferramenta de cálculo de diárias disponível na navegação. A transcrição não documenta regras financeiras detalhadas; confirmar fórmulas e arredondamentos no código antes de alterá-los. |
| Usuários | Consulta e gestão de perfis, atividade/presença, permissões personalizadas e fluxo de aprovação, conforme as permissões atribuídas. |
| Permissões | Matriz por papel e permissões personalizadas por usuário, com persistência automática segundo o histórico técnico. Há os papéis `admin`, `operator` e `viewer`. |
| Histórico | Consulta de eventos administrativos de criação, edição, exclusão e duplicação de produtos/equipamentos, com comparativos antes/depois. A leitura depende de `history.view`; a exportação de dados é controlada por `history.export` na interface. |
| Dados | Importação e exportação de backup JSON e operações de limpeza, sujeitas a permissões. A validação do estado também ocorre no Supabase. |
| Conta | Perfil/conta, alteração de senha, recuperação e saída da sessão. O HTML contém fluxos de autenticação e telas de conta. |

### Recursos transversais

- Login com Supabase Auth, recuperação de senha e gestão de sessão.
- Sincronização do estado operacional e controle otimista por número de revisão.
- Presença de usuários on-line.
- Interface de usuário guest para acesso à calculadora, conforme identificado no HTML.
- Impressão de etiquetas de equipamento, kit, local, O.S. e consumo; alguns fluxos distinguem clique simples e Ctrl/Cmd+clique.
- Histórico administrativo persistido pelo Supabase.

## Segurança planejada, ainda não implementada

O primeiro incremento planejado é a **v6.18.3**, com escopo exclusivo de prevenção de XSS:

1. Restringir IDs de produtos, códigos, equipamentos e kits no banco e nas entradas do navegador/importação.
2. Remover a interpolação de valores de dados em atributos de evento JavaScript inline; usar associação segura de eventos.
3. Revisar os pontos de `innerHTML` e inserir dados não confiáveis no contexto correto.
4. Rejeitar IDs incompatíveis com mensagem compreensível, sem renomear silenciosamente e quebrar relações.

Esta etapa não ativa CSP e não altera autenticação, permissões, regra de `products.edit` ou arquitetura de leitura por módulos.

O roteiro registrado depois propõe, ainda sem implementação: corrigir `products.edit`; padronizar usuário ativo/aprovado; adicionar SRI e avaliar a proteção contra senhas vazadas; refatorar eventos e implantar CSP gradualmente; por fim, estudar isolamento da leitura por módulo. A divisão de versões v6.18.4 a v6.18.7 é somente uma proposta de organização.

## Itens que exigem confirmação no código antes de uma mudança

- Fórmula e regras de arredondamento da Calculadora de Diárias.
- Casos exatos da normalização de equipamentos acionada ao editar categorias de produto.
- Regras completas de compatibilidade de kits além da validação descrita na auditoria.
- Comportamento de cada opção de backup e compatibilidade de arquivos antigos.
- Testes físicos de impressão Zebra e comportamento em dispositivos móveis.


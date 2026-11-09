# Giocapo ERP — módulos

## Regra de atualização do contexto — 09/11/2026

Por instrução explícita do usuário, atualizar somente os arquivos Markdown de contexto deste projeto. Após “versão aprovada”, registrar as alterações aprovadas nesses documentos e confirmar sua persistência aqui. Não tentar criar branches, commits, pull requests ou alterar arquivos diretamente no GitHub para atualizar a documentação, salvo solicitação explícita futura do usuário.

Esta regra substitui a preferência anterior de persistir a documentação no repositório. A recusa HTTP 403 anterior permanece apenas como histórico; não é motivo para tentar novamente. Nenhum envio manual ao GitHub é obrigatório para concluir a atualização do contexto.

**Versão atual aprovada: v6.18.4 — aprovação explícita em 09/11/2026.**

Aprovação registrada após o usuário confirmar, pelo Console do site com conta limitada, a rejeição das oito tentativas independentes: `location`, `series`, `type`, `hce`, `balance`, `code`, `codeId` e `productId`. O servidor respondeu “Alteração incompatível com a ação autorizada: products.edit”.

Base de desenvolvimento: arquivo único `v6.18.4.html` entregue nesta conversa. Commit correspondente à v6.18.4 não consultado nem confirmado; não presumir publicação no GitHub. A aprovação original atualizou somente o contexto. Em solicitação posterior de 09/11/2026, o usuário autorizou explicitamente criar este Markdown atualizado em `memory/` por commit direto na `main`, sem criar branch. Esta autorização não se estende automaticamente a futuras alterações.

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


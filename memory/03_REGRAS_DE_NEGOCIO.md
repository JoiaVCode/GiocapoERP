# Giocapo ERP — regras de negócio e decisões operacionais

## Regra de atualização do contexto — 09/11/2026

Por instrução explícita do usuário, atualizar somente os arquivos Markdown de contexto deste projeto. Após “versão aprovada”, registrar as alterações aprovadas nesses documentos e confirmar sua persistência aqui. Não tentar criar branches, commits, pull requests ou alterar arquivos diretamente no GitHub para atualizar a documentação, salvo solicitação explícita futura do usuário.

Esta regra substitui a preferência anterior de persistir a documentação no repositório. A recusa HTTP 403 anterior permanece apenas como histórico; não é motivo para tentar novamente. Nenhum envio manual ao GitHub é obrigatório para concluir a atualização do contexto.

**Versão atual aprovada: v6.18.4 — aprovação explícita em 09/11/2026.**

Aprovação registrada após o usuário confirmar, pelo Console do site com conta limitada, a rejeição das oito tentativas independentes: `location`, `series`, `type`, `hce`, `balance`, `code`, `codeId` e `productId`. O servidor respondeu “Alteração incompatível com a ação autorizada: products.edit”.

Base de desenvolvimento: arquivo único `v6.18.4.html` entregue nesta conversa. Commit correspondente à v6.18.4 não consultado nem confirmado; não presumir publicação no GitHub. A aprovação original atualizou somente o contexto. Em solicitação posterior de 09/11/2026, o usuário autorizou explicitamente criar este Markdown atualizado em `memory/` por commit direto na `main`, sem criar branch. Esta autorização não se estende automaticamente a futuras alterações.

## Regras vigentes da edição de produtos

- Sem mudança de categoria, `products.edit` não pode modificar nenhum campo de equipamento.
- Alteração de categoria exige uma categoria reconhecida e permite exclusivamente o resultado calculado pelo servidor.
- Acessório: série `N/S`, tipo vazio, HCE desativado e saldo mínimo 1 a partir do saldo anterior.
- Outras categorias: removem saldo. Receptor mantém tipo existente ou usa `RX` se vazio; demais limpam tipo. Coletora mantém HCE existente ou inicializa desativado se ausente; demais desativam HCE.
- Trocar Acessório por categoria seriada preserva `N/S`, conforme comportamento anterior; a série real deve ser definida pela edição de equipamento.
- Local, código, codeId, productId, IDs e campos adicionais não podem mudar independentemente por `products.edit`.
- Ter `equipment.edit` não libera alterações arbitrárias dentro de `products.edit`: a edição independente deve usar a ação própria.
- A validação é aplicada no Supabase e também protege requisições vindas de HTML antigo. HTML antigo pode sofrer recusa ao normalizar desnecessariamente numa renomeação; usar a base v6.18.4.

## Histórico preservado — estado aprovado anterior, v6.18.3

O conteúdo seguinte descreve o estado anterior; as seções acima definem o estado vigente da v6.18.4.

**Versão atual aprovada: v6.18.3 — aprovação explícita em 09/11/2026.**

Commit confirmado no `main`: `96da47f756cfe52abe5b15a19d61808d342651a3` (`v6.18.3`, de 06/11/2026). O blob do HTML entregue coincide com o `index.html` desse commit: `a3c2943bd89498acd6534aa69719f56a01ae71f4`.

## Regras vigentes após aprovação

- IDs operacionais devem ser strings únicas de 1–64 caracteres, apenas A–Z, a–z, 0–9, hífen e sublinhado. A regra é aplicada no banco e nas entradas do navegador.
- Referências locais também são validadas antes da normalização. Não renomear IDs malformados automaticamente.
- Para migrações legadas, IDs ausentes de equipamentos/kits podem ser gerados pelo comportamento anterior; não confundir ausência legada com ID explicitamente inválido.
- Dados não podem compor instruções JavaScript em handlers dinâmicos. Ações usam delegação e argumentos serializados/escapados.
- Uma falha ao preparar estado recebido restaura o estado anterior; a importação exibe motivo compreensível e mantém dados anteriores.
- Texto com marcação em Local/Série já era escapado na v6.18.2; sua exibição literal, isoladamente, não prova a correção dos IDs.
- Ambas as versões apontam para o banco com a validação nova. Comparações entre HTMLs não reproduzem o banco anterior.
- A regra de aprovação explícita e o merge manual continuam vigentes. A próxima base de desenvolvimento é o HTML v6.18.3 entregue.

## Histórico preservado — fotografia de 06/11/2026 anterior à implementação

As informações abaixo descrevem a v6.18.2 e o planejamento daquele momento. Afirmações como “atual”, “não aplicado” ou “próxima etapa” nesse registro são históricas; o estado vigente é o registrado acima.


**Base:** v6.18.2 e estrutura do banco consultada em 06/11/2026. Regras que não aparecem completas no histórico devem ser confirmadas no HTML antes de alteração.

## Dados e relações

- O estado sincronizado usa versão de dados 3 e agrupa produtos, códigos, equipamentos e kits em um único JSON.
- Cada entidade tem ID próprio. Equipamento referencia um produto e um código; kit referencia equipamentos existentes.
- `nextKitNumber` deve ser número inteiro a partir de 1 e é incrementado na montagem de kit conforme a validação do banco.
- IDs devem ser únicos e não vazios. A validação atual **não restringe caracteres**, mesmo que os IDs gerados normalmente sigam um formato interno.
- Importações devem preservar referências entre registros. Não corrigir IDs automaticamente: isso pode romper vínculos de equipamentos e kits.

## Usuários e permissões

- Papéis existentes: `admin`, `operator`, `viewer`.
- O perfil pode usar matriz de permissões por papel ou permissões personalizadas (`permission_mode`/`permissions`).
- A função de autorização exige simultaneamente usuário ativo e aprovado.
- O administrador tem tratamento especial; regras/triggers protegem permissões administrativas e o último administrador ativo.
- Cadastros e mudanças de nome passam por fluxos de aprovação no servidor.
- Ocultar uma aba ou botão no HTML não substitui a validação de autorização no banco/API.
- A permissão `sankhya.view` não corresponde a uma página no HTML atual; foi encontrada como chave residual na matriz de papéis (`operator: true`, `viewer: false`) e não em perfis customizados. O usuário autorizou que ela seja removida; a remoção ainda não foi executada.

## Operações de equipamentos e produtos

- Cadastro, edição, duplicação, exclusão e ajuste de saldo de equipamentos usam chaves de ação distintas no salvamento.
- Exclusão de produto é bloqueada na interface quando há equipamentos associados; exclusão de código é bloqueada quando há equipamentos que o utilizam.
- Alterações de categoria de produto podem normalizar informações de equipamentos associados. A regra atual precisa ser preservada com exatidão ao corrigir `products.edit`.
- O problema de autorização registrado é que `products.edit` pode ser usado para modificar campos de equipamentos ligados ao produto editado sem exigir `equipment.edit`; a regra do servidor não limita quais campos de equipamento podem mudar.
- Código/serial/local/HCE e saldo possuem regras específicas no HTML que devem ser verificadas antes de refatorar.

## Kits

- Kits são formados por referências a equipamentos existentes e guardam nome, número e metadados de atualização no estado da aplicação.
- O servidor valida unicidade dos equipamentos listados e referências válidas.
- O HTML possui uma validação de compatibilidade para determinados kits laser/HCE.
- Montagem, edição e desmonte são ações separadas com permissões próprias e são comparadas pelo servidor.

## Histórico e dados

- O histórico cobre criação, edição, duplicação e exclusão de produtos/equipamentos, incluindo ator, horário, operação e dados antes/depois.
- `history.view` dá acesso aos registros. `history.export` controla a função de exportação do ERP, mas não impede que alguém copie dados que já pode visualizar.
- Backup JSON pode ser importado/exportado com permissões próprias. A importação passa pela função de salvamento e validação de estado.
- O Supabase mantém estado operacional em uma linha JSONB global; consequência: permissões de módulo não isolam os dados recebidos.
- O navegador mantém cache em `localStorage` sob `controle_kits_v2`. A transcrição registra que a cópia não é limpa ao sair; é um ponto planejado de segurança, sem mudança aplicada.

## Identificadores e prevenção de XSS

- A aplicação não deve interpretar valores de dados como código ou markup executável.
- A regra proposta para IDs na próxima correção é `^[A-Za-z0-9_-]{1,64}$`. É uma proposta da transcrição, ainda não aplicada. Antes de adotá-la, confirmar compatibilidade com IDs de todos os ambientes, backups e geração de IDs.
- Valores não confiáveis devem ser inseridos como texto ou escapados de acordo com o contexto HTML/atributo/URL; escapar HTML não torna segura interpolação dentro de JavaScript.
- Eventos devem ser associados por `addEventListener`/delegação, sem handlers JavaScript montados com dados dinâmicos.
- Não corrigir automaticamente IDs malformados: retornar erro claro e preservar backup para análise.

## Regras de mudança e publicação

- `v6.18.2` é a versão atual aprovada, confirmada pelo usuário e correspondente ao commit atual do `main` consultado.
- Correções em desenvolvimento são provisórias. “Funcionou” não equivale a aprovação oficial; a expressão **“versão aprovada”** é o gatilho do protocolo de aprovação do projeto.
- O roteiro de segurança não é implementação nem aprovação de mudança de banco. Cada fase precisa ser desenvolvida/testada e aprovada segundo o fluxo do projeto.
- `sankhya.view` foi autorizada para remoção, porém não houve alteração no banco nesta etapa de contexto.


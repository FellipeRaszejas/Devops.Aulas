# Semana 02 — Resumo: Controle de Versão Avançado & GitFlow

## Estrutura interna do Git (DAG)
O Git guarda **snapshots imutáveis** do projeto (não diffs) encadeados num grafo. Os 4 objetos principais:
- **Blob**: o conteúdo cru de um arquivo (sem nome/permissão).
- **Tree**: como uma pasta — mapeia nomes de arquivo para blobs (ou sub-trees).
- **Commit**: aponta para uma tree raiz + metadados (autor, data, mensagem) + ponteiro(s) para o(s) commit(s) pai(s).
- **Ref**: ponteiro móvel para um commit (ex: `main`, uma tag).

## GitFlow — as 5 branches
| Branch | Nasce de | Vai para | Propósito |
|---|---|---|---|
| `main` | — | — | Código em produção. Nunca recebe commit direto. |
| `develop` | `main` | `main` (via release) | Integração contínua de tudo que está pronto. |
| `feature/*` | `develop` | `develop` | Isolamento de uma funcionalidade específica. |
| `release/*` | `develop` | `main` + `develop` | Homologação e ajustes finais antes do lançamento. |
| `hotfix/*` | `main` | `main` + `develop` | Correção urgente de bug crítico em produção. |

Regra geral: **tudo nasce de uma branch "pai" e sempre volta para ela** (ou para duas, no caso de release/hotfix).

## Conventional Commits
Padrão de mensagem: `tipo(escopo opcional): descrição no imperativo`.

Tipos principais: `feat`, `fix`, `docs`, `refactor`, `chore`. O sufixo `!` (ex: `feat!:`) sinaliza uma **breaking change**.

Vantagem: permite gerar changelog automático e decidir versionamento semântico só lendo as mensagens.

## merge --no-ff vs rebase
- **`git merge --no-ff`**: força a criação de um commit de merge, mesmo quando seria possível avançar direto. Preserva visualmente que aquele código nasceu numa branch separada. É a recomendação padrão do GitFlow.
- **`git rebase`**: reescreve o histórico, "replantando" os commits de uma branch em cima da ponta de outra — resultado linear, mas apaga o rastro de que era uma branch isolada.

## O código da semana (demonstração, não exercício)
- Um validador regex que checa se mensagens de commit seguem o padrão Conventional Commits.
- Uma simulação simplificada de resolução de conflito de merge (compara linha a linha entre `develop` e `feature`, mantendo o valor da feature onde diverge) — didática, não é como o Git resolve merges de verdade (que trabalha em blocos de diff).

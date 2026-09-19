# GitFlow — Conceitos e Perguntas de Fixação

## Conceitos

**Homologação:** fase do ciclo de vida do software onde uma versão está estável o suficiente para ser testada por analistas de QA, clientes ou usuários finais em um ambiente idêntico ao de produção, antes do lançamento oficial. No GitFlow, isso ocorre na branch de *release*.

**Versionamento (SemVer):** o GitFlow integra-se ao *Semantic Versioning* (MAJOR.MINOR.PATCH):

- **MAJOR:** quebras de compatibilidade (ex.: v2.0.0) — alteração estrutural na *main*.
- **MINOR:** novas funcionalidades compatíveis, criadas na *develop* e lançadas via *release* (ex.: v1.1.0).
- **PATCH:** correções de bugs críticos via *hotfix*, aplicadas diretamente sobre a *main* (ex.: v1.0.1).

**Pull Request (PR):** mecanismo de colaboração (usado em plataformas como GitHub, GitLab ou Bitbucket) onde um desenvolvedor propõe que as alterações de sua branch sejam integradas a outra. Serve como ponto de checagem para Code Review, execução de testes automatizados (CI) e discussão antes da mesclagem.

**Merge:** o ato de pegar o histórico de commits de uma branch e integrá-lo a outra.

---

## 1. O DAG do Git (Blob, Tree, Commit)

Utilizando conhecimentos gerais: acíclico é um tipo de metodologia onde retornar a etapas anteriores para correções e depois avançar é bastante comum — portanto, o DAG do Git deve funcionar no mesmo princípio, porém na forma de desenvolvimento do Git.

- **Blob:** só o conteúdo "cru" de um arquivo.
- **Tree:** funciona como uma pasta — mapeia nomes de arquivos para blobs (ou outras trees).
- **Commit:** aponta para uma Tree raiz + metadados do commit.

**Conceito de metadados:** autor, mensagem, data (período de envio), etc.

---

## 2. As cinco divisões (branches) do GitFlow

- **Main:** linha do tempo principal — base do funcionamento atual, de onde todas as ramificações para adições saem e para onde retornam ao estarem completas.
- **Hotfix:** ramificação da Main para reparo, que deve retornar tanto para a Main quanto para a Develop — corrigindo a produção e alertando a Develop.
- **Release:** nasce da Develop (criação da branch), recebe homologação (correção de bugs e testes) e, ao finalizar, retorna para a Main e para a Develop.
- **Develop:** recebe merges de features via pull requests, servindo de ponto de partida para a release, e recebe de volta os merges de hotfix e release.
- **Feature:** feature/funcionalidade A e feature/funcionalidade B nascem da Develop de maneira isolada, até a pull request.

---

## 3. Quando usar Hotfix e quando usar Release

Um problema crítico deve ser enviado ao *hotfix* e, ao terminar, deve retornar à Main e à Develop. Já atualizações padrão e/ou correções de bugs não críticos são feitas via *release*.

---

## 4. Diferencie `git merge --no-ff` de `git rebase`. Por que a flag `--no-ff` é a recomendação padrão do GitFlow para mesclagens na branch develop?

**`git merge --no-ff` (No Fast-Forward):** força a criação de um commit de merge explícito, em vez de permitir que o histórico seja simplesmente "adiantado" — como ilustrado nos gráficos do GitHub — mostrando claramente onde o trabalho começou, quais commits fizeram parte dele e onde foi integrado.

**`git rebase`:** reescreve o histórico. Pega os commits da sua branch de feature, desconecta-os do ponto de origem e os "aplica" um a um no topo da branch de destino.

**Por que `--no-ff` é recomendado?**

- **Rastreabilidade e contexto histórico:** o GitFlow prioriza saber exatamente quais commits formaram uma funcionalidade específica. Sem o `--no-ff`, se a develop não tivesse recebido novos commits enquanto a feature era desenvolvida, o Git faria um merge fast-forward, misturando os commits diretamente na develop, sem deixar rastro de que vieram de uma branch de feature.
- **Facilidade para reverter (rollback):** se a funcionalidade introduzir um erro grave, com o `--no-ff` é possível reverter o agrupamento inteiro desfazendo apenas o commit de merge, em vez de ter que reverter múltiplos commits individuais espalhados pelo histórico.

---

## Definições complementares

**DAG (Directed Acyclic Graph / Grafo Acíclico Dirigido) no Git:**

- **Dirigido:** as conexões (arestas) têm uma direção clara — cada commit aponta para trás, para o(s) seu(s) commit(s) pai(s).
- **Acíclico:** é impossível criar um ciclo. Nunca é possível navegar pelos commits pais e acabar voltando para o mesmo commit no futuro.
- **Função no Git:** garantir um histórico de alterações imutável e rastreável, permitindo que o Git saiba exatamente a "árvore genealógica" do projeto para realizar merges, ramificações (branches) e detecção de conflitos de forma eficiente.
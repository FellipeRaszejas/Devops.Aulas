# Semana 04 — Resumo: Prática Colaborativa de GitFlow e Resolução de Conflitos

Esta semana é prática: aplica no terminal tudo o que foi visto nas Semanas 02 e 03 (branches, merge --no-ff, Conventional Commits), com foco nos erros reais de trabalho em equipe.

## Repositório aninhado (erro antes de começar)
Clonar um repositório **dentro de outra pasta que já é um Git** confunde o Git sobre qual repositório controla os commits.
- Verificação: rode `git status` numa pasta neutra antes de clonar.
- `fatal: not a git repository` → seguro para clonar.
- `On branch main/master` → você já está dentro de outro repositório, suba um nível (`cd ..`).

## Fluxo completo de comandos
```
git clone → git checkout develop → git checkout -b feature/seu-nome
→ desenvolver e commitar → git checkout develop → git pull
→ git merge --no-ff feature/seu-nome → git push origin develop
```

## Fast-forward vs --no-ff (metáfora da fita)
- **Fast-forward** (padrão do Git): se a `develop` não mudou enquanto você trabalhava, o Git só "avança a fita" — parece que os commits foram feitos direto na develop, sem registro de que vieram de uma feature.
- **`--no-ff`**: força um commit de merge exclusivo, documentando claramente onde a feature começou e quando entrou na develop. É o padrão recomendado no GitFlow.

## Erro `[rejected - non-fast-forward]`
Acontece quando **outra pessoa fez push antes de você** na mesma branch remota. O remoto já tem commits que você não tem localmente.
- Solução: `git pull origin develop` antes de tentar o push de novo.

## Conflito de merge
Ocorre quando duas pessoas alteram a mesma linha do mesmo arquivo. O Git insere marcadores no arquivo:
```
<<<<<<< HEAD
sua versão local
=======
versão que veio do pull
>>>>>>> hash-do-commit
```
Resolução: editar manualmente (ou usar os botões do VS Code: Accept Current / Incoming / Both), remover os marcadores, depois `git add` → `git commit` → `git push`.

## Boas práticas finais
- Depois do merge, apague a branch de feature (local: `git branch -d`; remota: `git push origin --delete`).
- `git log --oneline --graph --decorate --all` mostra visualmente toda a árvore de commits e merges.

## Tabela de diagnóstico rápido
| Erro | Causa | Solução |
|---|---|---|
| `warning: adding embedded git repository` | Clone dentro de outro `.git` | Remover pasta, clonar em local neutro |
| `fatal: not a git repository` | Terminal fora da pasta do projeto | `cd NOME_DO_PROJETO` |
| `error: src refspec ... does not match` | Push sem nenhum commit local | `git add .` + `git commit` antes do push |
| `[rejected - non-fast-forward]` | Remoto tem commits novos | `git pull origin develop` |
| `Automatic merge failed` | Edição simultânea nas mesmas linhas | Resolver no editor, `git add`, `git commit`, `git push` |
| `refusing to merge unrelated histories` | Repositórios sem base comum | `git pull origin develop --allow-unrelated-histories` |

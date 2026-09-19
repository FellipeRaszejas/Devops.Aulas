# Semana 04 — Perguntas de Fixação

## 1. O que é um repositório aninhado e como você verifica, antes de clonar, se está numa pasta segura?

É um repositório com um `.git` já presente dentro de outra pasta. Verificamos utilizando um `git status` antes de clonar.

---

## 2. Descreva a sequência completa de comandos, do clone até o push final, para desenvolver uma feature isolada.

1. **Clone do repositório**
2. **Averiguação da versão:** `git checkout develop` e `git pull origin develop`
3. **Criação de uma branch isolada:** `git checkout -b feature/nome-da-feature`
4. **Desenvolvimento e registro das alterações:** `git add .` e `git commit -m "feat: adiciona funcionalidade X"`
5. **Publicação da branch remota:** `git push -u origin feature/nome-da-feature`

---

## 3. Depois de integrar uma feature com sucesso na `develop`, quais dois comandos você usaria para limpar a branch (local e remota)?

- **Excluir a branch localmente:** `git branch -d feature/nome-da-feature`
- **Excluir a branch do repositório remoto:** `git push origin --delete feature/nome-da-feature`

---

## 4. Para que serve o comando `git log --oneline --graph --decorate --all`?

Visualiza o histórico de commits em formato de gráfico no terminal.

- `--oneline`: resume cada commit em apenas uma linha.
- `--graph`: desenha um gráfico em arte ASCII.
- `--decorate`: exibe para onde os ponteiros das branches estão apontando.
- `--all`: mostra o histórico de todas as branches.
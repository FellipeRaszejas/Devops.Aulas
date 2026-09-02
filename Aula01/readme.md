# DevOps Turma Sesi — Painel de Tarefas

Aplicação web para gerenciamento e acompanhamento de tarefas de **Git Flow, Branches, Pull Requests e boas práticas de desenvolvimento** da turma N2S.

O projeto foi desenvolvido com **Python + Flask** e possui um painel visual para acompanhar o progresso individual e coletivo dos alunos.

## 🚀 Como executar

### Pré-requisitos

- Python 3.8 ou superior
- Flask

### 1. Verifique a instalação do Python

```bash
python --version
```

### 2. Instale o Flask

Na pasta do projeto, execute:

```bash
python -m pip install flask
```

### 3. Inicie o servidor

```bash
python app.py
```

### 4. Acesse o painel

Abra o navegador e acesse:

**http://127.0.0.1:5000**

---

## 📁 Estrutura do projeto

```text
Devops_N2S/
├── app.py             # Backend Flask, rotas, dados e API
├── progresso.json     # Progresso dos alunos (gerado automaticamente)
├── static/
│   └── style.css      # Estilos e tema visual da aplicação
├── templates/
│   ├── index.html     # Painel principal da turma
│   ├── tarefa.html    # Detalhes de cada tarefa
│   └── aluno.html     # Progresso individual do aluno
├── GitFlow.md         # Guia de instalação e utilização do Git Flow
└── README.md          # Documentação do projeto
```

---

## 📋 Tarefas

|   # | Tarefa                                         | Categoria     | Nível         |  Prazo |
| --: | ---------------------------------------------- | ------------- | ------------- | -----: |
|   1 | 🌿 Configurar Git Flow no repositório          | Git Flow      | Iniciante     | 2 dias |
|   2 | 🔀 Criar e desenvolver uma Feature Branch      | Branches      | Iniciante     | 3 dias |
|   3 | 🔒 Configurar Proteção de Branches no GitHub   | GitHub        | Intermediário |  1 dia |
|   4 | 👀 Realizar Code Review e aprovar Pull Request | Code Review   | Intermediário | 2 dias |
|   5 | ⚡ Resolver Conflito de Merge                  | Git Avançado  | Avançado      | 3 dias |
|   6 | 🚀 Criar Release e Tag de Versão               | Git Flow      | Intermediário | 3 dias |
|   7 | 👤 Configurar CODEOWNERS                       | GitHub        | Intermediário |  1 dia |
|   8 | ✍️ Aplicar Conventional Commits                | Boas Práticas | Iniciante     | 2 dias |

---

## ✨ Funcionalidades

O painel oferece:

- 📊 **Painel geral** com estatísticas da turma.
- ✅ Acompanhamento de tarefas concluídas.
- 🔄 Status de cada tarefa:
  - Pendente
  - Em andamento
  - Concluída

- 📈 Barra de progresso individual e coletiva.
- 🔎 Busca e filtro de alunos.
- 💾 Salvamento automático do progresso em `progresso.json`.
- 🔌 API REST para atualização dos status.
- 👤 Página de progresso individual de cada aluno.
- 📋 Página detalhada de cada tarefa.

---

## 🔗 Rotas disponíveis

| Método | Rota             | Descrição                                       |
| ------ | ---------------- | ----------------------------------------------- |
| `GET`  | `/`              | Exibe o painel principal com tarefas e alunos   |
| `GET`  | `/tarefa/<id>`   | Exibe os detalhes de uma tarefa                 |
| `GET`  | `/aluno/<nome>`  | Exibe o progresso individual do aluno           |
| `POST` | `/api/status`    | Atualiza o status de uma tarefa para um aluno   |
| `GET`  | `/api/progresso` | Retorna os dados completos de progresso em JSON |

---

## 📖 Git Flow

O projeto utiliza o conceito de **Git Flow** para organizar o desenvolvimento.

### Estrutura

```text
main
 │
 │ → versão estável / produção
 │
 └── develop
      │
      │ → integração do desenvolvimento
      │
      ├── feature/*   → novas funcionalidades
      ├── release/*   → preparação para produção
      └── hotfix/*    → correções urgentes em produção
```

### Fluxo de desenvolvimento

Cada aluno deve seguir o seguinte fluxo:

```bash
# 1. Atualizar a branch develop
git switch develop
git pull origin develop

# 2. Criar uma feature branch
git switch -c feature/minha-funcionalidade

# 3. Desenvolver e realizar commits

# 4. Enviar a branch para o GitHub
git push -u origin feature/minha-funcionalidade
```

Depois disso:

```text
feature/minha-funcionalidade
            │
            ▼
      Pull Request
            │
            ▼
        Code Review
            │
            ▼
      Aprovação do colega
            │
            ▼
      Merge → develop
```

---

## ✍️ Conventional Commits

Os commits devem seguir o padrão **Conventional Commits**.

| Tipo        | Utilização                                 |
| ----------- | ------------------------------------------ |
| `feat:`     | Nova funcionalidade                        |
| `fix:`      | Correção de bug                            |
| `docs:`     | Alteração na documentação                  |
| `chore:`    | Tarefa de manutenção                       |
| `refactor:` | Refatoração sem alteração de comportamento |
| `test:`     | Adição ou correção de testes               |

### Exemplos

```bash
git commit -m "feat: adiciona tela de progresso do aluno"
```

```bash
git commit -m "fix: corrige atualização do status da tarefa"
```

```bash
git commit -m "docs: atualiza instruções do Git Flow"
```

---

## ⚠️ Regras da turma

As seguintes regras devem ser respeitadas durante o desenvolvimento:

```text
NUNCA trabalhar diretamente na main.

NUNCA fazer push direto na main.

NUNCA fazer merge sem Pull Request.

Cada funcionalidade deve ter sua própria feature branch.

Todo Pull Request deve ser revisado por outra pessoa.
```

### Fluxo obrigatório

```text
develop
   │
   ▼
feature/*
   │
   ▼
Pull Request
   │
   ▼
Code Review
   │
   ▼
Aprovação
   │
   ▼
Merge → develop
```

---

## 🖥️ Tutorial rápido

### Verificar Python

```bash
python --version
```

### Instalar Flask

```bash
python -m pip install flask
```

### Executar a aplicação

```bash
python app.py
```

### Abrir no navegador

```text
http://127.0.0.1:5000
```

---

## 💾 Persistência dos dados

O progresso dos alunos é armazenado automaticamente no arquivo:

```text
progresso.json
```

Esse arquivo contém os dados utilizados pelo painel para acompanhar o status das tarefas.

> **Observação:** o arquivo `progresso.json` é gerado automaticamente pela aplicação e pode ser recriado caso ainda não exista.

---

## 🛠️ Tecnologias utilizadas

- 🐍 **Python**
- 🌐 **Flask**
- 🎨 **HTML5**
- 🎨 **CSS3**
- 🔀 **Git**
- 🐙 **GitHub**
- 🔌 **API REST**
- 📄 **JSON**

---

## 🎯 Objetivo do projeto

O **DevOps— Painel de Tarefas** tem como objetivo auxiliar no aprendizado prático de conceitos fundamentais de DevOps e Git, permitindo que a turma acompanhe visualmente a execução das atividades relacionadas a:

- Git Flow
- Branches
- Pull Requests
- Code Review
- Proteção de branches
- Resolução de conflitos
- Releases e tags
- CODEOWNERS
- Conventional Commits

---

## 📌 Status do projeto

**Em desenvolvimento 🚧**

Projeto desenvolvido para acompanhamento das atividades práticas da turma **N2S**.

# Perguntas de Fixação (Vercel, Webhooks e CI/CD)

## 1. Ambientes de Preview na Vercel

A Vercel cria automaticamente um ambiente isolado com uma URL única para cada pull request ou commit enviado para uma branch de funcionalidade (`feature/*`).

---

## 2. Diferença entre a branch `develop` e a branch `main`

Como vimos anteriormente, a *develop* é a versão da aplicação em produção que está sendo desenvolvida — coisas que o público geral não tem acesso, para evitar diversos problemas, como vazamento de informações e falhas técnicas em uma funcionalidade. Alterar a *develop* é um processo comum; porém, alterar a branch *main* é basicamente uma das etapas para colocar a aplicação no ar — logo, ela deve estar 100% funcional.

---

## 3. O que são Webhooks?

Webhooks são o mecanismo que conecta duas plataformas diferentes.

**Exemplo:** GitHub e Vercel.

Quando ocorre um novo commit, é enviada uma requisição de webhook para realizar as alterações na plataforma, onde a Vercel instala as dependências, compila a aplicação, etc.

---

## 4. Sequência de comandos conhecida (fluxo de correção de bug)

Na branch local `feature/novo-menu`, o desenvolvedor ajusta o código para corrigir o problema visual encontrado.

1. `git add .` e `git commit -m "fix: ajusta alinhamento do novo menu"` — registra as mudanças no Git com uma mensagem explicativa.
2. `git push origin feature/novo-menu` — envia o novo commit para a branch remota no GitHub.
3. O GitHub dispara automaticamente o webhook para a Vercel, que inicia uma nova compilação e atualiza a mesma Preview URL do pull request existente, de forma transparente.

---

## Refinamentos (IA)

**Publish na branch `develop` (Staging / Pré-Produção):** gera uma implantação no ambiente de Preview/Staging. É usada para testes de integração de toda a equipe antes do lançamento oficial.

**Publish na branch `main` (Production):** a Vercel reconhece a branch `main` como a *Production Branch*. Ao receber um commit ou merge, a Vercel atualiza automaticamente o ambiente de produção oficial (substituindo a versão que os usuários finais estão acessando).

### Detalhamento da sequência de eventos

1. **Disparo do evento:** o desenvolvedor faz um `git push` para o GitHub em um PR aberto.
2. **Notificação (Webhook):** o GitHub envia uma requisição HTTP do tipo `POST` (o webhook) para o endpoint da Vercel, contendo os metadados do repositório, da branch e do commit.
3. **Execução na Vercel (pipeline de CI/CD):**
   - A Vercel clona o código do commit.
   - Instala as dependências (`npm install` / `yarn`).
   - Compila a aplicação (*build*).
   - Roda verificações estáticas.
   - Gera uma nova URL única de Preview e envia um comentário ou *status check* de volta para a tela do pull request no GitHub.
# Semana 05 — Perguntas de Fixação

## 1. O que diferencia um teste de integração de um teste E2E? Dê um exemplo de cada.

**Teste de Integração:** valida se dois ou mais módulos/componentes do sistema interagem corretamente entre si (ex.: testar se a camada de serviço consegue salvar e buscar dados em um repositório ou banco de dados SQLite em memória).

**Teste E2E (End-to-End):** valida o fluxo completo do usuário, do início ao fim, simulando o ambiente de produção real (ex.: abrir o navegador *headless* com Selenium/Cypress, fazer login na tela, adicionar um produto ao carrinho e finalizar a compra).

---

## 2. Explique o anti-padrão da "Ampulheta" e por que ele é diferente do Cone de Sorvete.

A Ampulheta é mais otimizada que o Cone, porém ainda fica atrás em relação ao seu custo, que se torna elevado por haver bugs nas camadas de comunicação dos módulos.

> **Extra (IA):** a Ampulheta tem uma base razoável de testes unitários e um topo pesado de testes E2E/manuais, mas a camada intermediária (testes de integração) é quase inexistente ou negligenciada.

---

## 3. Qual a diferença entre um Stub e um Mock?

São parecidos: ambos são dados projetados para testes. Porém o Mock contém registros, como o de movimentação, ajudando a ter, além de uma simulação dos dados, um monitoramento das interações.

---

## 4. Por que 100% de cobertura de código não garante que o software está livre de bugs?

Porque a lógica por trás do código pode estar correta, mas não ser o que deveria ser feito — um bug é uma falha em atender à necessidade real, mesmo que o código esteja "funcionando" tecnicamente. Por isso, é preciso reajuste e avaliação de como o sistema está interpretando os requisitos.

---

## 5. O que é um Quality Gate e o que acontece quando um Pull Request não atende aos critérios definidos?

É uma regra automática no pipeline de CI que bloqueia o merge de um pull request.

> **O que acontece quando o PR falha no Quality Gate (IA):**
>
> - O job do pipeline de CI falha (retorna *exit code* diferente de zero).
> - O GitHub/GitLab marca o pull request com o status vermelho (❌).
> - Se houver regras de proteção de branch ativadas, o botão de merge é bloqueado, impedindo que código fora dos padrões de qualidade (ex.: sem testes, com cobertura baixa ou com falhas de segurança) chegue à branch `develop` ou `main`.
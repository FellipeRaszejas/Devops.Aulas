# Perguntas de Fixação (Testes Automatizados e CI/CD)

## 1. Por que testar a aplicação em partes, em vez de validar tudo por completo a cada mudança?

A aplicação está em constante desenvolvimento e melhoria, e quando algo já está "redondo" (funcionando do começo ao fim), não seria necessário testá-lo novamente ao testar outra parte da aplicação. Agora imagine, a cada implementação, fazer uma validação do sistema por completo, linha por linha, sendo que diversas partes seriam reavaliadas e trariam o mesmo resultado — isso seria extremamente demorado, complexo, caro e desnecessário. Pegar trechos específicos para testar a parte, ir evoluindo constantemente e, no final, testar a aplicação completa é a forma ideal de se fazer.

---

## 2. Como é o padrão de testes de um projeto "cru" (sem maturidade em testes)?

O padrão "cru" é quase manual: utiliza poucos testes unitários e quase nenhuma automação, fazendo com que a descoberta de bugs seja bem demorada.

---

## 3. Por que não conectar a um Banco de Dados/Broker real no CI?

Questão de segurança: dados falsos, que podem sofrer alterações e até ser corrompidos (dependendo da falha), são muito mais práticos e simples de usar do que dados reais — além de não fazer diferença, evitando o cuidado que seria necessário para não vazar dados reais.

> **Resposta mais adequada (IA):** a resposta acima faz sentido e está correta, mas seria mais um complemento do que a resposta exata. Os motivos principais para não conectar a um banco/broker real no CI são:
>
> - **Determinismo e isolamento:** testes em rede tornam-se não determinísticos. Se o banco oscilar ou cair, o teste falha sem que o código esteja com defeito.
> - **Performance:** conexões de rede e operações de E/S (I/O) no banco deixam os testes infinitamente mais lentos.
> - **Poluição de estado:** testes concorrentes alterando o mesmo banco de dados criam "condições de corrida" (*race conditions*), em que um teste apaga os dados que outro teste estava usando.
> - **Insegurança de credenciais:** seria necessário injetar segredos (tokens/senhas) do banco no ambiente de CI para cada job.

---

## 4. Como validar uma cobertura mínima de testes no CI?

Utiliza-se a flag `--cov-fail-under`, fornecida pelo plugin `pytest-cov`.

**Exemplo de arquivo de workflow (sugerido por IA):**

```yaml
name: Continuous Integration

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main, develop ]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout do código
        uses: actions/checkout@v4

      - name: Configurar Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'

      - name: Instalar dependências
        run: |
          python -m pip install --upgrade pip
          pip install pytest pytest-cov
          if [ -f requirements.txt ]; then pip install -r requirements.txt; fi

      - name: Executar testes com validação de cobertura mínima (85%)
        run: |
          pytest --cov=src --cov-fail-under=85
```

**Funcionamento:**

- `--cov=src`: indica qual diretório/módulo do projeto deve ser monitorado para a medição da cobertura de código (substitua `src` pela pasta principal do seu código-fonte).
- `--cov-fail-under=85`: define a regra de bloqueio. O pytest calcula a porcentagem total de cobertura ao término da execução; se o resultado for inferior a 85%, ele retorna o código de saída 1 (*exit code* 1).

**Comportamento no GitHub Actions:** quando qualquer passo (*step*) de um job retorna um código de saída diferente de 0, o runner do GitHub interpreta o passo como falho. O job é interrompido com status vermelho (❌), bloqueando a mesclagem do pull request, caso haja proteção de branch ativada.

> **Extra (IA) — refinamento com foco em três fatores:**
>
> - **Velocidade de execução:** testes unitários rodam na memória em milissegundos. Testes E2E dependem da subida de servidores, navegação em tela ou chamadas de rede, levando minutos ou horas.
> - **Custo de manutenção:** testes E2E são extremamente "quebradiços" (*flaky*) — qualquer mudança sutil de layout ou na interface quebra o teste, exigindo manutenção constante. Testes unitários dependem apenas do contrato do código e mudam pouco.
> - **Isolamento de falhas:** quando um teste unitário falha, você sabe a classe e a linha exata do erro. Se um teste E2E falha, a causa raiz pode estar no front-end, na API, na rede ou no banco de dados, tornando o diagnóstico demorado.
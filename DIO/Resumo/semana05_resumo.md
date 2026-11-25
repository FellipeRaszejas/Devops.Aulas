
# Semana 05 — Resumo: Estratégias de Testes, Pirâmide de Testes e Quality Gates

## A Pirâmide de Testes
Modelo de Mike Cohn / Martin Fowler que orienta a distribuição ideal de testes automatizados:

| Camada | Proporção | Escopo | Velocidade | Custo |
|---|---|---|---|---|
| **Unitários** (base) | ~70% | Função/classe isolada | Milissegundos | Baixo |
| **Integração** (meio) | ~20% | Interação entre módulos/APIs/DB | Segundos | Médio |
| **E2E** (topo) | ~10% | Fluxo completo do usuário | Minutos | Alto |

Lógica: quanto mais embaixo na pirâmide, mais barato e rápido é detectar e localizar um bug. Por isso a base deve ser a maior camada.

## Detalhamento das camadas
- **Testes Unitários**: isolamento estrito — nunca fazem chamada de rede, banco de dados ou disco. Permitem diagnóstico exato do ponto de falha e viabilizam TDD.
- **Testes de Integração**: validam se a comunicação entre componentes (rotas HTTP, ORM, mensageria) segue o contrato esperado.
- **Testes E2E**: simulam a jornada completa do usuário (UI → backend → banco real). Caros, lentos e propensos a *flaky tests* (falhas intermitentes sem defeito real no código).

## Anti-padrões
- **Cone de sorvete**: quase nenhum unitário/integração, testes E2E/manuais em excesso → CI lento, feedback tardio, bugs só descobertos em produção.
- **Ampulheta**: muito unitário e muito E2E, mas sem integração → erros de comunicação entre módulos só aparecem no E2E, difíceis de depurar.

## Duplos de Teste
- **Stub**: resposta fixa e pré-programada para uma dependência externa (ex: sensor sempre retorna 25°).
- **Mock**: além de responder, registra se/quantas vezes/com quais parâmetros foi chamado.
- **Fixture** (Pytest): prepara o ambiente antes do teste e faz a limpeza depois.

## Cobertura de Código
- **Statement Coverage**: % de linhas executadas.
- **Branch Coverage**: % de caminhos condicionais (`if/else`) testados.

Importante: alta cobertura **não garante qualidade** — uma linha pode "rodar" sem que o teste valide de verdade o resultado esperado.

## Quality Gate
Barreira automatizada no CI: se o PR não atinge os critérios mínimos (ex: 0 testes falhando + cobertura ≥ 80%), o pipeline falha e o merge é bloqueado.

```
PR aberto → CI roda (testes + cobertura + linter) → critérios do gate
  ├── Aprovado → merge liberado
  └── Reprovado → build bloqueado
```

## O código da semana (demonstração)
Simula um sistema de controle de produção industrial com:
1. Testes unitários na classe `OrdemProducao` (cálculos e validações de regra de negócio).
2. Testes de integração usando um repositório **mock** (dicionário em memória) no lugar de um banco real.
3. Um `avaliar_quality_gate` que junta os resultados + uma cobertura simulada e decide se o "PR" seria aprovado ou bloqueado.

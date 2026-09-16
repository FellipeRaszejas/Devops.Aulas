# Semana 01 — Resumo: Fundamentos de DevOps, CALMS e Fluxo de Valor

## Por que o DevOps existe
Antes do DevOps, Dev (foco em entregar features) e Ops (foco em estabilidade) trabalhavam como times rivais, separados pelo **"Wall of Confusion"**. Isso gerava deploys raros, arriscados e culpa cruzada quando algo quebrava.

**DevOps** não é ferramenta nem cargo — é uma filosofia de **responsabilidade compartilhada** por todo o ciclo de vida do software (código até produção).

## CALMS — os 5 pilares
| Pilar | Ideia central |
|---|---|
| **C**ulture | Colaboração, confiança, post-mortems **sem culpa** (foco no processo, não na pessoa) |
| **A**utomation | Automatizar build, testes, infra e deploy; eliminar trabalho manual repetitivo (*toil*) |
| **L**ean | Lotes pequenos, reduzir **WIP** (trabalho em progresso simultâneo), eliminar gargalos |
| **M**easurement | Decisões guiadas por dados reais (ciclo, latência, erros) |
| **S**haring | Transparência total de conhecimento e ferramentas entre times |

## Value Stream Mapping (VSM)
- **Process Time**: tempo em que alguém está de fato trabalhando na tarefa.
- **Lead Time**: tempo total, incluindo esperas em fila (aprovação, revisão parada, fila de QA).

$$\text{Eficiência} = \frac{\sum \text{Process Time}}{\text{Lead Time Total}} \times 100\%$$

O gargalo quase nunca é a velocidade de quem programa — geralmente são as **esperas manuais entre etapas**. O objetivo do DevOps é automatizar essas esperas.

## As 4 Métricas DORA
Duas de **velocidade** e duas de **qualidade** (de propósito, para não otimizar uma às custas da outra):

- **Deployment Frequency**: com que frequência você entrega em produção.
- **Lead Time for Changes**: tempo do commit até rodar em produção.
- **Change Failure Rate (CFR)**: % de deploys que quebram algo.
- **MTTR**: tempo médio para restaurar o serviço após uma falha.

Faixa "Elite": múltiplos deploys/dia, lead time < 1h, CFR até 15%, MTTR < 1h.

## O script Python da semana
Recebe um histórico de deploys (commit, deploy, sucesso/falha, tempo de recuperação, tempo de processo/espera) e calcula automaticamente: frequência de deploy, lead time médio, CFR, MTTR, eficiência do fluxo e classifica o time como "ELITE" ou "ALTO/MÉDIO".

## Glossário rápido
- **QA (Quality Assurance)**: time/etapa dedicada a testar a qualidade do software antes de ir para produção.
- **Post-mortem blameless**: análise pós-incidente focada em melhorar o processo, não em punir pessoas.
- **WIP**: quantidade de tarefas sendo trabalhadas ao mesmo tempo (sem terminar).

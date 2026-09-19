# Perguntas de Fixação (CALMS e Métricas DORA)

## 1. Por que separar desenvolvimento e operação (funcionamento) cria barreiras, e como o CALMS resolve isso?

Ao deixar o desenvolvimento e o funcionamento separados, isso criava uma barreira para qualquer tipo de atualização, pois frequentemente seriam necessárias correções em uma implementação. O modelo CALMS elimina esse conflito unindo os dois em um só, utilizando uma metodologia que entra em um loop contínuo — da finalização de uma entrega até a próxima.

---

## 2. Qual a diferença entre Process Time e Lead Time? Programar mais rápido reduz o Lead Time?

**Process Time** é o tempo que se leva para desenvolver alguma coisa — sendo ele um pedaço do Lead Time.

**Lead Time** é o tempo total de desenvolvimento, incluindo tempos de espera, como revisão, Quality Analytics (QA), etc.

Programar mais rápido não interfere necessariamente no Lead Time, porque, desenvolvendo mais rápido, também seriam feitas mais entregas — logo, haveria mais itens para avaliar no Lead Time, que passariam pelo mesmo tempo de espera.

---

## 3. Qual o risco de a equipe focar só na velocidade de desenvolvimento?

Se a equipe focasse só no desenvolvimento rápido, poderia acabar passando por diversos bugs ou retrabalho — trabalhando em dobro em algo e levando o projeto à ruína.

---

## Métricas DORA

### Velocidade

| Métrica | Definição |
|---|---|
| **Deployment Frequency** | Com que frequência você entrega em produção |
| **Lead Time for Changes** | Tempo do commit até estar rodando em produção |

### Qualidade

| Métrica | Definição |
|---|---|
| **Change Failure Rate** | Porcentagem de deploys que quebram algo |
| **MTTR** | Tempo médio de serviço para restauração após a falha |

---

## 4. Cálculo do Change Failure Rate

**❌ Errado:** 2h / 30h (= 45min × 40 dias) → 4%

**✅ Certo:** Número de falhas / Número de deploys
= 4 / 40 = **10%**

---

## Melhorias (explicação de IA)

### CALMS: elimina o conflito alinhando ambos os lados com objetivos compartilhados

- **Culture** — cultura de responsabilidade compartilhada
- **Automation** — automação de testes e deploys
- **Lean** — entrega em pequenos lotes
- **Measurement** — métricas visíveis para todos
- **Sharing** — compartilhamento de conhecimento e fracassos

### Métricas de Velocidade (Rendimento)
Deployment Frequency (frequência de deploys) e Lead Time for Changes (tempo do commit ao deploy).

### Métricas de Qualidade (Estabilidade)
Change Failure Rate (porcentagem de deploys que causam falhas) e MTTR (tempo médio para restaurar o serviço).

### Risco da Velocidade Sem Qualidade
Implantar software rapidamente sem automação de testes ou validação contínua gera um alto Change Failure Rate. Isso interrompe o serviço para os clientes, degrada a confiança na marca e força a equipe a interromper novos desenvolvimentos para apagar incêndios (*firefighting*).

---

## Nota: valores no contexto do que foi pedido

**Mapeamento das Métricas da Equipe**

| Métrica | Valor |
|---|---|
| Deployment Frequency | 40 deploys no mês → ~10 deploys por semana (mais de 1 por dia) |
| Lead Time for Changes | 45 minutos |
| MTTR (Mean Time to Recovery) | 30 minutos |
| Change Failure Rate (CFR) | 10% |

### Tabela — Maturidade DORA

| Métrica | Dado da Equipe | Nível DORA Correspondente |
|---|---|---|
| Deployment Frequency | ~1 vez ao dia | Elite / High (Elite: múltiplos por dia; High: entre 1x/dia e 1x/semana) |
| Lead Time for Changes | 45 minutos (< 1 hora) | Elite (< 1 hora) |
| MTTR | 30 minutos (< 1 hora) | Elite (< 1 hora) |
| Change Failure Rate | 10% (faixa de 0%–15%) | Elite / High |
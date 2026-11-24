# Evolução do Desenvolvimento de Software

Este guia apresenta, de forma didática, como as práticas de desenvolvimento de software evoluíram. Cada etapa surgiu para resolver um **gargalo** da anterior, por isso entender a sequência ajuda a entender o porquê de cada método.

![Evolução do desenvolvimento de software](evolucao.png)

## Sumário

- [1. Waterfall](#1-waterfall)
- [2. Agile](#2-agile)
- [3. Lean](#3-lean)
- [4. Continuous Integration (CI)](#4-continuous-integration-ci)
- [5. Continuous Delivery (CD)](#5-continuous-delivery-cd)
- [6. Continuous Deployment (CD)](#6-continuous-deployment-cd)
- [7. Continuous Operations](#7-continuous-operations)
- [Resumo](#resumo)

## 1. Waterfall

**O que é:** metodologia tradicional e sequencial. Cada etapa do ciclo de vida do software (Requisitos → Design → Implementação → Testes → Implantação → Manutenção) só começa quando a anterior termina por completo.

**Na prática:** exige planejamento exaustivo antes de escrever código. O cliente só vê o produto funcionando no final, que pode levar meses ou anos.

**Gargalo que gerou a evolução:** baixíssima adaptabilidade a mudanças. Um erro de requisito descoberto nos testes custava caro e demorava para ser corrigido. Além disso, surgia o **"muro da confusão"**: os desenvolvedores entregavam o código pronto para a equipe de operações colocar no ar, sem comunicação entre os dois lados.

## 2. Agile

**O que é:** resposta direta à rigidez do Waterfall. Quebra o desenvolvimento em **ciclos curtos e iterativos**, chamados de **Sprints**, geralmente de 1 a 4 semanas. Os métodos mais conhecidos são Scrum, Kanban e XP.

**Na prática:** ao final de cada ciclo, entrega-se um **incremento funcional** do software. O foco está na colaboração constante com o cliente e na adaptação rápida a mudanças de escopo.

**Gargalo que gerou a evolução:** o Agile acelerou muito a escrita de código, mas não resolveu a entrega em produção. O código ficava "pronto" no ambiente de desenvolvimento, mas esbarrava na lentidão dos testes manuais e da infraestrutura tradicional.

## 3. Lean

**O que é:** filosofia originada no Sistema Toyota de Produção e adaptada para software (Lean Software Development). Seu foco central é **maximizar o valor entregue ao cliente** e **eliminar desperdícios**, conhecidos pelo termo japonês *Muda*.

**Na prática:** identifica e corta tudo o que não agrega valor direto, como:

- código desnecessário;
- burocracia excessiva;
- filas de espera entre equipes;
- retrabalho causado por defeitos;
- troca constante de contexto.

Introduz também o conceito de **fluxo contínuo** e de **trabalho em lotes pequenos** (*small batches*).

**Gargalo que gerou a evolução:** preparou a mentalidade de fluxo enxuto, mas precisava de **automação técnica pesada** para sustentar entregas pequenas e frequentes sem erro humano.

## 4. Continuous Integration (CI)

**O que é:** prática de engenharia em que os desenvolvedores integram suas alterações de código em um **repositório central compartilhado** várias vezes ao dia.

**Na prática:** cada *push* ou *Pull Request* dispara automaticamente um **pipeline** (por exemplo, GitHub Actions, GitLab CI ou Jenkins) que:

1. compila ou faz o *build* da aplicação;
2. executa baterias de testes automatizados (unitários e de integração);
3. verifica a qualidade e a segurança do código (linters e análise estática).

**Gargalo que gerou a evolução:** garante que a branch principal nunca fique "quebrada" e elimina o caos de juntar meses de código de vários desenvolvedores, conhecido como **merge hell**. Porém, o pacote gerado ainda precisa ser levado até os servidores.

## 5. Continuous Delivery (CD)

**O que é:** extensão direta do CI. Garante que todo código aprovado nos testes automatizados seja empacotado (por exemplo, como imagem Docker ou artefato `.jar`) e esteja **sempre pronto para ir para produção** a qualquer momento.

**Na prática:** o pipeline automatiza o deploy em ambientes de **homologação (staging)** e executa testes de aceitação e testes ponta a ponta (E2E). A ida final para produção, porém, **exige aprovação manual**, um clique de uma pessoa, geralmente por decisão de negócio ou por janela de manutenção.

## 6. Continuous Deployment (CD)

**O que é:** o passo seguinte à Entrega Contínua, que **remove a intervenção humana** no final.

**Na prática:** toda alteração que passa por todas as etapas automatizadas do pipeline (build, testes unitários, integração, segurança e staging) é publicada **automaticamente em produção**, sem aprovação manual.

**Requisitos essenciais:**

- cobertura de testes automatizados extremamente confiável;
- **infraestrutura como código (IaC)**;
- estratégias de deploy seguro, como **Blue-Green** ou **Canary Release**, para reverter falhas instantaneamente caso algo passe pelos testes.

## 7. Continuous Operations

**O que é:** representada pelo robô na imagem, simboliza a **automação completa do ciclo de vida do sistema após o deploy**, garantindo disponibilidade, resiliência e manutenção **sem tempo de inatividade** (*zero downtime*).

**Na prática:** envolve a gestão autônoma e proativa da infraestrutura em produção:

- **Observabilidade:** monitoramento contínuo de métricas, logs e traces (por exemplo, Prometheus, Grafana e OpenTelemetry).
- **Auto-escalonamento e auto-recuperação (*self-healing*):** orquestradores como o Kubernetes reiniciam contêineres com falha e escalam recursos conforme o tráfego sobe ou desce.
- **Segurança e patching contínuos:** atualizações de sistema, certificados e políticas de segurança aplicadas sem derrubar o serviço para o usuário final.

## Resumo

Cada etapa resolveu um gargalo da anterior:

| Etapa | Foco principal | Gargalo que resolveu |
|---|---|---|
| Waterfall | Planejamento sequencial | Rigidez e custo alto de correções |
| Agile | Ciclos curtos e colaboração | Lentidão na escrita de código |
| Lean | Eliminar desperdícios | Falta de fluxo contínuo e entregas pequenas |
| Continuous Integration | Integrar código com frequência | Caos de merge e código quebrado |
| Continuous Delivery | Código sempre pronto para produção | Deploy manual e demorado |
| Continuous Deployment | Publicação automática | Intervenção humana na produção |
| Continuous Operations | Operação automatizada | Falhas e indisponibilidade em produção |

**Pontos principais:**

- O **Waterfall** é sequencial e pouco adaptável.
- O **Agile** entrega em ciclos curtos (Sprints).
- O **Lean** foca em eliminar desperdícios e trabalhar em lotes pequenos.
- O **CI** integra e testa o código com frequência.
- O **CD** (Entrega) deixa o código pronto para produção, com aprovação manual.
- O **CD** (Implantação) publica automaticamente em produção.
- O **Continuous Operations** cuida da operação com monitoramento, auto-recuperação e segurança contínuos.
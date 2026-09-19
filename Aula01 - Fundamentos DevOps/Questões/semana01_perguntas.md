# Semana 01 — Perguntas de Fixação

*Responda com suas próprias palavras, sem consultar o resumo. Se travar em alguma, é sinal de que vale revisar aquele ponto.*

## 1. Por que um post-mortem "sem culpa" (*blameless*) é considerado mais eficaz do que um post-mortem tradicional que busca um responsável?

Aparentemente, no método clássico o dev recebia algum tipo de advertência por quebrar a aplicação, enquanto atualmente ele serve apenas para melhorar a própria aplicação, sem julgar quem desenvolveu e teve erros no sistema.

> **Melhoria (IA):** no modelo tradicional, buscar um culpado gera medo de punição, fazendo com que a equipe esconda erros ou evite reportar falhas precocemente. No modelo *blameless*, assume-se que as pessoas agiram com a melhor intenção, com os recursos que tinham. O foco muda de "Quem errou?" para "Por que o sistema/processo permitiu que esse erro acontecesse e chegasse à produção?". Isso cria transparência e aprendizado contínuo.

---

## 2. Por que, segundo o DevOps, reduzir o WIP (trabalho em progresso) tende a acelerar a entrega, mesmo que pareça contraintuitivo (fazer menos coisas ao mesmo tempo)?

Porque facilita as validações e o funcionamento, acelerando essa etapa; já tendo uma base funcional, adicionar as melhorias torna-se mais rápido.

> **Melhoria (IA):** fazer muitas coisas ao mesmo tempo aumenta a troca de contexto (*context switching*), o que gera perda de tempo, aumento de erros e criação de filas/gargalos. Ao reduzir o WIP:
> - O trabalho flui mais rápido pelo pipeline (menor tempo de ciclo).
> - A detecção de bugs é imediata (mais fácil identificar o erro num lote pequeno).
> - Evita-se o acúmulo de trabalho pela metade (*Work in Progress* é inventário parado que não gera valor).

---

## 7. Por que um time que otimiza só a Deployment Frequency, sem olhar para o Change Failure Rate, corre risco?

Relembrando: o Change Failure Rate mostra quantos por cento do sistema já em deploy quebra algum funcionamento. Se um programador ficar desenvolvendo de forma rápida sem validar adequadamente, corre-se um alto risco de algum bug no software.

---

## 8. O que significa a sigla QA e qual o papel dela no fluxo de valor?

**QA = Quality Assurance** (Analista/Garantia de Qualidade).

O papel moderno do QA é construir a cultura de qualidade ao longo de todo o processo, ajudando o time a definir e automatizar testes desde o início (*Shift-Left Testing*), identificando brechas de segurança ou de funcionamento para relatar e enviar aos desenvolvedores para correção do problema.
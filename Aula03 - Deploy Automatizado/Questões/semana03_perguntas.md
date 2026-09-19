# Semana 03 — Perguntas de Fixação

## 1. Qual ambiente é gerado quando você faz push numa branch `feature/*`, e qual sua finalidade?

**Preview Deployment** (ambiente de preview isolado, com uma URL única).

**Finalidade:** permitir que desenvolvedores, QA e revisores de código testem e validem aquela funcionalidade específica em um ambiente real na nuvem, antes de fazer o merge. O ambiente de *develop* (Staging) só é atualizado depois que o pull request é aprovado e mesclado.

---

## 5. Para que servem os comandos `vercel` e `vercel --prod`, e quando você usaria cada um?

- `vercel`: gera um deploy de preview.
- `vercel --prod`: força um deploy em produção.

---

## 6. No script de simulação da semana, como o programa decide se um deploy é "produção", "staging" ou "preview"?

- Branch `main` → publica em **Produção**.
- Branch `develop` → publica em **Staging** (pré-produção).
- Qualquer outra branch (`feature/*`, `hotfix/*`) → publica como **Preview**.
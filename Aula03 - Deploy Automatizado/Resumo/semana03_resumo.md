# Semana 03 — Resumo: GitFlow + Deploy Automatizado no Vercel

## A ideia central
Cada branch do GitFlow passa a corresponder automaticamente a um **ambiente publicado**, sem nenhum passo manual de deploy:

| Branch | Ambiente | Comportamento |
|---|---|---|
| `feature/*` | Preview efêmero | URL única por push, só para quem testa aquela feature |
| `develop` | Staging/Homologação | URL fixa, atualizada a cada merge de feature aprovada |
| `main` | Produção oficial | URL de produção, atualizada só ao final de release ou hotfix, com zero downtime |

## Webhooks — a mecânica por trás
1. Dev roda `git push` numa branch.
2. O GitHub recebe o commit.
3. O GitHub dispara um **webhook** (requisição HTTP POST com JSON) para o Vercel.
4. O Vercel instala dependências, compila a aplicação e gera a URL.
5. O status do build volta para o GitHub e aparece como check no Pull Request.

**Webhook** é o mecanismo geral que conecta duas plataformas diferentes (controle de versão e infraestrutura de deploy) sem intervenção humana — conceito central de CI/CD.

## Vercel CLI (uso opcional via terminal)
```bash
npm install -g vercel
vercel          # deploy de Preview
vercel --prod   # deploy direto em produção
```

## O código da semana (demonstração)
Simula o que o Vercel faz ao receber um webhook: dado um evento com branch + commit, decide a categoria do deploy só pelo nome da branch —
`main` → produção, `develop` → staging, qualquer outra coisa → preview (com URL montada a partir do nome da branch + hash do commit).

## Conectando com a Semana 02
O fluxo de branches (feature → develop → main) continua o mesmo do GitFlow puro — a novidade é que agora cada merge/push dispara automaticamente uma publicação real, sem comando manual de deploy.

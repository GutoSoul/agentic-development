# Workflow — Spec-Driven Development

Este projeto segue um pipeline rígido de 4 etapas. **Pular etapa é anti-padrão** (ver [anti-patterns.md](anti-patterns.md)).

## Pipeline

```
Briefing    →  /spec        →  specs/<slug>.md
SPEC        →  /plan        →  plans/<slug>.md
Task        →  /tech-spec   →  tech-specs/<slug>__<TASK_ID>.md
Tech Spec   →  /code        →  invocação explícita do agente coder → código + PR
```

## Responsabilidade de cada etapa

| Etapa | Responde | **Não** responde |
|---|---|---|
| **SPEC** | Qual problema? Para quem? Como sabemos que funcionou? | Como implementar |
| **Plano** | Quais tasks? Em que ordem? O que é MVP? | Stack, schema, endpoints |
| **Tech Spec** | Como implementar **esta** task? Contratos? Trade-offs? | Horas/prazos |
| **Código** | Executar a Tech Spec sem desviar | Redefinir escopo |

## Gatilhos disponíveis

| Comando | Skill ativada | Saída |
|---|---|---|
| `/spec` | `spec-creator` | `specs/<slug>.md` |
| `/plan` | `task-planner` | `plans/<slug>.md` |
| `/tech-spec` | `tech-spec-creator` | `tech-specs/<slug>__<TASK_ID>.md` |
| `/code` | — (invoca agente coder) | handoff explícito para agente definido em `agents/` |

## Agentes de execução disponíveis

Definidos em `agents/`:

- [preencher ou remover: `react-coder`, `vue-coder`, `tester`]

## Princípio

> **Skills pensam junto; agentes executam.**
> Toda decisão de produto e arquitetura passa por skill no contexto principal, com você no loop.
> Toda execução pesada (código, browser real) vai para agente isolado.

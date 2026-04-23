---
description: Invoca o agente de código apropriado para executar uma Tech Spec. Handoff explícito, com confirmação.
argument-hint: "[tech-specs/<slug>__<TASK_ID>.md]"
---

Você foi invocado via `/code`. Este comando **não** é magia — ele é um handoff controlado da Tech Spec para o agente de código.

**Argumento recebido:** $ARGUMENTS

## O que fazer (em ordem, sem pular passos)

### 1. Localizar a Tech Spec

- Se `$ARGUMENTS` for um caminho existente em `tech-specs/` → prossiga.
- Se vazio → liste os arquivos em `tech-specs/` e pergunte ao usuário qual.
- Se apontar para arquivo que **não existe** → informe e sugira rodar `/tech-spec` antes. **Não invente conteúdo.**

### 2. Validar prontidão

Leia a Tech Spec e confirme que o checklist **"Pronto para codar?"** está **todo marcado**. Se houver item pendente:

- **Pare imediatamente.**
- Mostre quais itens não estão atendidos.
- Oriente o usuário a voltar ao `/tech-spec` para completar. **Não prossiga.**

### 3. Determinar o agente correto

Consulte em ordem:

1. **Stack declarada em `rules/stack.md`** (ex: React → `react-coder`, Vue → `vue-coder`).
2. **Agentes disponíveis em `agents/`** (ou `.claude/agents/` do projeto real).
3. Se ambíguo → **pergunte ao usuário via `AskUserQuestion`** com as opções disponíveis. Não adivinhe.

### 4. Resumo explícito antes de invocar

Apresente ao usuário, **antes de fazer qualquer chamada ao `Task` tool**:

```
Prestes a invocar:

  Agente:      react-coder
  Tech Spec:   tech-specs/checkout-v2__T01.md
  Task:        T01 — Cancelar pedido com confirmação
  Plano de implementação (da Tech Spec):
    1. Criar schema Zod cancel.schema.ts
    2. Criar hook useCancelOrderMutation (+ testes)
    3. Criar <CancelOrderDialog /> (+ testes)
    4. Integrar no <OrdersTable />
    5. Cobrir erro 409 (já cancelado)
    6. Revisar acessibilidade

  Briefing que o agente vai receber:
    "Execute a Tech Spec em tech-specs/checkout-v2__T01.md.
     Respeite integralmente as convenções em CLAUDE.md + rules/.
     Siga a sequência do Plano de implementação.
     Gere testes para cada passo. Pare se encontrar ambiguidade — não adivinhe."

Confirmar invocação?
```

Use `AskUserQuestion` para a confirmação final. Opções: `Sim, invocar agora` / `Não, quero ajustar algo`.

### 5. Só então invocar

**Apenas** com confirmação explícita, use a tool `Task` com:

- `subagent_type`: o agente escolhido (ex: `react-coder`)
- `description`: nome curto da task (ex: `T01 — Cancel order dialog`)
- `prompt`: o briefing mostrado acima, incluindo caminho da Tech Spec e obrigação de respeitar `CLAUDE.md`/`rules/`.

### 6. Ao retornar

O agente volta com um resumo. Repasse ao usuário **o que o agente produziu** (arquivos alterados, testes passando/falhando) e sugira o próximo passo:

- Revisão do PR
- `/code tech-specs/<slug>__T02.md` se houver próxima task no plano

## Lembretes rígidos

- **Resposta ao usuário em pt-BR.** (Código gerado pelo agente permanece em inglês — responsabilidade do agente.)
- **Nunca pule a confirmação explícita do passo 4.** O valor deste comando é **remover ambiguidade**, não automatizar às cegas.
- **Uma Tech Spec por invocação.** Sem batch.
- **Se a Tech Spec estiver desatualizada** em relação às rules (ex: cita padrão que já mudou em `rules/patterns.md`), **pare** e oriente a atualizar a Tech Spec primeiro.

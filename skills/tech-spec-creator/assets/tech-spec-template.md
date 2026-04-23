# Tech Spec: [Nome da task] — `<TASK_ID>`

> **SPEC:** [`specs/<slug>.md`](../specs/<slug>.md)
> **Plano:** [`plans/<slug>.md`](../plans/<slug>.md) — task `<TASK_ID>`
> **Convenções aplicadas:** `CLAUDE.md` (projeto) + `~/.claude/CLAUDE.md` (usuário, quando aplicável)
>
> Este documento detalha **como** entregar a task. O **porquê** vive na SPEC; **o que** e **em que ordem**, no Plano.

---

## 🎯 Escopo desta task

- **Comportamento entregue** (do Plano): [uma frase do ponto de vista do usuário]
- **Histórias/critérios da SPEC cobertos:** H1, C3
- **Depende de:** — | T00
- **Dependências externas:** [doc de parceiro, credencial, etc. — ou "nenhuma"]

---

## 🧱 Arquitetura

- **Abordagem geral:** [2–4 frases descrevendo como a task se encaixa no código existente]
- **Módulos afetados:** [`src/features/X/`, `src/lib/Y.ts`, etc.]
- **Novos arquivos:** [lista curta com propósito de cada um]
- **Padrões reutilizados:** [cite arquivos do repo — ex: "segue padrão de `src/features/orders/ConfirmDialog.tsx`"]

> **Fonte das decisões:** CLAUDE.md (stack), padrão existente em [arquivo].

---

## 🔌 Contratos

### API / Integração
```
POST /orders/:id/cancel
Request:
  { reason: string (1..280) }
Response 200:
  { status: 'cancelled', cancelledAt: ISO8601 }
Response 4xx:
  400 invalid_reason | 404 order_not_found | 409 already_cancelled
```

### Eventos / mensagens (se aplicável)
```
OrderCancelled { orderId, reason, cancelledAt }
```

### Interfaces internas (hooks, services, types)
```ts
// src/features/orders/cancel/types.ts
type CancelOrderInput = { orderId: string; reason: string };
type CancelOrderResult = { cancelledAt: string };
```

---

## 🗂️ Modelo de dados

| Campo | Tipo | Obrigatório | Default | Observações |
|---|---|---|---|---|
| `reason` | `string` | sim | — | 1..280 chars, trim aplicado |
| `cancelledAt` | `ISO8601` | sim | `now()` | preenchido pelo backend |

> **Validação:** schema Zod em `cancel.schema.ts`. Fonte: padrão existente em `src/features/checkout/`.

---

## 🔗 Integrações externas

Somente preencher se a task depende de sistema de terceiro:

- **Parceiro:** [nome]
- **Documentação de referência:** [link Swagger/wiki/arquivo — obtido na SPEC]
- **Endpoint(s) usado(s):** [método + path]
- **Autenticação:** [OAuth2 bearer / API key / etc.]
- **Rate limits / retry:** [política]
- **Contrato mock para testes:** [arquivo de fixture]

---

## ⚖️ Trade-offs e alternativas descartadas

Para cada decisão não-trivial, registre:

**Decisão:** [ex: usar TanStack Query em vez de fetch direto]
- **Alternativa descartada:** [fetch direto no componente]
- **Motivo:** [cache, retry, invalidation já padronizados no repo]
- **Fonte:** [CLAUDE.md / padrão em X.tsx]

---

## ⚠️ Riscos e mitigações

| Risco | Impacto | Mitigação |
|---|---|---|
| [ex: cancelamento concorrente (dupla chamada)] | dados inconsistentes | idempotência via `orderId` no backend + disable do botão no frontend |
| [ex: usuário cancela por engano] | reversão cara | dialog de confirmação com nome do pedido |

---

## 🧪 Plano de testes

- **Unit:**
  - `useCancelOrderMutation` — sucesso, erro 409, erro de rede
  - `cancel.schema.ts` — validação de `reason` (vazio, longo demais, com espaços)
- **Integration:**
  - `<CancelOrderDialog />` — abre, confirma, fecha em sucesso, mostra erro em falha
- **E2E (se aplicável):**
  - [cenário ponta a ponta, geralmente coberto pelo agente `tester`]

> **Framework/padrão:** Vitest + Testing Library. Fonte: padrão existente em `tests/`.

---

## 🪜 Plano de implementação

Sequência executável (cada passo deve virar 1 commit coeso):

1. Criar schema Zod `cancel.schema.ts`
2. Criar hook `useCancelOrderMutation` (com testes unit)
3. Criar componente `<CancelOrderDialog />` (com testes integration)
4. Integrar o dialog no `<OrdersTable />` (ação "Cancelar")
5. Cobrir o cenário de erro 409 (já cancelado)
6. Revisar acessibilidade do dialog (foco, escape, aria-label)

---

## 📚 Convenções aplicadas (de CLAUDE.md)

Liste aqui **apenas** convenções do CLAUDE.md que impactam esta task — não copie o CLAUDE.md inteiro:

- Stack: React + TypeScript + Vite
- Estilo: Tailwind CSS, sem CSS-in-JS
- Auth: `AuthProvider` + hook `useAuthedFetch`
- Testes: Vitest + Testing Library
- Idioma: código em inglês, resposta ao humano em pt-BR

> Se o projeto **não** tiver CLAUDE.md, esta seção registra as convenções combinadas durante a conversa.

---

## ✅ Pronto para codar?

- [ ] Arquitetura descrita com módulos e novos arquivos nomeados
- [ ] Contratos (API/eventos/interfaces) com forma final
- [ ] Modelo de dados com tipos, obrigatoriedade e defaults
- [ ] Trade-offs não-triviais têm alternativa descartada
- [ ] Riscos conhecidos listados com mitigação
- [ ] Plano de testes cobre happy path + pelo menos 2 erros
- [ ] Sequência de implementação é executável sem perguntas
- [ ] Nenhuma lib nova introduzida (ou, se sim, com justificativa explícita)
- [ ] Convenções de CLAUDE.md citadas e respeitadas

# Padrões de código

Padrões inegociáveis que toda Tech Spec e todo código precisa respeitar.

## Autenticação

- **Provider:** [preencher: ex. `AuthProvider` em `src/providers/auth.tsx`]
- **Requests autenticados:** [preencher: ex. usar hook `useAuthedFetch` — nunca `fetch`/`axios` direto em rotas protegidas]

## Data fetching e estado remoto

- **Lib:** [preencher: ex. TanStack Query v5]
- **Client centralizado em:** [preencher: ex. `src/lib/queryClient.ts`]
- **Query keys:** [preencher: ex. `['orders', orderId]`]

## Estado local / global

- **Local:** [preencher: ex. `useState` / `useReducer`]
- **Global:** [preencher: ex. Zustand — store por domínio em `src/stores/`]
- **Proibido:** [preencher: ex. Redux, Context API para estado mutável]

## Formulários e validação

- **Form lib:** [preencher: ex. React Hook Form]
- **Schema lib:** [preencher: ex. Zod — schema sempre em `*.schema.ts` ao lado do componente]
- **Exibição de erro:** [preencher: ex. inline via `<FormError />`]

## Estilo

- **Lib:** [preencher: ex. Tailwind CSS]
- **Design tokens:** [preencher: ex. `tailwind.config.ts`]
- **Proibido:** [preencher: ex. CSS-in-JS (styled-components, emotion), CSS Modules]

## Tratamento de erro

- **Boundary:** [preencher: ex. `<ErrorBoundary />` em `src/components/ErrorBoundary.tsx`]
- **Logging:** [preencher: ex. Sentry — helper em `src/lib/logger.ts`]
- **Mensagem ao usuário:** [preencher: ex. toast com `<Toast variant="error" />`, nunca `alert()`]

## Acessibilidade

- **Alvo:** [preencher: ex. WCAG 2.1 AA]
- **Regras inegociáveis:**
  - Navegação por teclado em toda ação
  - `aria-label` em controles sem texto visível
  - Foco visível e retornável em dialogs/modais

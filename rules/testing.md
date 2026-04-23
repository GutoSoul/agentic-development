# Testes

- **Framework:** [preencher: ex. Vitest + Testing Library]
- **Estrutura:** [preencher: ex. `*.test.ts(x)` ao lado do arquivo testado]
- **Fixtures/mocks:** [preencher: ex. `tests/fixtures/`]
- **E2E:** [preencher: ex. Playwright em `tests/e2e/` | via agente `tester`]

## Cobertura mínima esperada

Toda função/hook público deve ter, no mínimo:

- ✅ Happy path
- ✅ 1 caso de erro explícito
- ✅ 1 caso de borda (entrada vazia, limite numérico, etc.)

Código sem testes passa na revisão **apenas** com justificativa registrada na Tech Spec.

## O que NÃO testar

- Implementação interna de libs de terceiros
- Estilos (Tailwind classes) — a menos que a lógica condicional seja complexa
- Stubs/fixtures em si

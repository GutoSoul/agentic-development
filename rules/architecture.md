# Arquitetura & estrutura de pastas

## Organização padrão

```
src/
  features/       # feature-first — 1 pasta por domínio de negócio
    <domain>/
      components/
      hooks/
      schemas/
      types.ts
  lib/            # utilitários cross-domain (queryClient, logger, ...)
  providers/      # providers de alto nível (auth, theme, ...)
  components/     # componentes de UI compartilhados entre features
```

## Princípios

- **Feature-first, não layer-first.** Nada de `controllers/`, `services/`, `models/` como pastas primárias.
- **Compartilhado só depois de provado.** Componente só sobe para `components/` quando 2+ features usam.
- **Um arquivo, uma responsabilidade.** Componente pai, subcomponentes privados, hook, schema — separados.
- **Nomeação em inglês.** Pastas e arquivos seguem a regra de [language.md](language.md).

## Quando criar uma nova `feature/`

- O domínio de negócio é claramente distinto (ex: `checkout` vs `orders` vs `users`)
- Tem pelo menos 2 telas/fluxos próprios, OU
- Tem modelo de dados próprio com regras específicas

> Motivo: `features/` rasa e plana fica legível; nested profundo é pesadelo de manutenção.

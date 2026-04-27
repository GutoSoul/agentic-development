# CLAUDE.md — Convenções deste projeto

> **Sobre este arquivo:** Este é o **índice das Rules** do projeto. Claude Code carrega este arquivo automaticamente no início de toda sessão, seguindo cada `@import` abaixo.
>
> **Como usar ao copiar para um projeto real:**
> 1. Coloque este arquivo e a pasta `rules/` na **raiz do repo** (ou em `~/.claude/` para aplicar globalmente).
> 2. Abra cada arquivo em `rules/` e preencha os placeholders `[preencher: ...]` com as decisões reais do time.
> 3. **Remova imports de seções que não se aplicam** — regras infladas são ignoradas. Menos é mais.
> 4. Quando uma convenção mudar, **atualize o arquivo correspondente** em `rules/`. Este conjunto é a fonte da verdade.

## Rules (@imports)

@rules/language.md
@rules/stack.md
@rules/patterns.md
@rules/testing.md
@rules/architecture.md
@rules/anti-patterns.md
@rules/workflow.md

---

> **Princípio:** este arquivo é só o índice. Toda convenção substantiva vive em `rules/<tópico>.md`. Isso deixa cada regra auditável, evolutiva e fácil de discutir em PR.


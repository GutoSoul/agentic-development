---
description: Quebra uma SPEC aprovada em um plano de tasks independentes, prontas para Tech Spec.
argument-hint: "[caminho-da-spec.md]"
---

Você foi invocado via `/plan`. Inicie o fluxo de quebra de tasks.

**Argumento recebido:** $ARGUMENTS

## O que fazer

1. **Invoque imediatamente a skill `task-planner`** via a tool `Skill`. Essa skill contém o protocolo completo (leitura da SPEC, research opcional via subagentes `Explore`, proposta inicial, rodadas de `AskUserQuestion`, escrita final em `plans/<slug>.md`).

2. **Entrada para a skill:**
   - Se `$ARGUMENTS` for um caminho de arquivo existente → trate como SPEC de referência.
   - Se `$ARGUMENTS` estiver vazio → liste os arquivos em `specs/` e pergunte ao usuário qual SPEC ele quer planejar.
   - Se `$ARGUMENTS` apontar para um arquivo que **não existe** → informe e sugira rodar `/spec` antes. **Não invente SPEC.**

3. **Pré-requisito inegociável:** a SPEC deve existir e ter o checklist "Pronto para virar plano?" atendido. Se estiver com lacunas visíveis, **pare** e oriente o usuário a voltar para `/spec`.

4. **Não escreva o plano diretamente aqui.** O comando `/plan` é apenas o gatilho — o trabalho real acontece dentro da skill `task-planner`.

## Lembretes rígidos

- **Resposta ao usuário sempre em pt-BR.**
- **Zero detalhes técnicos no plano** (stack, schema, endpoint, infra, estimativas). Essas decisões vivem na Tech Spec de cada task, uma etapa depois.
- **Uma task = um comportamento entregável = uma Tech Spec.** Se não couber nessa equação, quebre mais.
- **Fim de jogo:** plano gravado em `plans/<slug>.md` + resumo curto + próximo passo sugerido (`/tech-spec plans/<slug>.md#T01`).

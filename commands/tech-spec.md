---
description: Detalha tecnicamente UMA task de um plano aprovado. Produz a Tech Spec pronta para o agente de código.
argument-hint: "[plans/<slug>.md#<TASK_ID>]"
---

Você foi invocado via `/tech-spec`. Inicie o fluxo de detalhamento técnico.

**Argumento recebido:** $ARGUMENTS

## O que fazer

1. **Invoque imediatamente a skill `tech-spec-creator`** via a tool `Skill`. A skill contém o protocolo completo (carregar CLAUDE.md + SPEC + plano, research via subagentes `Explore` em paralelo, proposta inicial, rodadas de `AskUserQuestion`, escrita final em `tech-specs/<slug>__<TASK_ID>.md`).

2. **Entrada para a skill:**
   - `plans/<slug>.md#T01` → task-alvo identificada → siga direto para a skill.
   - `plans/<slug>.md` sem âncora → peça ao usuário qual task do plano.
   - Vazio → liste arquivos em `plans/` e pergunte qual plano + qual task.
   - Plano inexistente ou não aprovado ("Pronto para Tech Spec?" não marcado) → **pare** e oriente a rodar `/plan` antes. **Não invente task.**

3. **Uma Tech Spec por invocação.** Se o usuário pedir para detalhar várias tasks, recuse e faça uma por vez — cada task merece sua rodada própria de research e negociação.

4. **Contexto do repo é obrigatório.** A skill vai carregar `CLAUDE.md` do projeto (e `~/.claude/CLAUDE.md` do usuário, se existir). Se nenhum existir, a skill **pergunta** as convenções antes de propor — não adivinha.

5. **Não escreva a Tech Spec diretamente aqui.** O comando `/tech-spec` é apenas o gatilho.

## Lembretes rígidos

- **Resposta ao usuário sempre em pt-BR.**
- **Código e identificadores em inglês** no documento (nomes de arquivos, variáveis, funções, tipos, endpoints, campos).
- **Decisões citam fonte:** CLAUDE.md, arquivo existente no repo, lib já instalada, ou "nova: motivo".
- **Research é mandatório** — mesmo task aparentemente simples passa por 1–2 subagentes `Explore` antes da proposta, para garantir alinhamento com padrões do repo.
- **Fim de jogo:** Tech Spec gravada em `tech-specs/<slug>__<TASK_ID>.md` + resumo curto + sugestão de qual agente de código invocar em seguida.

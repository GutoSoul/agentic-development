# Anti-padrões

O que **não** fazer neste projeto, e o motivo. Sem motivo, regra vira arbitrariedade e ninguém respeita.

## Código

- **`any` em TypeScript** — Motivo: mata o type-safety. Use `unknown` + narrowing.
- **Comentários explicando `o que`** — Motivo: nomes claros já dizem. Comente só o `por quê` quando não for óbvio.
- **Abstrações especulativas** — Motivo: 3 linhas duplicadas é melhor que um helper prematuro. Abstraia quando doer.
- **Feature flags deixadas "para depois"** — Motivo: código morto vira debt. Remova assim que a feature estabilizar.

## Dependências

- **Lib nova sem discussão** — Motivo: este repo é minimalista por decisão. Reaproveitar > instalar.
- **Manter versão de dependência travada sem razão** — Motivo: debt de segurança. Atualize ou justifique o trave na Tech Spec.

## Processo

- **Código sem Tech Spec** — Motivo: implementação sem contrato vira retrabalho.
- **Tech Spec sem Plano** — Motivo: detalhar isoladamente perde a sequência e dependências.
- **Plano sem SPEC** — Motivo: quebrar task sem entender o problema gera scope creep.
- **Pular research técnico no Tech Spec** — Motivo: reinventa padrão que já existe no repo.

## UX

- **`alert()` ou `confirm()` nativos** — Motivo: quebram o design system e não são acessíveis como esperado.
- **Loading sem feedback visual** — Motivo: parece travado. Toda ação > 200ms precisa de indicador.
- **Erro sem ação sugerida ao usuário** — Motivo: "algo deu errado" é bullying do sistema com o usuário.

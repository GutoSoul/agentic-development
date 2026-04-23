# Agentic Development 

## Agentes disponíveis

| Agente | Modelo | Propósito |
|---|---|---|
| `react-coder` | sonnet | Escrever, refatorar e revisar código React |
| `vue-coder` | sonnet | Escrever, refatorar e revisar código Vue 3 |
| `tester` | sonnet | Testes manuais de UI, validação de interações e console |

Todos respondem ao usuário em **pt-BR** e mantêm código + termos técnicos em inglês.

## Pré-requisitos

### Geral
- Claude Code instalado e configurado
- Permissão de uso dos MCPs declarados em cada agente (`tools:` no frontmatter)

### Específico do `tester` — Claude in Chrome MCP

O agente `tester` depende do **Claude in Chrome MCP**, que controla uma instância real do Chrome via extensão de browser. **Sem essa extensão instalada e autorizada, o agente não funciona.**

#### Como instalar

1. Instale a extensão **Claude for Chrome** na loja do Chrome
2. Faça login com a conta Claude autorizada (mesma conta usada no Claude Code)
3. Abra o Chrome **antes** de invocar o agente — o MCP se conecta à janela ativa
4. Conceda permissão quando o agente tentar usar as tools `mcp__Claude_in_Chrome__*` pela primeira vez

#### Tools usadas pelo `tester`

- **Navegação**: `navigate`, `tabs_create_mcp`, `tabs_close_mcp`, `tabs_context_mcp`
- **Inspeção**: `read_page`, `get_page_text`, `find`, `read_console_messages`, `read_network_requests`
- **Interação**: `form_input`, `computer` (clique/screenshot), `browser_batch`
- **Utilitários**: `resize_window`, `javascript_tool`

#### Alternativa considerada

O Claude Preview MCP (sandbox headless) foi avaliado, mas descartado em favor do Claude in Chrome porque:
- Permite testar em ambiente real do usuário (cookies, auth, extensões)
- Facilita depuração visual — você vê o que o agente vê
- Não depende de subir preview separado para cada app

### Específico dos coders (`react-coder`, `vue-coder`)

Nenhum MCP especial. Usam apenas tools nativas: `Read`, `Edit`, `Write`, `Grep`, `Glob`, `Bash`, `WebFetch`.

## Convenções adotadas

- **Idioma**: resposta em pt-BR; código, identificadores e termos técnicos em inglês
- **Modelo padrão**: `sonnet` (evita custo desnecessário de `opus` em tarefas de execução)
- **Tools declaradas explicitamente** no frontmatter — nenhum agente herda todas
- **Escopo restrito**: cada agente tem seção "What NOT to do" para evitar overreach
- **Hard stops numéricos**: limites concretos (ex.: max 8 interações) em vez de "use julgamento"

## Como invocar

No Claude Code principal:

```
Use o agente tester para validar o formulário em localhost
Use o agente react-coder para criar um componente de dropdown responsivo
```

Ou via ferramenta `Task` com `subagent_type` correspondente.

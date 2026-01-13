# Guia Mestre do Ecossistema Claude: Da Teoria à Prática Agêntica

**Versão:** 1.0 | Janeiro 2026  
**Propósito:** Base de conhecimento unificada para orientar agentes de inteligência artificial e desenvolvedores no uso completo do ecossistema Claude da Anthropic.

---

## Instruções para Uso como Base de Conhecimento

Este documento foi estruturado para servir como referência autoritativa sobre o ecossistema Claude. Uma inteligência artificial que utilize este conhecimento deve:

### Princípios de Aplicação
1. **Priorizar informações específicas** — Quando o usuário perguntar sobre Claude Code, consultar as seções 4-14 para detalhes técnicos precisos
2. **Contextualizar recomendações** — Adaptar sugestões ao nível de experiência do usuário (iniciante vs. avançado)
3. **Referenciar seções relevantes** — Ao responder, indicar qual seção do guia contém informações complementares
4. **Manter coerência** — Seguir as convenções, comandos e práticas descritas neste documento

### Estrutura de Consulta Recomendada
- **Perguntas sobre instalação e configuração:** Seções 4, 15-18
- **Perguntas sobre comandos e uso diário:** Seções 5-6, Apêndice B
- **Perguntas sobre personalização:** Seções 7-10
- **Perguntas sobre recursos avançados:** Seções 11-14
- **Perguntas sobre boas práticas:** Seções 19-20, Apêndice A
- **Perguntas sobre problemas:** Seção 21

### Atualização de Conhecimento
Este guia reflete o estado do ecossistema Claude em janeiro de 2026. Funcionalidades, preços e comandos podem ter sido atualizados. Quando houver dúvida sobre informações atuais, recomendar consulta à documentação oficial em https://code.claude.com/docs.

---

## Sumário

### Parte I: Fundamentos
1. [Visão Geral do Ecossistema Claude](#1-visão-geral-do-ecossistema-claude)
2. [Modelos, Planos e Precificação](#2-modelos-planos-e-precificação)
3. [Filosofia e Paradigma de Desenvolvimento](#3-filosofia-e-paradigma-de-desenvolvimento)

### Parte II: Claude Code — Ferramenta Central
4. [Instalação e Configuração Inicial](#4-instalação-e-configuração-inicial)
5. [Modos de Operação e Interface](#5-modos-de-operação-e-interface)
6. [Comandos e Atalhos Essenciais](#6-comandos-e-atalhos-essenciais)
7. [Sistema de Memória e Contextualização](#7-sistema-de-memória-e-contextualização)

### Parte III: Personalização e Automação
8. [Comandos Slash Personalizados](#8-comandos-slash-personalizados)
9. [Hooks: Automação Baseada em Eventos](#9-hooks-automação-baseada-em-eventos)
10. [Skills: Capacidades Portáteis](#10-skills-capacidades-portáteis)

### Parte IV: Recursos Agênticos Avançados
11. [Subagentes: Especialização e Paralelismo](#11-subagentes-especialização-e-paralelismo)
12. [Model Context Protocol e Integrações](#12-model-context-protocol-e-integrações)
13. [Técnicas Avançadas de Uso de Ferramentas](#13-técnicas-avançadas-de-uso-de-ferramentas)
14. [Sistema de Plugins Claude Code](#14-sistema-de-plugins-claude-code)

### Parte V: Ambiente de Desenvolvimento
15. [Extensão VS Code e Configuração de IDE](#15-extensão-vs-code-e-configuração-de-ide)
16. [Extensões VS Code Complementares](#16-extensões-vs-code-complementares)
17. [Terminal, Shell e Ferramentas de Linha de Comando](#17-terminal-shell-e-ferramentas-de-linha-de-comando)
18. [Fontes, Temas e Personalização Visual](#18-fontes-temas-e-personalização-visual)

### Parte VI: Prática e Excelência
19. [Fluxos de Trabalho Práticos](#19-fluxos-de-trabalho-práticos)
20. [Melhores Práticas e Modelos Mentais](#20-melhores-práticas-e-modelos-mentais)
21. [Solução de Problemas](#21-solução-de-problemas)
22. [Referências e Recursos](#22-referências-e-recursos)

### Apêndices
- [Apêndice A: Exemplos Práticos de Prompts e Fluxos](#apêndice-a-exemplos-práticos-de-prompts-e-fluxos)
- [Apêndice B: Comandos de Referência Rápida](#apêndice-b-comandos-de-referência-rápida)
- [Apêndice C: Template CLAUDE.md](#apêndice-c-template-claudemd)
- [Apêndice D: Script de Configuração Automatizada](#apêndice-d-script-de-configuração-automatizada)

---

# Parte I: Fundamentos

---

## 1. Visão Geral do Ecossistema Claude

### 1.1 O Que é o Claude Code

O Claude Code é uma ferramenta de codificação agêntica desenvolvida pela Anthropic que opera diretamente no terminal do desenvolvedor. Diferente de ferramentas de autocomplete como GitHub Copilot, o Claude Code funciona como um agente completo capaz de:

- Ler, escrever e editar arquivos no sistema
- Executar comandos de shell
- Gerenciar contexto de projeto
- Fazer commits no Git
- Iterar autonomamente até completar tarefas

O princípio de design fundamental é dar à inteligência artificial as mesmas ferramentas que programadores usam diariamente, transformando-a de um assistente passivo em um participante ativo no ambiente de desenvolvimento.

### 1.2 Componentes do Ecossistema

```
┌─────────────────────────────────────────────────────────────────┐
│                    ECOSSISTEMA CLAUDE                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │   Modelos   │  │    APIs     │  │   SDKs      │             │
│  │             │  │             │  │             │             │
│  │ • Opus      │  │ • Messages  │  │ • Python    │             │
│  │ • Sonnet    │  │ • Files     │  │ • TypeScript│             │
│  │ • Haiku     │  │ • Batch     │  │ • Java/Go   │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    CLAUDE CODE                           │   │
│  │  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐       │   │
│  │  │Terminal │ │ VS Code │ │JetBrains│ │  Web    │       │   │
│  │  │  (CLI)  │ │Extension│ │ Plugin  │ │Interface│       │   │
│  │  └─────────┘ └─────────┘ └─────────┘ └─────────┘       │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │  Agent SDK  │  │     MCP     │  │   Plugins   │             │
│  │             │  │  Servers    │  │  & Skills   │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 1.3 Plataformas de Acesso

| Plataforma | Descrição | Melhor Para |
|------------|-----------|-------------|
| **Terminal (CLI)** | Interface nativa de linha de comando | Power users, automação, scripts |
| **VS Code Extension** | Integração direta no editor | Desenvolvedores web, iniciantes |
| **JetBrains Plugin** | Plugin para IntelliJ, PyCharm etc. | Desenvolvedores Java, Python |
| **Claude.ai Web** | Interface web conversacional | Uso geral, não-desenvolvedores |
| **Claude Desktop** | Aplicativo desktop | Uso offline, integração sistema |

---

## 2. Modelos, Planos e Precificação

### 2.1 Família de Modelos Claude

| Modelo | Características | Casos de Uso |
|--------|-----------------|--------------|
| **Claude Opus 4.5** | Mais capaz, raciocínio profundo | Tarefas complexas, análise avançada, arquitetura |
| **Claude Sonnet 4.5** | Equilíbrio velocidade/capacidade | Desenvolvimento diário, código, assistência geral |
| **Claude Haiku 3.5** | Mais rápido, menor custo | Tarefas simples, alto volume, baixa latência |

### 2.2 Planos de Assinatura

| Plano | Preço | Uso Claude Code | Características |
|-------|-------|-----------------|-----------------|
| **Free** | Gratuito | Limitado | Cota variável, reset a cada 5 horas |
| **Pro** | 20 dólares/mês | Sim | 5x mais uso que Free, acesso ao Opus |
| **Max 5x** | 100 dólares/mês | Sim | 5x mais uso que Pro |
| **Max 20x** | 200 dólares/mês | Sim | 20x mais uso que Pro, sem restrições |
| **Team Standard** | 30 dólares/usuário/mês | Sim | Mínimo 5 usuários, faturamento centralizado |
| **Team Premium** | 150 dólares/usuário/mês | Sim | Uso elevado, recursos avançados |
| **Enterprise** | Personalizado | Sim | SSO, auditoria, governança avançada |

**Importante:** Os limites de uso são resetados a cada 5 horas e são compartilhados entre todas as interfaces Claude (web, desktop, mobile e Claude Code).

### 2.3 Precificação da API (Pay-as-you-go)

| Modelo | Input (por milhão de tokens) | Output (por milhão de tokens) |
|--------|------------------------------|-------------------------------|
| Claude Opus 4.5 | 5,00 dólares | 25,00 dólares |
| Claude Sonnet 4.5 (até 200K input) | 3,00 dólares | 15,00 dólares |
| Claude Sonnet 4.5 (acima de 200K input) | 6,00 dólares | 22,50 dólares |
| Claude Haiku 3.5 | 0,80 dólares | 4,00 dólares |

**Otimizações de Custo:**
- **Batch API:** Desconto de 50% para processamento assíncrono
- **Prompt Caching:** Tokens em cache custam 0.1x da taxa base
- **Custo médio estimado:** Um desenvolvedor individual usando Claude Code gasta aproximadamente 6 dólares por dia

---

## 3. Filosofia e Paradigma de Desenvolvimento

### 3.1 O Modelo Mental Correto

O Claude Code deve ser tratado como um **colega de equipe júnior** — especificamente, um "estagiário muito rápido com memória perfeita, mas que precisa de direção". Esta mentalidade é crucial porque:

1. **Requer instruções claras** — prompts vagos geram resultados vagos
2. **Precisa de supervisão** — revisar mudanças antes de aceitar
3. **Beneficia-se de estrutura** — controle de versão como rede de segurança
4. **Aprende com feedback** — adicionar regras ao CLAUDE.md refina comportamento

### 3.2 O Ciclo Agêntico

O Claude Code opera em um ciclo de feedback contínuo:

```
┌──────────────────────────────────────────────────────┐
│                                                      │
│    ┌─────────────┐                                   │
│    │   COLETAR   │◄──────────────────────────────┐  │
│    │  CONTEXTO   │                               │  │
│    └──────┬──────┘                               │  │
│           │                                      │  │
│           ▼                                      │  │
│    ┌─────────────┐                               │  │
│    │    TOMAR    │                               │  │
│    │    AÇÃO     │                               │  │
│    └──────┬──────┘                               │  │
│           │                                      │  │
│           ▼                                      │  │
│    ┌─────────────┐                               │  │
│    │  VERIFICAR  │───────────────────────────────┘  │
│    │  RESULTADO  │                                  │
│    └─────────────┘                                  │
│                                                      │
└──────────────────────────────────────────────────────┘
```

### 3.3 Princípios de Colaboração Efetiva

| Princípio | Descrição |
|-----------|-----------|
| **Especificidade** | "Corrija o bug de login onde usuários veem tela em branco após credenciais erradas" em vez de "corrija o bug" |
| **Divisão de tarefas** | Tarefas complexas devem ser quebradas em etapas numeradas |
| **Uso do sistema de arquivos** | Organize contexto em arquivos em vez de sobrecarregar prompts |
| **Controle de versão como âncora** | Commits frequentes permitem `git restore .` quando abordagem falha |
| **Interrupção e redirecionamento** | Interromper (Escape ou Control+C) quando caminho é incorreto |

---

# Parte II: Claude Code — Ferramenta Central

---

## 4. Instalação e Configuração Inicial

### 4.1 Métodos de Instalação

| Método | Comando | Observações |
|--------|---------|-------------|
| **Nativo (Recomendado)** | `curl -fsSL https://claude.ai/install.sh \| bash` (macOS/Linux) | Não depende de npm ou Node.js |
| **Windows PowerShell** | `irm https://claude.ai/install.ps1 \| iex` | Instalador nativo Windows |
| **Homebrew** | `brew install --cask claude-code` | Requer Homebrew instalado |
| **NPM** | `npm install -g @anthropic-ai/claude-code` | Requer Node.js 18 ou superior |

### 4.2 Autenticação

**Opção 1: Variável de Ambiente (Recomendado para API)**
```bash
# Adicionar ao ~/.zshrc ou ~/.bashrc
export ANTHROPIC_API_KEY="sua-chave-aqui"
```

**Opção 2: Login via Navegador (Pro/Max)**
Na primeira execução do comando `claude`, será oferecida a opção de autenticar via navegador.

### 4.3 Primeira Sessão

```bash
# Iniciar Claude Code
claude

# No projeto, executar inicialização
/init
```

O comando `/init` é essencial para novos projetos. Ele:
- Analisa a base de código automaticamente
- Cria arquivo `CLAUDE.md` com contexto do projeto
- Identifica comandos de build, estrutura de pastas e convenções

---

## 5. Modos de Operação e Interface

### 5.1 Três Modos de Operação

O Claude Code possui três modos principais, alternados com `Shift+Tab`:

| Modo | Comportamento | Quando Usar |
|------|---------------|-------------|
| **Edit Mode** (Padrão) | Requer aprovação antes de modificar arquivos; exibe diffs para revisão | Tarefas críticas, código de produção |
| **Auto-accept Mode** | Aplica mudanças automaticamente | Prototipagem, tarefas de baixo risco |
| **Plan Mode** | Cria planos de ação sem modificar código | Pesquisa, arquitetura, análise |

**Ciclo de alternância:** Edit → Auto-accept → Plan → Edit (via `Shift+Tab`)

### 5.2 Formas de Abrir o Claude Code (VS Code)

| Método | Ação |
|--------|------|
| Ícone Spark | Canto superior direito do editor |
| Barra Lateral | Ícone do Claude na Activity Bar |
| Paleta de Comandos | `Cmd+Shift+P` → "Claude Code" → "Open in New Tab" |
| Atalho Direto | `Cmd+Escape` (Mac) ou `Ctrl+Escape` (Windows/Linux) |

### 5.3 Gerenciamento de Sessão

| Comando | Descrição |
|---------|-----------|
| `claude` | Inicia nova sessão interativa |
| `claude "prompt"` | Inicia sessão com prompt inicial |
| `claude -p "prompt"` | Executa consulta única e sai (modo impressão) |
| `claude -c` ou `--continue` | Continua conversa mais recente |
| `claude -r "session-id"` | Retoma sessão específica |
| `cat arquivo \| claude -p "prompt"` | Processa conteúdo via pipe |

---

## 6. Comandos e Atalhos Essenciais

### 6.1 Atalhos de Teclado

**Controles Gerais:**

| Atalho | Função |
|--------|--------|
| `Ctrl+C` | Cancela entrada ou geração atual |
| `Ctrl+D` | Sai da sessão |
| `Ctrl+L` | Limpa a tela do terminal |
| `Seta para Cima/Baixo` | Navega histórico de comandos |
| `Escape+Escape` | Retrocede para mensagem anterior |
| `Tab` | Autocomplete |
| `Shift+Tab` | Alterna modos (Edit/Auto-accept/Plan) |
| `Ctrl+R` | Histórico pesquisável de prompts |

**Edição de Texto (estilo Bash):**

| Atalho | Função |
|--------|--------|
| `Ctrl+A` | Vai para início da linha |
| `Ctrl+E` | Vai para fim da linha |
| `Option+F` (Mac) | Avança uma palavra |
| `Option+B` (Mac) | Retrocede uma palavra |
| `Ctrl+W` | Deleta palavra anterior |

**Entrada Multilinha:**
- Barra invertida + Enter: funciona universalmente
- `Option+Enter`: cria nova linha no Mac
- `Shift+Enter`: funciona após executar `/terminal-setup`

### 6.2 Comandos Slash (Slash Commands)

**Comandos de Sessão:**

| Comando | Descrição |
|---------|-----------|
| `/clear` | Limpa histórico de conversa e contexto |
| `/compact [instruções]` | Compacta conversa com foco opcional |
| `/exit` | Sai do modo interativo |
| `/help` | Mostra comandos disponíveis |
| `/cost` | Mostra estatísticas de uso de tokens |

**Comandos de Projeto:**

| Comando | Descrição |
|---------|-----------|
| `/init` | Inicializa projeto com arquivo de memória |
| `/add-dir` | Adiciona diretórios de trabalho |
| `/memory` | Edita arquivos de memória |
| `/review` | Solicita revisão de código |
| `/todos` | Lista itens pendentes da conversa |

**Comandos de Configuração:**

| Comando | Descrição |
|---------|-----------|
| `/config` | Abre interface de configurações |
| `/model` | Seleciona ou altera o modelo |
| `/permissions` | Visualiza ou atualiza permissões |
| `/doctor` | Verifica saúde da instalação |
| `/plugin` | Gerencia plugins |

**Comandos de Integração:**

| Comando | Descrição |
|---------|-----------|
| `/ide` | Gerencia integrações com IDEs |
| `/mcp` | Gerencia conexões com servidores MCP |
| `/agents` | Gerencia subagentes |
| `/hooks` | Configura ganchos de automação |
| `/install-github-app` | Configura ações do GitHub |

### 6.3 Notação Especial na Entrada

**Referências de Arquivo com `@`:**
```
# Arquivo único
@src/main.py Revise e melhore o tratamento de erros

# Com linhas específicas
@src/utils/helpers.js#L10-50

# Diretório recursivo
@./src/api/

# Padrões glob
@./src/**/*.test.ts

# Múltiplos arquivos
@./src/old.js @./src/new.js Compare estas implementações
```

**Memória Rápida com `#`:**
```
#Este projeto usa convenções de nomenclatura camelCase
```
Adiciona diretamente ao arquivo CLAUDE.md.

**Comandos Shell com `!`:**
```
!git status
!npm test
!docker ps
```
Executa sem processamento conversacional, economizando tokens.

---

## 7. Sistema de Memória e Contextualização

### 7.1 Hierarquia de Arquivos de Memória

O Claude Code carrega memórias em ordem de prioridade:

```
┌─────────────────────────────────────────────────────────────┐
│  1. MEMÓRIA GLOBAL                                          │
│     ~/.claude/CLAUDE.md                                     │
│     Aplica a todos os seus projetos                         │
├─────────────────────────────────────────────────────────────┤
│  2. MEMÓRIA DE PROJETO                                      │
│     ./CLAUDE.md ou ./.claude/CLAUDE.md                      │
│     Compartilhada via git com a equipe                      │
├─────────────────────────────────────────────────────────────┤
│  3. MEMÓRIA LOCAL                                           │
│     ./CLAUDE.local.md                                       │
│     Pessoal, ignorada pelo git                              │
├─────────────────────────────────────────────────────────────┤
│  4. REGRAS CONDICIONAIS                                     │
│     .claude/rules/                                          │
│     Regras por tipo de arquivo ou diretório                 │
└─────────────────────────────────────────────────────────────┘
```

### 7.2 Estrutura Recomendada do CLAUDE.md

```markdown
# Visão Geral do Projeto
Breve descrição do propósito e funcionalidade principal.

# Stack Tecnológica
- Frontend: React 18, TypeScript, Tailwind CSS
- Backend: Node.js, Express, PostgreSQL
- Deploy: Docker, AWS ECS

# Comandos Comuns
- `npm run dev`: Inicia servidor de desenvolvimento
- `npm test`: Executa testes
- `npm run build`: Gera build de produção
- `npm run lint`: Verifica qualidade do código

# Convenções de Código
- Use TypeScript com tipagem estrita
- Siga padrões de nomenclatura camelCase para variáveis e funções
- Use PascalCase para componentes e classes
- Testes devem estar no diretório __tests__
- Nunca commite arquivos .env

# Arquitetura
Referência @docs/architecture.md para detalhes completos.

# Regras Específicas
- Sempre faça: Adicionar tratamento de erros em chamadas de API
- Nunca faça: Usar console.log em produção
- Sempre faça: Escrever testes para funções críticas
```

### 7.3 Configuração via settings.json

**Hierarquia dos Arquivos:**
1. `~/.claude/settings.json` — Configurações do usuário (global)
2. `.claude/settings.json` — Configurações do projeto (compartilhado via git)
3. `.claude/settings.local.json` — Configurações locais (ignorado pelo git)

**Exemplo de settings.json:**
```json
{
  "model": "claude-sonnet-4-20250514",
  "permissions": {
    "allowedTools": [
      "Read",
      "Write(src/**)",
      "Bash(git *)",
      "Bash(npm *)"
    ],
    "deny": [
      "Read(.env*)",
      "Write(production.config.*)",
      "Bash(rm *)",
      "Bash(sudo *)"
    ]
  },
  "mcpServers": {
    "playwright": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@playwright/mcp@latest"]
    }
  }
}
```

### 7.4 Prompts para Análise de Projeto

| Prompt | Finalidade |
|--------|------------|
| `> summarize this project` | Visão geral do propósito e stack |
| `> explain the folder structure` | Organização e propósito de cada diretório |
| `> find the files that handle user authentication` | Localiza código de funcionalidade específica |
| `> explain the main architecture patterns used here` | Compreende decisões de design |
| `> what are the key data models?` | Entende estrutura de dados |

---

# Parte III: Personalização e Automação

---

## 8. Comandos Slash Personalizados

### 8.1 Criando Comandos de Projeto

Comandos compartilhados com a equipe via git:

```bash
# Criar diretório de comandos
mkdir -p .claude/commands

# Criar comando simples
echo "Analise este código em busca de problemas de performance:" > .claude/commands/optimize.md
```

**Uso:** `/optimize`

### 8.2 Criando Comandos Pessoais

Comandos disponíveis em todos os seus projetos:

```bash
mkdir -p ~/.claude/commands
echo "Revise este código para vulnerabilidades de segurança:" > ~/.claude/commands/security.md
```

### 8.3 Comandos com Argumentos

Crie `.claude/commands/fix-issue.md`:
```markdown
---
description: Corrige uma issue específica
argument-hint: [número-da-issue]
---

Corrija a issue #$ARGUMENTS seguindo nossos padrões de código.
Analise os requisitos da issue e implemente a solução.
```

**Uso:** `/fix-issue 123`

### 8.4 Frontmatter Avançado

```markdown
---
allowed-tools: Bash(git *), Read, Write
description: Cria um commit git com mensagem descritiva
model: claude-sonnet-4-20250514
---

Execute os seguintes passos:
1. !git status
2. !git diff --staged
3. Analise as mudanças e gere uma mensagem de commit seguindo Conventional Commits
4. !git commit -m "[mensagem gerada]"
```

### 8.5 Exemplos de Comandos Úteis

**Comando de Commit Inteligente (.claude/commands/commit.md):**
```markdown
---
description: Gera commit com mensagem automática
allowed-tools: Bash(git *)
---

Execute em ordem:
1. !git add .
2. !git status
3. Analise as mudanças com !git diff --cached
4. Gere mensagem de commit seguindo Conventional Commits
5. Execute o commit
```

**Comando de Documentação (.claude/commands/doc.md):**
```markdown
---
description: Documenta função ou arquivo
argument-hint: [caminho-do-arquivo]
---

Analise o arquivo @$ARGUMENTS e:
1. Adicione JSDoc/docstrings para todas as funções
2. Crie um comentário de cabeçalho explicando o propósito do arquivo
3. Documente parâmetros e retornos
```

---

## 9. Hooks: Automação Baseada em Eventos

### 9.1 Conceito

Hooks são gatilhos determinísticos que executam comandos de shell em pontos específicos do ciclo de vida do Claude Code. Diferente dos prompts (sugestões), hooks são garantias de execução.

### 9.2 Eventos Disponíveis

| Evento | Descrição | Caso de Uso |
|--------|-----------|-------------|
| **PreToolUse** | Antes de usar uma ferramenta | Bloquear ações em arquivos .env (retornar código 2) |
| **PostToolUse** | Após ferramenta ser usada com sucesso | Formatar código Python com black após escrita |
| **SessionStart** | No início de cada sessão | Injetar contexto, carregar lista de tarefas |
| **Notification** | Quando Claude precisa de entrada do usuário | Enviar notificação para desktop |

### 9.3 Configuração em settings.json

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Write(.env*)",
        "command": "echo 'Bloqueado: não é permitido escrever em arquivos .env' && exit 2"
      }
    ],
    "PostToolUse": [
      {
        "matcher": "Write(*.py)",
        "command": "black $FILE"
      },
      {
        "matcher": "Write(*.ts)",
        "command": "prettier --write $FILE"
      }
    ],
    "SessionStart": [
      {
        "command": "echo 'Tarefas pendentes:' && cat TODO.md 2>/dev/null || echo 'Nenhuma'"
      }
    ]
  }
}
```

### 9.4 Bloqueando Ações

Um hook pode bloquear uma ação retornando código de saída `2`:
```bash
# Hook PreToolUse que bloqueia escrita em produção
if [[ "$FILE" == *"production"* ]]; then
  echo "ERRO: Escrita em arquivos de produção não permitida"
  exit 2
fi
```

---

## 10. Skills: Capacidades Portáteis

### 10.1 Conceito

Skills são pacotes que combinam instruções (prompts) com código (scripts), criando capacidades reutilizáveis invocáveis por linguagem natural. O Claude decide quando usá-las com base no contexto.

### 10.2 Diferença entre Skills e Slash Commands

| Aspecto | Slash Commands | Skills |
|---------|----------------|--------|
| Invocação | Explícita (`/comando`) | Por linguagem natural |
| Controle | Determinístico | Claude decide quando usar |
| Portabilidade | Apenas Claude Code | Claude Code, Claude.ai, Desktop |

### 10.3 Estrutura de uma Skill

```
minha-skill/
├── SKILL.md           # Instruções principais (obrigatório)
├── scripts/           # Scripts auxiliares
│   └── process.py
└── templates/         # Templates reutilizáveis
    └── output.md
```

**Exemplo de SKILL.md:**
```markdown
---
name: Gerador de Relatórios
description: Gera relatórios formatados a partir de dados
trigger: quando o usuário pedir para gerar relatório ou criar report
---

# Instruções

Quando solicitado a gerar um relatório:

1. Colete os dados necessários
2. Execute o script @scripts/process.py para processar
3. Use o template @templates/output.md para formatar
4. Gere o arquivo final em formato Markdown

# Formato de Saída

O relatório deve conter:
- Resumo executivo
- Dados detalhados
- Conclusões e recomendações
```

### 10.4 Consideração sobre Confiabilidade

A invocação automática de skills por linguagem natural pode ser inconsistente. Para fluxos de trabalho críticos que exigem execução garantida, **Slash Commands personalizados** são mais confiáveis que Skills.

---

# Parte IV: Recursos Agênticos Avançados

---

## 11. Subagentes: Especialização e Paralelismo

### 11.1 Conceito

Subagentes são instâncias especializadas do Claude, cada uma com sua própria janela de contexto e persona. Eles resolvem dois problemas centrais:

1. **Paralelização:** Múltiplos subagentes trabalham simultaneamente em diferentes partes de um problema
2. **Gerenciamento de Contexto:** Isolar tarefas evita poluição da janela de contexto principal

### 11.2 Criação e Gerenciamento

```bash
# Via comando interativo
/agents

# Definição em arquivo
mkdir -p .claude/agents/
```

**Exemplo de definição (.claude/agents/security-reviewer.md):**
```markdown
---
name: Revisor de Segurança
description: Especialista em revisão de código para vulnerabilidades de segurança
---

# Persona
Você é um especialista em segurança de software com foco em:
- Vulnerabilidades OWASP Top 10
- Injeção de SQL e XSS
- Autenticação e autorização
- Exposição de dados sensíveis

# Comportamento
Ao revisar código:
1. Identifique todas as potenciais vulnerabilidades
2. Classifique por severidade (Alta, Média, Baixa)
3. Forneça exemplos de exploração
4. Sugira correções específicas
```

### 11.3 Delegação Automática

O Claude pode delegar tarefas automaticamente para subagentes com base em suas descrições:

```
> review my recent code changes for security issues
```

O Claude identificará o subagente "Revisor de Segurança" e delegará a tarefa.

### 11.4 Casos de Uso

| Subagente | Responsabilidade |
|-----------|------------------|
| Desenvolvedor | Implementação de código |
| Revisor | Revisão de qualidade |
| Testador | Criação de testes |
| Documentador | Escrita de documentação |
| Arquiteto | Decisões de design |
| Refatorador | Modernização de código legado |

---

## 12. Model Context Protocol e Integrações

### 12.1 O Que é MCP

O Model Context Protocol (MCP) é um sistema padronizado que conecta o Claude a ferramentas e serviços externos de forma segura. Ele abstrai a complexidade de autenticação e chamadas de API.

### 12.2 Adicionando Servidores MCP

```bash
# GitHub - Integração completa com repositórios
claude mcp add github -- npx -y @modelcontextprotocol/server-github

# Playwright - Automação de navegador
claude mcp add playwright -- npx -y @playwright/mcp@latest

# PostgreSQL - Consultas em linguagem natural
claude mcp add postgres -- npx -y @modelcontextprotocol/server-postgres

# SQLite - Gerenciamento de banco de dados
claude mcp add sqlite -- npx -y @modelcontextprotocol/server-sqlite

# Sistema de arquivos avançado
claude mcp add filesystem -- npx -y @modelcontextprotocol/server-filesystem

# Supabase
claude mcp add supabase -- npx -y @supabase/mcp-server
```

### 12.3 Configuração via settings.json

```json
{
  "mcpServers": {
    "playwright": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@playwright/mcp@latest"],
      "env": {}
    },
    "github": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "${GITHUB_TOKEN}"
      }
    }
  }
}
```

### 12.4 Gerenciamento

```bash
# Listar servidores configurados
claude mcp list

# Interface interativa
/mcp
```

### 12.5 Servidores MCP Especializados

| Servidor | Função |
|----------|--------|
| **memory-mcp** | Memória persistente baseada em grafo de conhecimento |
| **claude-context-mcp** | Busca semântica em milhões de linhas de código |
| **everything-mcp** | Servidor de referência com prompts e recursos |
| **browser-mcp** | Navegação, screenshot, clique, digitação |
| **slack-mcp** | Integração com Slack |
| **jira-mcp** | Gerenciamento de tickets Jira |
| **google-drive-mcp** | Acesso a documentos do Google Drive |

### 12.6 Exemplo Prático com Playwright

```
> Vá ao nosso site, faça login como usuário de teste e tire uma captura de tela do painel
```

O Claude usará o MCP do Playwright para automatizar o navegador e executar a tarefa.

---

## 13. Técnicas Avançadas de Uso de Ferramentas

### 13.1 Tool Search Tool

**Problema:** Carregar definições de dezenas de ferramentas consome massivamente tokens (100k+ em casos extremos), reduzindo espaço para conversação.

**Solução:** Em vez de carregar tudo antecipadamente, o Claude descobre e carrega ferramentas sob demanda.

**Impacto:**
- Redução de até 85% no consumo de tokens
- Precisão do Opus 4.5 aumentou de 79.5% para 88.1%

### 13.2 Programmatic Tool Calling

**Problema:** Cada chamada de ferramenta retorna ao contexto principal, poluindo-o com dados intermediários.

**Solução:** O Claude escreve um script Python que orquestra múltiplas chamadas. Os resultados intermediários são processados no ambiente de execução, e apenas o resultado final é retornado.

**Impacto:**
- Redução de 37% em tokens para tarefas de pesquisa complexas
- Diminui latência eliminando múltiplas passagens de inferência
- Permite lógica de orquestração explícita (loops, condicionais)

### 13.3 Tool Use Examples

**Problema:** JSON Schema define estrutura, mas não convenções de uso (formato de data, correlações entre parâmetros).

**Solução:** Fornecer exemplos concretos de chamadas de ferramentas diretamente na definição.

**Impacto:** Precisão no manuseio de parâmetros complexos aumentou de 72% para 90%.

### 13.4 Técnicas de Prompting Avançadas

| Palavra-chave | Comportamento |
|---------------|---------------|
| `think` | Raciocínio estruturado básico |
| `think hard` | Raciocínio mais profundo |
| `ultrathink` | Máxima profundidade de análise |

**Exemplo:**
```
> ultrathink how to design a scalable real-time chat application
```

---

## 14. Sistema de Plugins Claude Code

### 14.1 Conceito

Plugins são pacotes que agrupam comandos slash, agentes especializados, servidores MCP e hooks em unidades instaláveis com um único comando.

### 14.2 Comandos de Plugin

```bash
# Adicionar marketplace
/plugin marketplace add ananddtyagi/claude-code-marketplace

# Instalar plugin específico
/plugin install owner/repo

# Instalar de URL
/plugin install https://github.com/user/plugin-name

# Listar plugins instalados
/plugin list

# Informações sobre plugin
/plugin info plugin-name

# Remover plugin
/plugin remove plugin-name
```

### 14.3 Marketplaces Recomendados

| Marketplace | Descrição |
|-------------|-----------|
| `ananddtyagi/claude-code-marketplace` | Marketplace comunitário principal |
| `jmanhype/claude-code-plugins` | 19 plugins de produção |
| `kivilaid/plugin-marketplace` | 87 plugins de 10+ fontes |
| `davila7/claude-code-templates` | Templates por fluxo de trabalho |

### 14.4 Plugins Oficiais Anthropic

| Plugin | Função |
|--------|--------|
| `anthropic/pr-review` | Revisão de pull requests |
| `anthropic/security-guidance` | Orientações de segurança |
| `anthropic/claude-agent-sdk` | Desenvolvimento com Agent SDK |
| `anthropic/git-workflow` | Automação de fluxos Git |

### 14.5 Estrutura de Plugin

```
meu-plugin/
├── .claude-plugin/
│   ├── plugin.json          # Metadados (obrigatório)
│   └── marketplace.json     # Para publicação
├── commands/                # Comandos slash
├── agents/                  # Subagentes
├── skills/                  # Skills
├── hooks/                   # Hooks
├── .mcp.json               # Servidores MCP
└── README.md
```

---

# Parte V: Ambiente de Desenvolvimento

---

## 15. Extensão VS Code e Configuração de IDE

### 15.1 Instalação da Extensão

**Requisitos:**
- VS Code versão 1.98.0 ou superior
- Conta Anthropic com plano Pro ou Max

**Instalação:**
```bash
# Via linha de comando
code --install-extension anthropic.claude-code

# Via VS Code: Ctrl+Shift+X → pesquisar "Claude Code" → Instalar
```

**Marketplace:** https://marketplace.visualstudio.com/items?itemName=anthropic.claude-code

### 15.2 Configuração para Provedores Terceiros

Para usar com Amazon Bedrock ou Google Vertex AI:

```json
{
  "env": {
    "CLAUDE_CODE_USE_BEDROCK": "1",
    "AWS_REGION": "us-east-2",
    "AWS_PROFILE": "seu-perfil"
  }
}
```

Desabilitar prompt de login:
```json
{
  "claudeCode.disableLoginPrompt": true
}
```

### 15.3 Integração com JetBrains

O Claude Code possui plugin oficial para a família JetBrains (IntelliJ IDEA, PyCharm, WebStorm, etc.):
- Instalação via JetBrains Marketplace
- Funcionalidades semelhantes à extensão VS Code
- Atalhos podem conflitar com editor (ajustar em Settings > Tools > Terminal)

---

## 16. Extensões VS Code Complementares

### 16.1 Pacote Essencial (Obrigatório)

```bash
code --install-extension esbenp.prettier-vscode \
     --install-extension dbaeumer.vscode-eslint \
     --install-extension eamodio.gitlens \
     --install-extension PKief.material-icon-theme \
     --install-extension usernamehw.errorlens
```

| Extensão | Função |
|----------|--------|
| **Prettier** | Formatação automática de código |
| **ESLint** | Análise estática JavaScript/TypeScript |
| **GitLens** | Visualização avançada de histórico Git |
| **Material Icon Theme** | Ícones distintos para arquivos |
| **Error Lens** | Exibe erros inline no editor |

### 16.2 Pacote Desenvolvimento Web

```bash
code --install-extension ritwickdey.LiveServer \
     --install-extension formulahendry.auto-rename-tag \
     --install-extension bradlc.vscode-tailwindcss \
     --install-extension pranaygp.vscode-css-peek
```

### 16.3 Pacote Produtividade

```bash
code --install-extension streetsidesoftware.code-spell-checker \
     --install-extension christian-kohler.path-intellisense \
     --install-extension yzhang.markdown-all-in-one \
     --install-extension ms-azuretools.vscode-docker
```

### 16.4 Configurações Recomendadas (settings.json)

```json
{
  "editor.fontFamily": "'JetBrains Mono', 'Fira Code', monospace",
  "editor.fontSize": 14,
  "editor.fontLigatures": true,
  "editor.lineHeight": 1.6,
  "editor.tabSize": 2,
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.minimap.enabled": false,
  "editor.wordWrap": "on",
  "editor.bracketPairColorization.enabled": true,
  "editor.guides.bracketPairs": true,
  
  "terminal.integrated.fontFamily": "'JetBrainsMono Nerd Font'",
  "terminal.integrated.fontSize": 13,
  
  "files.autoSave": "onFocusChange",
  "files.trimTrailingWhitespace": true,
  "files.insertFinalNewline": true,
  
  "git.autofetch": true,
  "git.confirmSync": false,
  
  "prettier.singleQuote": true,
  "prettier.trailingComma": "es5",
  
  "workbench.iconTheme": "material-icon-theme"
}
```

---

## 17. Terminal, Shell e Ferramentas de Linha de Comando

### 17.1 Emuladores de Terminal Recomendados

| Terminal | Características | Melhor Para |
|----------|-----------------|-------------|
| **Warp** | IA integrada, blocos, colaboração | Iniciantes, colaboração |
| **Ghostty** | Rápido, nativo, leve (Zig) | Velocidade, macOS nativo |
| **iTerm2** | Máxima customização, tmux | Power users, sysadmins |
| **WezTerm** | Programável (Lua), WebGPU | Trabalho remoto |
| **kitty** | Protocolo gráfico, extensível | Imagens no terminal |
| **Alacritty** | Minimalista, GPU | Simplicidade, velocidade |

### 17.2 Configuração do Shell

**Instalar Oh-My-Zsh:**
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

**Instalar Starship (prompt moderno):**
```bash
# macOS
brew install starship

# Linux
curl -sS https://starship.rs/install.sh | sh
```

**Instalar plugins Zsh:**
```bash
# zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

**Configuração ~/.zshrc:**
```bash
# Oh-My-Zsh
export ZSH="$HOME/.oh-my-zsh"
ZSH_THEME=""  # Desabilitado para Starship

# Plugins
plugins=(git zsh-autosuggestions zsh-syntax-highlighting docker)

source $ZSH/oh-my-zsh.sh

# Starship
eval "$(starship init zsh)"

# Histórico otimizado
export HISTSIZE=1000000
export SAVEHIST=1000000
setopt HIST_IGNORE_ALL_DUPS
```

### 17.3 Homebrew e Ferramentas CLI

**Instalação Homebrew:**
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**Ferramentas Recomendadas:**
```bash
# Essenciais
brew install git node python rust go

# Utilitários modernos
brew install wget curl jq fzf ripgrep bat eza tree htop

# Desenvolvimento
brew install docker docker-compose postgresql redis

# Produtividade
brew install tmux neovim lazygit gh starship
```

---

## 18. Fontes, Temas e Personalização Visual

### 18.1 Fontes para Programação

| Fonte | Ligatures | Melhor Para |
|-------|-----------|-------------|
| **JetBrains Mono** | Sim | IDEs JetBrains, uso geral |
| **Fira Code** | Sim (extensivo) | Quem ama ligatures |
| **Cascadia Code** | Sim | Windows Terminal, VS Code |
| **Source Code Pro** | Não | Estilo neutro |
| **Iosevka** | Configurável | Personalização total |
| **Monaspace** | Sim | Recursos modernos |

### 18.2 Nerd Fonts

Nerd Fonts adicionam ícones essenciais para prompts modernos como Starship.

```bash
# macOS via Homebrew
brew tap homebrew/cask-fonts
brew install --cask font-jetbrains-mono-nerd-font
brew install --cask font-fira-code-nerd-font
```

### 18.3 Ferramentas de Produtividade

| Ferramenta | Função | Instalação |
|------------|--------|------------|
| **Raycast** | Launcher com IA | `brew install --cask raycast` |
| **Rectangle** | Gerenciamento de janelas | `brew install --cask rectangle` |
| **Maccy** | Histórico de clipboard | `brew install --cask maccy` |
| **Obsidian** | Notas em Markdown | `brew install --cask obsidian` |

---

# Parte VI: Prática e Excelência

---

## 19. Fluxos de Trabalho Práticos

### 19.1 Análise e Compreensão de Código

**Estratégia:** Primeiros 30 minutos em qualquer novo repositório.

```
# Passo 1: Visão geral
> summarize this project

# Passo 2: Estrutura
> explain the folder structure

# Passo 3: Arquitetura
> explain the main architecture patterns used here

# Passo 4: Modelos de dados
> what are the key data models?

# Passo 5: Funcionalidade específica
> find the files that handle user authentication
```

### 19.2 Desenvolvimento de Funcionalidades

**Estratégia:** Delegar código boilerplate, focar em lógica de negócios.

```
# Passo 1: Descrever tarefa
> Implement a user auth system with JWT tokens and password hashing

# Passo 2: Gerar testes
> add tests for the authentication module

# Passo 3: Documentação
> update the README with installation instructions
```

### 19.3 Correção de Bugs (Debugging)

**Estratégia:** Investigação sistemática com contexto preciso.

```
# Passo 1: Fornecer contexto do erro
> Debug this error: "TypeError: Cannot read property 'id' of undefined" @./src/user-service.js

# Passo 2: Pedir sugestões
> suggest a few ways to fix the @ts-ignore in user.ts

# Passo 3: Aplicar correção
> update user.ts to add the null check you suggested
```

### 19.4 Refatoração de Código

**Estratégia:** Modernização assistida com verificação de comportamento.

```
# Passo 1: Identificar código legado
> find deprecated API usage in our codebase

# Passo 2: Obter recomendações
> suggest how to refactor utils.js to use modern JavaScript features

# Passo 3: Aplicar e verificar
> refactor utils.js to use async/await while maintaining the same behavior
> run tests for the refactored code
```

### 19.5 Geração de Testes

**Estratégia:** Aumentar cobertura delegando criação de testes.

```
# Passo 1: Identificar código não testado
> find functions in NotificationsService.swift that are not covered by tests

# Passo 2: Gerar testes unitários
> add tests for the notification service

# Passo 3: Adicionar casos de borda
> add test cases for edge conditions in the notification service
```

### 19.6 Criação de Pull Requests

**Estratégia:** Automatizar documentação de PRs.

```
# Passo 1: Resumir mudanças
> summarize the changes I've made to the authentication module

# Passo 2: Gerar PR
> create a pr

# Passo 3: Refinar
> enhance the PR description with more context about the security improvements
```

### 19.7 Fluxo Completo de Projeto

```
┌────────────────────────────────────────────────────────────┐
│ Terminal 1: Claude Code                                    │
│ > claude                                                   │
│ (conversa e pede mudanças)                                 │
├────────────────────────────────────────────────────────────┤
│ Terminal 2: Servidor de Desenvolvimento                    │
│ > npm run dev                                              │
│ (roda o sistema para testar)                               │
├────────────────────────────────────────────────────────────┤
│ Navegador: http://localhost:3000                           │
│ (visualiza mudanças em tempo real)                         │
└────────────────────────────────────────────────────────────┘
```

---

## 20. Melhores Práticas e Modelos Mentais

### 20.1 Mentalidade Correta

| Mentalidade | Descrição |
|-------------|-----------|
| **Estagiário rápido** | Precisa de direção clara, não autonomia total |
| **Supervisão ativa** | Revisar mudanças antes de aceitar |
| **Iteração rápida** | Usar `git restore` quando abordagem falha |
| **Sessões curtas** | `/clear` entre tarefas diferentes |

### 20.2 Aceitando e Recusando Mudanças

Após cada modificação, o Claude Code mostra um diff (diferença) do que mudou:

| Entrada | Ação |
|---------|------|
| `y` ou `yes` | Aceita a mudança proposta |
| `n` ou `no` | Recusa a mudança |
| Texto livre | Faz uma pergunta ou pede explicação |
| `Escape` | Cancela a operação atual |

**Boas práticas ao revisar diffs:**
- Leia o diff completo antes de aceitar
- Verifique se não há código removido acidentalmente
- Confirme que a lógica está correta
- Em caso de dúvida, pergunte antes de aceitar

### 20.3 Práticas de Produtividade

| Prática | Implementação |
|---------|---------------|
| **Controle de versão como âncora** | Commit antes de tarefas significativas; `git restore .` para resetar |
| **Sistema de arquivos a seu favor** | Organizar contexto em arquivos, não sobrecarregar prompts |
| **Especificidade** | "Corrija o bug de login onde..." em vez de "corrija o bug" |
| **Divisão de tarefas** | Quebrar tarefas complexas em etapas numeradas |
| **Plan Mode para análise** | Usar `--permission-mode plan` para exploração segura |
| **Sessões paralelas** | tmux ou múltiplas abas para tarefas diferentes |
| **Interrupção e redirecionamento** | Escape ou Ctrl+C quando caminho incorreto |

### 20.4 Otimização de Uso

| Situação | Recomendação |
|----------|--------------|
| Nova tarefa | Execute `/clear` primeiro |
| Sessão longa | Use `/compact` para resumir contexto |
| Debug complexo | Ative Extended Thinking |
| Múltiplos arquivos | Use `@arquivo` para contexto específico |
| Tarefa recorrente | Crie comando slash personalizado |
| Custo alto | Monitore com `/cost` |

### 20.5 Padrões de Prompt Efetivos

**Estrutura recomendada para prompts complexos:**
```
[Contexto] O que o sistema faz / estado atual
[Objetivo] O que você quer alcançar
[Restrições] Limitações ou requisitos específicos
[Formato] Como você quer a resposta
```

**Exemplo:**
```
O sistema atual usa callbacks para chamadas de API.
Quero migrar para async/await mantendo compatibilidade.
Não pode quebrar os testes existentes.
Faça arquivo por arquivo, começando pelo api.js.
```

### 20.6 Workflow de Desenvolvimento Iterativo

```
┌─────────────────────────────────────────────────────────┐
│ 1. COMMIT INICIAL                                       │
│    git add . && git commit -m "checkpoint antes de X"   │
├─────────────────────────────────────────────────────────┤
│ 2. SOLICITAR MUDANÇA                                    │
│    Descrever claramente o que precisa                   │
├─────────────────────────────────────────────────────────┤
│ 3. REVISAR DIFF                                         │
│    Analisar cada alteração proposta                     │
├─────────────────────────────────────────────────────────┤
│ 4. ACEITAR OU AJUSTAR                                   │
│    y para aceitar, texto para ajustar                   │
├─────────────────────────────────────────────────────────┤
│ 5. TESTAR                                               │
│    Executar testes, verificar comportamento             │
├─────────────────────────────────────────────────────────┤
│ 6. ITERAR OU REVERTER                                   │
│    Se OK: continuar. Se não: git restore .              │
└─────────────────────────────────────────────────────────┘
```

### 20.7 Segurança

- **Sempre revise mudanças** antes de aceitar
- **Configure permissões** para negar acesso a arquivos sensíveis (.env)
- **Use Modo Plan** para explorar código novo sem riscos
- **Nunca execute** comandos que você não entende
- **Mantenha backups** via controle de versão
- **Cuidado com API keys** — nunca deixe expostas no código

---

## 21. Solução de Problemas

### 21.1 Erros Comuns da API

| Erro | Causa | Solução |
|------|-------|---------|
| `overloaded_error` | Servidor com alto tráfego | Aguardar ou mudar para Sonnet |
| `invalid_request_error` | Bug interno | Escape duas vezes para reenviar; reiniciar sessão |
| `request_timeout` | Tarefa muito complexa | Dividir em etapas menores |
| `tool_call_error` | Falha inesperada em ferramenta | Tentar novamente ou reiniciar |

### 21.2 Problemas de Instalação

| Problema | Solução |
|----------|---------|
| Erros de permissão NPM | Usar instalador nativo em vez de npm |
| IDE não detectado no WSL2 | Criar regra no Firewall do Windows para WSL2 |
| Tecla Escape não funciona (JetBrains) | Settings > Tools > Terminal > Desmarcar "Move focus to editor with Escape" |
| Alto uso de CPU | Usar `/compact` regularmente; adicionar diretórios de build ao .gitignore |
| Pesquisa lenta no WSL | Mover projeto para sistema de arquivos Linux (/home/) |

### 21.3 Limites de Uso Atingidos

- Aguardar reset (a cada 5 horas)
- Considerar upgrade para plano Max
- Usar `/cost` para monitorar consumo
- Otimizar prompts para usar menos tokens
- Usar `/compact` para comprimir contexto

### 21.4 Extensão VS Code Não Funciona

1. Verificar versão do VS Code (mínimo 1.98.0)
2. Executar "Developer: Reload Window" via Paleta de Comandos
3. Confirmar autenticação com conta Anthropic
4. Tentar usar via CLI (`claude` no terminal)
5. Reportar bug em https://github.com/anthropics/claude-code/issues

---

## 22. Referências e Recursos

### 22.1 Documentação Oficial

| Recurso | URL |
|---------|-----|
| Documentação principal | https://code.claude.com/docs |
| Referência de comandos CLI | https://code.claude.com/docs/en/cli-reference |
| Guia de modo interativo | https://code.claude.com/docs/en/interactive-mode |
| Comandos slash | https://code.claude.com/docs/en/slash-commands |
| Extensão VS Code | https://marketplace.visualstudio.com/items?itemName=anthropic.claude-code |

### 22.2 Suporte

| Canal | URL |
|-------|-----|
| Central de suporte | https://support.claude.com |
| Status do serviço | https://status.anthropic.com |
| Issues GitHub | https://github.com/anthropics/claude-code/issues |
| Discord oficial | https://discord.gg/anthropic |

### 22.3 Repositórios Úteis

| Repositório | Descrição |
|-------------|-----------|
| awesome-claude-code | Coleção de recursos e plugins |
| awesome-mcp-servers | Servidores MCP disponíveis |
| Nerd Fonts | Fontes com ícones para terminal |

### 22.4 Ferramentas Complementares

| Ferramenta | Propósito |
|------------|-----------|
| Starship | Prompt de terminal moderno |
| Oh-My-Zsh | Framework de configuração Zsh |
| Raycast | Launcher de produtividade |
| GitLens | Visualização Git no VS Code |
| Warp | Terminal com IA integrada |

---

# Apêndice A: Exemplos Práticos de Prompts e Fluxos

## A.1 Prompts para Inicialização de Projeto

### Criar CLAUDE.md Completo
```
Crie um arquivo CLAUDE.md na raiz do projeto seguindo as melhores práticas. Esse arquivo deve conter:

1. Visão geral do projeto
2. Estrutura de arquivos e o que cada um faz
3. Stack tecnológica
4. Convenções de código que devem ser seguidas
5. Comandos úteis para desenvolvimento
6. Regras específicas do projeto
7. Contexto adicional relevante

Analise os arquivos existentes para extrair informações relevantes.
```

### Análise Completa de Código
```
Analise o arquivo [nome-do-arquivo] completamente. Identifique:

1. Bugs ou erros de lógica
2. Problemas de tratamento de erro
3. Falhas de usabilidade na interface
4. Código duplicado que pode ser refatorado
5. Vulnerabilidades de segurança

Para cada problema, explique o que está errado e proponha a correção.
```

## A.2 Prompts para Melhorias Incrementais

### Tratamento de Erros Robusto
```
Melhore o tratamento de erros no JavaScript. Adicione:
- Mensagens de erro claras em português para o usuário
- Retry automático em caso de falha de rede (máximo 3 tentativas)
- Timeout de 60 segundos por requisição
- Loading spinner durante o processamento
```

### Modularização de Código
```
Extraia o JavaScript do index.html para arquivos separados em src/js/:
- config.js (configurações e constantes)
- api.js (chamadas à API)
- utils.js (funções utilitárias)
- ui.js (manipulação do DOM)
- main.js (ponto de entrada)

Mantenha o index.html funcionando com imports de módulos ES6.
```

### Melhoria de Interface
```
Melhore o CSS para uma aparência mais profissional:
- Paleta de cores coerente
- Tipografia adequada
- Cards com sombra suave
- Indicadores visuais de progresso
- Design responsivo
```

### Adicionar Funcionalidade de Exportação
```
Adicione botão para exportar o relatório completo em formato que possa ser colado no Word, incluindo:
- Dados de entrada
- Resultados processados
- Métricas relevantes
- Data e hora da execução
```

## A.3 Comandos de Manutenção do Dia a Dia

| Objetivo | Prompt Sugerido |
|----------|-----------------|
| Ver estrutura atual | `Liste todos os arquivos do projeto e descreva cada um` |
| Desfazer última mudança | `Desfaça a última modificação que você fez` |
| Explicar código | `Explique como funciona a função X no arquivo Y` |
| Otimizar performance | `Otimize o arquivo X para melhor performance` |
| Documentar código | `Adicione comentários explicativos no arquivo X` |
| Criar testes | `Crie testes unitários para as funções do arquivo X` |
| Refatorar | `Refatore o arquivo X seguindo padrões SOLID` |
| Debugar | `O erro Y está ocorrendo. Analise e corrija.` |

## A.4 Configurações Recomendadas para CLAUDE.md

### Seção de Comandos Bash
```markdown
# Bash commands
- npm run build: Build the project
- npm run typecheck: Run the typechecker
- npm run test: Run test suite
- npm run lint: Run linter
```

### Seção de Code Style
```markdown
# Code style
- Use ES modules (import/export) syntax, not CommonJS (require)
- Destructure imports when possible (eg. import { foo } from 'bar')
- Use TypeScript strict mode
- Follow naming conventions: camelCase for variables, PascalCase for classes
```

### Seção de Workflow
```markdown
# Workflow
- Be sure to typecheck when you're done making a series of code changes
- Prefer running single tests, and not the whole test suite, for performance
- Always run linter before committing
- Use conventional commits format
```

## A.5 Fluxo de Trabalho Completo para Novo Projeto

### Fase 1: Inicialização
```bash
# Terminal 1: Abrir Claude Code
cd /caminho/do/projeto
claude

# Primeiro comando no Claude Code
/init
```

### Fase 2: Análise e Diagnóstico
```
Analise este projeto completamente. Liste:
1. Arquitetura atual
2. Problemas críticos identificados
3. Oportunidades de melhoria
4. Dependências desatualizadas
```

### Fase 3: Planejamento (Modo Plan)
```
# Pressione Shift+Tab duas vezes para entrar no Modo Plan

Crie um plano de refatoração para este projeto em 5 etapas, 
priorizando por impacto e risco. Para cada etapa, liste:
- O que será alterado
- Arquivos afetados
- Testes necessários
- Riscos potenciais
```

### Fase 4: Execução Incremental
```
# Volte ao Modo Edit (Shift+Tab)
# Execute uma melhoria de cada vez

Implemente a etapa 1 do plano de refatoração.
Após concluir, execute os testes para validar.
```

### Fase 5: Validação e Documentação
```
Atualize o README.md com:
- Instruções de instalação
- Como executar o projeto
- Como rodar os testes
- Arquitetura do sistema
- Contribuindo com o projeto
```

## A.6 Exemplo: Fluxo com Live Server

Para projetos web que precisam de servidor de desenvolvimento:

```
┌────────────────────────────────────────────────────────────┐
│ Terminal 1: Claude Code                                    │
│ > claude                                                   │
│ (conversa e pede mudanças)                                 │
├────────────────────────────────────────────────────────────┤
│ Terminal 2: Servidor de Desenvolvimento                    │
│ > npm run dev                                              │
│ ou                                                         │
│ > npx live-server                                          │
│ (roda o sistema para testar)                               │
├────────────────────────────────────────────────────────────┤
│ Navegador: http://localhost:3000                           │
│ (visualiza mudanças em tempo real)                         │
└────────────────────────────────────────────────────────────┘
```

**Workflow:**
1. Faça uma solicitação no Terminal 1 (Claude Code)
2. Claude Code mostra o diff das mudanças
3. Digite `y` para aceitar ou `n` para recusar
4. Live Server atualiza automaticamente
5. Verifique o resultado no navegador
6. Repita ou ajuste conforme necessário

## A.7 Criando Casos de Teste

```
Crie um arquivo tests/test-cases.json com casos de teste para validar:

1. Cenário de sucesso com entrada válida
2. Cenário com entrada vazia
3. Cenário com entrada inválida
4. Cenário de timeout/erro de rede
5. Cenário de limite (strings muito longas, caracteres especiais)

Inclua para cada caso:
- Descrição do teste
- Dados de entrada
- Resultado esperado
- Critério de aceitação
```

---

# Apêndice B: Comandos de Referência Rápida

## Sessão
```bash
claude                    # Nova sessão
claude "prompt"           # Sessão com prompt inicial
claude -c                 # Continuar última sessão
claude -r "id"            # Retomar sessão específica
claude -p "prompt"        # Consulta única (print mode)
```

## Slash Commands Principais
```
/init                     # Inicializar projeto
/clear                    # Limpar contexto
/compact                  # Comprimir histórico
/cost                     # Ver uso de tokens
/model                    # Alterar modelo
/review                   # Revisão de código
/help                     # Ajuda
/plugin                   # Gerenciar plugins
/mcp                      # Gerenciar servidores MCP
/agents                   # Gerenciar subagentes
```

## Notação Especial
```
@arquivo.js               # Incluir arquivo
@src/file.js#L10-50       # Linhas específicas
@./src/                   # Diretório recursivo
@**/*.test.ts             # Padrão glob
#texto                    # Adicionar à memória
!comando                  # Executar shell
```

## Atalhos
```
Ctrl+C                    # Cancelar
Ctrl+D                    # Sair
Ctrl+L                    # Limpar tela
Shift+Tab                 # Alternar modo
Escape+Escape             # Retroceder mensagem
Ctrl+R                    # Histórico de prompts
```

---

# Apêndice C: Template CLAUDE.md

```markdown
# [Nome do Projeto]

## Visão Geral
[Breve descrição do propósito e funcionalidade principal]

## Stack Tecnológica
- Frontend: [frameworks, bibliotecas]
- Backend: [linguagem, frameworks]
- Banco de Dados: [tipo, nome]
- Deploy: [plataforma, ferramentas]

## Comandos Comuns
- `[comando]`: [descrição]
- `[comando]`: [descrição]
- `[comando]`: [descrição]

## Convenções de Código
- [convenção 1]
- [convenção 2]
- [convenção 3]

## Estrutura de Diretórios
- `src/`: Código fonte principal
- `tests/`: Testes automatizados
- `docs/`: Documentação

## Regras Específicas
- Sempre faça: [regra]
- Nunca faça: [regra]
- Prefira: [padrão]

## Referências
- Documentação: @docs/README.md
- Arquitetura: @docs/architecture.md
```

---

# Apêndice D: Script de Configuração Automatizada

```bash
#!/bin/bash
# setup-claude-dev-environment.sh

set -e
echo "🚀 Configurando ambiente de desenvolvimento Claude Code..."

# 1. Homebrew
if ! command -v brew &> /dev/null; then
    echo "📦 Instalando Homebrew..."
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    eval "$(/opt/homebrew/bin/brew shellenv)"
fi

# 2. Ferramentas CLI
echo "🔧 Instalando ferramentas CLI..."
brew install git node python starship fzf ripgrep bat eza gh lazygit

# 3. Oh-My-Zsh
if [ ! -d "$HOME/.oh-my-zsh" ]; then
    echo "🐚 Instalando Oh-My-Zsh..."
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended
fi

# 4. Plugins Zsh
echo "🔌 Instalando plugins Zsh..."
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions 2>/dev/null || true
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting 2>/dev/null || true

# 5. Aplicativos
echo "🖥️ Instalando aplicativos..."
brew install --cask visual-studio-code warp raycast rectangle

# 6. Fontes
echo "🔤 Instalando fontes..."
brew tap homebrew/cask-fonts
brew install --cask font-jetbrains-mono-nerd-font

# 7. Extensões VS Code
echo "📝 Instalando extensões VS Code..."
code --install-extension anthropic.claude-code
code --install-extension esbenp.prettier-vscode
code --install-extension dbaeumer.vscode-eslint
code --install-extension eamodio.gitlens
code --install-extension PKief.material-icon-theme
code --install-extension usernamehw.errorlens

# 8. Configurar Starship
echo "⭐ Configurando Starship..."
mkdir -p ~/.config
cat > ~/.config/starship.toml << 'EOF'
add_newline = true
[character]
success_symbol = "[❯](bold green)"
error_symbol = "[❯](bold red)"
EOF

echo "✅ Configuração concluída!"
echo "🔄 Reinicie o terminal para aplicar as mudanças."
```

---

**Documento compilado em Janeiro de 2026**  
**Fontes:** Documentação oficial Anthropic, guias da comunidade e melhores práticas de usuários avançados.

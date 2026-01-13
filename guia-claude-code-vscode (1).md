# Guia Completo: Claude Code no Visual Studio Code

## O Que é o Claude Code?

O Claude Code é uma ferramenta de codificação agêntica desenvolvida pela Anthropic que funciona como um assistente de programação conversacional. Diferente de ferramentas de autocomplete como GitHub Copilot, o Claude Code opera como um agente completo capaz de ler arquivos, executar comandos, gerenciar contexto e fazer commits no Git.

A ferramenta pode ser usada de duas formas principais:
- **Extensão nativa do Visual Studio Code** (recomendada para iniciantes)
- **Interface de linha de comando** no terminal integrado

---

## Requisitos e Planos de Assinatura

### Requisitos Técnicos
- Visual Studio Code versão 1.98.0 ou superior
- Conta Anthropic (criada durante a primeira abertura da extensão)
- Assinatura Claude Pro ou Max (ou créditos de acesso via Interface de Programação de Aplicações)

### Planos Disponíveis

| Plano | Preço | Uso do Claude Code | Observações |
|-------|-------|-------------------|-------------|
| Free | Gratuito | Não disponível | Apenas chat básico |
| Pro | 20 dólares por mês | Sim | 5x mais uso que o Free |
| Max 5x | 100 dólares por mês | Sim | 5x mais uso que o Pro, acesso ao Opus |
| Max 20x | 200 dólares por mês | Sim | 20x mais uso que o Pro, sem restrições |

**Importante:** Os limites de uso são resetados a cada 5 horas e são compartilhados entre Claude web, desktop, mobile e Claude Code.

---

## Instalação da Extensão

### Método 1: Via Visual Studio Code
1. Pressione `Command + Shift + X` no Mac ou `Control + Shift + X` no Windows/Linux
2. Pesquise por "Claude Code"
3. Localize a extensão oficial da Anthropic
4. Clique em "Install"
5. Reinicie o Visual Studio Code se necessário

### Método 2: Via Marketplace
Acesse diretamente: https://marketplace.visualstudio.com/items?itemName=anthropic.claude-code

### Após a Instalação
Execute "Developer: Reload Window" pela Paleta de Comandos (`Command + Shift + P` ou `Control + Shift + P`) se a extensão não aparecer imediatamente.

---

## Primeiros Passos

### Abrindo o Claude Code

Existem várias formas de abrir a interface:

| Método | Ação |
|--------|------|
| Ícone Spark | Clique no ícone de faísca no canto superior direito do editor |
| Barra Lateral | Clique no ícone do Claude na Activity Bar |
| Paleta de Comandos | `Command + Shift + P`, digite "Claude Code", selecione "Open in New Tab" |
| Atalho Direto | `Command + Escape` no Mac ou `Control + Escape` no Windows/Linux |

### Inicializando um Projeto

Execute o comando `/init` na primeira vez que usar Claude Code em um projeto. Isso irá:
- Analisar sua base de código automaticamente
- Criar um arquivo `CLAUDE.md` com contexto do projeto
- Identificar comandos de build, estrutura de pastas e convenções

```
/init
```

O arquivo gerado serve como "memória persistente" que o Claude carrega em toda sessão.

---

## Modos de Operação

O Claude Code possui três modos principais, alternados com `Shift + Tab`:

### Modo Edit (Padrão)
- Requer aprovação antes de modificar arquivos
- Exibe diffs para revisão
- Ideal para tarefas críticas

### Modo Auto-accept
- Aplica mudanças automaticamente
- Mais ágil para tarefas de menor risco
- Use com cautela em código de produção

### Modo Plan
- Cria planos de ação sem modificar código
- Perfeito para pesquisa e arquitetura
- Permite revisar e editar planos antes da execução

**Ciclo:** Edit → Auto-accept → Plan → Edit (via `Shift + Tab`)

---

## Atalhos de Teclado Essenciais

### Controles Gerais

| Atalho | Função |
|--------|--------|
| `Control + C` | Cancela entrada ou geração atual |
| `Control + D` | Sai da sessão |
| `Control + L` | Limpa a tela do terminal |
| Seta para Cima/Baixo | Navega histórico de comandos |
| `Escape + Escape` | Retrocede para mensagem anterior |
| `Tab` | Autocomplete |
| `Shift + Tab` | Alterna modos (Edit/Auto-accept/Plan) |

### Edição de Texto (estilo Bash)

| Atalho | Função |
|--------|--------|
| `Control + A` | Vai para início da linha |
| `Control + E` | Vai para fim da linha |
| `Option + F` (Mac) | Avança uma palavra |
| `Option + B` (Mac) | Retrocede uma palavra |
| `Control + W` | Deleta palavra anterior |

### Entrada Multilinha
- Barra invertida + Enter funciona universalmente
- `Option + Enter` cria nova linha no Mac
- `Shift + Enter` funciona após executar `/terminal-setup`

---

## Comandos Slash Principais

### Comandos de Sessão

| Comando | Descrição |
|---------|-----------|
| `/clear` | Limpa histórico de conversa e contexto |
| `/compact [instruções]` | Compacta conversa com foco opcional |
| `/exit` | Sai do modo interativo |
| `/help` | Mostra comandos disponíveis |

### Comandos de Projeto

| Comando | Descrição |
|---------|-----------|
| `/init` | Inicializa projeto com arquivo de memória |
| `/add-dir` | Adiciona diretórios de trabalho |
| `/memory` | Edita arquivos de memória |
| `/review` | Solicita revisão de código |
| `/todos` | Lista itens pendentes da conversa |

### Comandos de Configuração

| Comando | Descrição |
|---------|-----------|
| `/config` | Abre interface de configurações |
| `/model` | Seleciona ou altera o modelo de inteligência artificial |
| `/permissions` | Visualiza ou atualiza permissões |
| `/doctor` | Verifica saúde da instalação |
| `/cost` | Mostra estatísticas de uso de tokens |

### Comandos de Integração

| Comando | Descrição |
|---------|-----------|
| `/ide` | Gerencia integrações com ambientes de desenvolvimento |
| `/mcp` | Gerencia conexões com servidores do Model Context Protocol |
| `/install-github-app` | Configura ações do GitHub para repositório |

---

## Notação Especial na Entrada

### Referências de Arquivo
Use `@` para incluir conteúdo de arquivos no contexto:
```
@src/main.py Revise e melhore o tratamento de erros
```

Funciona com caminhos relativos e linhas específicas:
```
@src/utils/helpers.js#L10-50
```

### Memória Rápida
Use `#` no início da linha para adicionar ao arquivo de memória:
```
#Este projeto usa convenções de nomenclatura camelCase
```

### Comandos Shell Diretos
Use `!` para executar comandos sem processamento conversacional:
```
!git status
!npm test
```

---

## Sistema de Memória

### Hierarquia de Arquivos de Memória

O Claude Code carrega memórias em ordem de prioridade:

1. **Memória de Usuário:** `~/.claude/CLAUDE.md` (aplica a todos projetos)
2. **Memória de Projeto:** `./CLAUDE.md` ou `./.claude/CLAUDE.md` (compartilhada via git)
3. **Memória Local:** `CLAUDE.local.md` (pessoal, ignorada pelo git)
4. **Regras Condicionais:** `.claude/rules/` (regras por tipo de arquivo)

### Estrutura Recomendada do CLAUDE.md

```markdown
# Visão Geral do Projeto
Breve descrição do que o projeto faz.

# Comandos Comuns
- `npm run dev`: Inicia servidor de desenvolvimento
- `npm test`: Executa testes
- `npm run build`: Gera build de produção

# Convenções de Código
- Use TypeScript com tipagem estrita
- Siga padrões de nomenclatura camelCase
- Testes devem estar no diretório __tests__

# Arquitetura
Referência @docs/architecture.md para detalhes completos.
```

### Boas Práticas para Memória

**Faça:**
- Mantenha instruções concisas e específicas
- Use referências `@arquivo.md` para conteúdo extenso
- Documente comandos que você usa repetidamente
- Inclua convenções únicas do projeto

**Evite:**
- Instruções genéricas como "escreva código limpo"
- Sobrecarregar com todas as informações possíveis
- Duplicar informação que pode ser descoberta automaticamente
- Instruções contraditórias

---

## Comandos Slash Personalizados

### Criando Comandos de Projeto
Comandos compartilhados com a equipe via git:

```bash
mkdir -p .claude/commands
echo "Analise este código em busca de problemas de performance:" > .claude/commands/optimize.md
```

Uso: `/optimize`

### Criando Comandos Pessoais
Comandos disponíveis em todos seus projetos:

```bash
mkdir -p ~/.claude/commands
echo "Revise este código para vulnerabilidades de segurança:" > ~/.claude/commands/security.md
```

### Usando Argumentos

Crie um arquivo `.claude/commands/fix-issue.md`:
```markdown
---
description: Corrige uma issue específica
argument-hint: [número-da-issue]
---

Corrija a issue #$ARGUMENTS seguindo nossos padrões de código.
```

Uso: `/fix-issue 123`

### Frontmatter Avançado

```markdown
---
allowed-tools: Bash(git *), Read, Write
description: Cria um commit git
model: claude-sonnet-4-20250514
---

Analise as mudanças e crie um commit com mensagem descritiva.
```

---

## Configurações e Permissões

### Localização dos Arquivos de Configuração

| Arquivo | Escopo | Localização |
|---------|--------|-------------|
| Configurações de Usuário | Todos projetos | `~/.claude/settings.json` |
| Configurações de Projeto | Equipe | `.claude/settings.json` |
| Configurações Locais | Pessoal | `.claude/settings.local.json` |

### Exemplo de Configuração

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
  }
}
```

### Configuração para Provedores Terceiros

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

E desabilite o prompt de login no Visual Studio Code:
```json
{
  "claudeCode.disableLoginPrompt": true
}
```

---

## Model Context Protocol (Servidores de Contexto)

### O Que São Servidores do Model Context Protocol
Servidores do Model Context Protocol estendem as capacidades do Claude Code com ferramentas externas como automação de navegador, acesso a bancos de dados e integrações com ferramentas de projeto.

### Adicionando Servidores

```bash
claude mcp add github -- npx -y @modelcontextprotocol/server-github
claude mcp add playwright -- npx -y @playwright/mcp@latest
```

### Configuração via arquivo JSON

Adicione ao seu `settings.json`:

```json
{
  "mcpServers": {
    "playwright": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@playwright/mcp@latest"],
      "env": {}
    }
  }
}
```

### Gerenciamento

```bash
claude mcp list                    # Lista servidores configurados
/mcp                               # Interface interativa de gerenciamento
```

---

## Fluxo de Trabalho Recomendado

### Para Iniciantes

1. **Instale a extensão** do Visual Studio Code
2. **Execute `/init`** no seu primeiro projeto
3. **Revise e ajuste** o `CLAUDE.md` gerado
4. **Use o Modo Plan** (`Shift + Tab` 2x) para tarefas complexas
5. **Comece com Modo Edit** para ter controle sobre mudanças
6. **Use `/clear` frequentemente** ao iniciar novas tarefas

### Otimização de Uso

| Situação | Recomendação |
|----------|--------------|
| Nova tarefa | Execute `/clear` primeiro |
| Sessão longa | Use `/compact` para resumir contexto |
| Debug complexo | Ative Extended Thinking no canto inferior direito |
| Múltiplos arquivos | Use `@arquivo` para contexto específico |
| Tarefa recorrente | Crie comando slash personalizado |

### Continuando Sessões

```bash
claude --continue          # Continua última sessão
claude -c                  # Atalho
claude --resume abc123     # Retoma sessão específica
```

---

## Resolução de Problemas

### Extensão Não Instala
- Verifique se o Visual Studio Code está na versão 1.98.0 ou superior
- Confirme permissões para instalar extensões
- Tente instalar diretamente pelo site do Marketplace

### Claude Code Não Responde
1. Verifique sua conexão com a internet
2. Inicie uma nova conversa com `/clear`
3. Tente usar via linha de comando: `claude` no terminal
4. Reporte bug em https://github.com/anthropics/claude-code/issues

### Limites de Uso Atingidos
- Aguarde o reset (a cada 5 horas)
- Considere upgrade para plano Max
- Use `/cost` para monitorar consumo
- Otimize prompts para usar menos tokens

### Integração com Ambiente de Desenvolvimento Não Funciona
Execute na Paleta de Comandos:
```
Shell Command: Install 'code' command in PATH
```

---

## Recursos Oficiais

### Documentação
- Documentação principal: https://code.claude.com/docs
- Referência de comandos: https://code.claude.com/docs/en/cli-reference
- Guia de modo interativo: https://code.claude.com/docs/en/interactive-mode
- Comandos slash: https://code.claude.com/docs/en/slash-commands

### Extensão
- Visual Studio Code Marketplace: https://marketplace.visualstudio.com/items?itemName=anthropic.claude-code

### Suporte
- Central de suporte: https://support.claude.com
- Status do serviço: https://status.anthropic.com
- Issues no GitHub: https://github.com/anthropics/claude-code/issues

---

## Dicas Finais para Iniciantes

1. **Trate o Claude Code como um desenvolvedor júnior** que precisa de direção clara, não como uma ferramenta mágica

2. **Use o Modo Plan antes de executar** tarefas complexas para revisar a abordagem

3. **Mantenha sessões curtas e focadas** usando `/clear` entre tarefas diferentes

4. **Crie comandos personalizados** para tarefas que você repete frequentemente

5. **Revise sempre os diffs** antes de aceitar mudanças, especialmente em código de produção

6. **Combine com controle de versão** para poder reverter mudanças facilmente

7. **Monitore seus custos** com `/cost` para entender seu padrão de uso

8. **A extensão do Visual Studio Code é mais amigável** para iniciantes que a linha de comando

---

*Guia compilado em janeiro de 2026 com base na documentação oficial da Anthropic e melhores práticas da comunidade.*

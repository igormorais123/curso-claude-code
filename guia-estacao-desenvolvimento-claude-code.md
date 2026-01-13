# Guia Completo: Configuração de Estação de Desenvolvimento com Claude Code e VS Code

**Versão:** Janeiro 2026  
**Objetivo:** Configurar uma estação de trabalho otimizada para desenvolvimento com inteligência artificial

---

## Sumário

1. [Extensão Claude Code para VS Code](#1-extensão-claude-code-para-vs-code)
2. [Sistema de Plugins Claude Code](#2-sistema-de-plugins-claude-code)
3. [Servidores MCP Essenciais](#3-servidores-mcp-essenciais)
4. [Extensões VS Code Fundamentais](#4-extensões-vs-code-fundamentais)
5. [Terminal e Shell](#5-terminal-e-shell)
6. [Fontes para Programação](#6-fontes-para-programação)
7. [Gerenciador de Pacotes](#7-gerenciador-de-pacotes)
8. [Ferramentas de Produtividade](#8-ferramentas-de-produtividade)
9. [Script de Instalação Automatizada](#9-script-de-instalação-automatizada)
10. [Configurações Recomendadas](#10-configurações-recomendadas)

---

## 1. Extensão Claude Code para VS Code

### Requisitos
- VS Code versão 1.98.0 ou superior
- Assinatura Claude Pro ou Max
- Conta Anthropic

### Instalação
```bash
# Via linha de comando
code --install-extension anthropic.claude-code

# Ou via VS Code: Ctrl+Shift+X → pesquisar "Claude Code" → Instalar
```

### Primeiro Uso
```bash
# Após instalar, executar no projeto:
/init
```

O comando `/init` gera o arquivo `CLAUDE.md` com a memória do projeto.

### Atalhos Essenciais

| Atalho | Função |
|--------|--------|
| `Cmd+Escape` (Mac) / `Ctrl+Escape` (Win) | Abrir Claude Code |
| `Shift+Tab` | Alternar entre modos (Edit, Auto-accept, Plan) |
| `Ctrl+C` | Cancelar operação |
| `Ctrl+D` | Encerrar sessão |
| `Esc+Esc` | Retroceder para mensagem anterior |
| `Ctrl+R` | Histórico pesquisável de prompts |

### Modos de Operação

| Modo | Comportamento |
|------|---------------|
| **Edit Mode** | Requer aprovação antes de modificar arquivos |
| **Auto-accept Mode** | Aplica mudanças automaticamente |
| **Plan Mode** | Cria planos de ação sem modificar código |

### Comandos de Barra Essenciais

**Sessão:**
- `/clear` — Limpa contexto (usar frequentemente entre tarefas)
- `/compact` — Compacta histórico (usar com cautela)
- `/cost` — Mostra custos da sessão

**Projeto:**
- `/init` — Gera arquivo CLAUDE.md
- `/memory` — Edita memória do projeto
- `/review` — Revisão de código
- `/todos` — Lista tarefas pendentes

**Configuração:**
- `/model` — Alterna modelo
- `/permissions` — Gerencia permissões
- `/doctor` — Diagnóstico de problemas
- `/plugin` — Gerencia plugins

### Notação Especial

| Sintaxe | Função |
|---------|--------|
| `@arquivo.js` | Inclui arquivo no contexto |
| `@src/file.js#L10-50` | Referencia linhas específicas |
| `#texto` | Adiciona ao CLAUDE.md |
| `!comando` | Executa comando shell |

---

## 2. Sistema de Plugins Claude Code

### Conceito
Plugins são pacotes que agrupam comandos slash, agentes especializados, servidores MCP e hooks em unidades instaláveis.

### Instalação de Plugins
```bash
# Adicionar marketplace
/plugin marketplace add ananddtyagi/claude-code-marketplace

# Instalar plugin específico
/plugin install owner/repo

# Instalar de URL
/plugin install https://github.com/user/plugin-name

# Listar plugins instalados
/plugin list

# Remover plugin
/plugin remove plugin-name
```

### Marketplaces Recomendados

| Marketplace | Descrição |
|-------------|-----------|
| `ananddtyagi/claude-code-marketplace` | Marketplace comunitário principal |
| `jmanhype/claude-code-plugins` | 19 plugins de produção para trading, swarm e automação GitHub |
| `kivilaid/plugin-marketplace` | 87 plugins de 10+ fontes |
| `davila7/claude-code-templates` | Templates por fluxo de trabalho |

### Plugins Oficiais Anthropic

| Plugin | Função |
|--------|--------|
| `anthropic/pr-review` | Revisão de pull requests |
| `anthropic/security-guidance` | Orientações de segurança |
| `anthropic/claude-agent-sdk` | Desenvolvimento com Agent SDK |
| `anthropic/git-workflow` | Automação de fluxos Git |

### Estrutura de Plugin
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

## 3. Servidores MCP Essenciais

MCP (Model Context Protocol) estende as capacidades do Claude Code conectando-o a ferramentas externas.

### Instalação de Servidores MCP
```bash
# GitHub - Integração completa com repositórios
claude mcp add github -- npx -y @modelcontextprotocol/server-github

# Playwright - Automação de browser
claude mcp add playwright -- npx -y @playwright/mcp@latest

# PostgreSQL - Consultas em linguagem natural
claude mcp add postgres -- npx -y @modelcontextprotocol/server-postgres

# SQLite - Gerenciamento de banco de dados
claude mcp add sqlite -- npx -y @modelcontextprotocol/server-sqlite

# Sistema de arquivos - Operações avançadas
claude mcp add filesystem -- npx -y @modelcontextprotocol/server-filesystem

# Supabase - Integração oficial
claude mcp add supabase -- npx -y @supabase/mcp-server
```

### Repositórios de Servidores MCP

| Repositório | Descrição |
|-------------|-----------|
| `awesome-mcp-servers` | Coleção principal de servidores MCP |
| `wong2/awesome-mcp-servers` | Coleção alternativa |
| `awesome-dxt-mcp` | Extensões desktop e MCP |
| `awesome-mcp-clients` | Implementações de clientes MCP |

### Servidores MCP Especializados

| Servidor | Função |
|----------|--------|
| `memory-mcp` | Memória persistente baseada em grafo de conhecimento |
| `claude-context-mcp` | Busca semântica em milhões de linhas |
| `everything-mcp` | Servidor de referência com prompts e recursos |
| `browser-mcp` | Navegação, screenshot, clique, digitação |

---

## 4. Extensões VS Code Fundamentais

### Pacote Essencial (Obrigatório)
```bash
# Instalar todas de uma vez
code --install-extension esbenp.prettier-vscode \
     --install-extension dbaeumer.vscode-eslint \
     --install-extension eamodio.gitlens \
     --install-extension PKief.material-icon-theme \
     --install-extension usernamehw.errorlens
```

| Extensão | Função |
|----------|--------|
| **Prettier** | Formatação automática de código |
| **ESLint** | Análise estática e correção de erros JavaScript/TypeScript |
| **GitLens** | Visualização avançada de histórico Git, blame inline |
| **Material Icon Theme** | Ícones distintos para tipos de arquivo |
| **Error Lens** | Exibe erros e avisos inline no editor |

### Pacote Desenvolvimento Web
```bash
code --install-extension ritwickdey.LiveServer \
     --install-extension formulahendry.auto-rename-tag \
     --install-extension bradlc.vscode-tailwindcss \
     --install-extension pranaygp.vscode-css-peek
```

| Extensão | Função |
|----------|--------|
| **Live Server** | Servidor local com recarga automática |
| **Auto Rename Tag** | Renomeia tags HTML/XML automaticamente |
| **Tailwind CSS IntelliSense** | Autocompletar classes Tailwind |
| **CSS Peek** | Navegação para definições CSS |

### Pacote Produtividade
```bash
code --install-extension streetsidesoftware.code-spell-checker \
     --install-extension christian-kohler.path-intellisense \
     --install-extension yzhang.markdown-all-in-one \
     --install-extension ms-azuretools.vscode-docker
```

| Extensão | Função |
|----------|--------|
| **Code Spell Checker** | Verificação ortográfica em código e comentários |
| **Path Intellisense** | Autocompletar caminhos de arquivo |
| **Markdown All in One** | Ferramentas completas para Markdown |
| **Docker** | Gerenciamento de containers no VS Code |

### Pacote Testes e Debug
```bash
code --install-extension Orta.vscode-jest \
     --install-extension ms-vscode.test-adapter-converter \
     --install-extension humao.rest-client
```

| Extensão | Função |
|----------|--------|
| **Jest** | Execução e debug de testes Jest |
| **Test Adapter** | Integração com frameworks de teste |
| **REST Client** | Testar APIs diretamente no VS Code |

### Extensões de Inteligência Artificial Complementares

| Extensão | Função |
|----------|--------|
| **Continue** | Framework open-source para múltiplos modelos |
| **Cody** | Busca semântica multi-repositório (Sourcegraph) |
| **TabNine** | Autocompletar com IA (alternativa gratuita) |
| **Codeium** | Assistente de código gratuito |

---

## 5. Terminal e Shell

### Emuladores de Terminal Recomendados

| Terminal | Plataforma | Características |
|----------|------------|-----------------|
| **Warp** | macOS, Linux (beta) | IA integrada, blocos, colaboração, moderno |
| **Ghostty** | macOS, Linux | Rápido, nativo, leve, suporte a Kitty Graphics |
| **iTerm2** | macOS | Integração tmux, máxima customização, maduro |
| **WezTerm** | Multiplataforma | Programável em Lua, WebGPU, mux remoto |
| **kitty** | Multiplataforma | Protocolo gráfico próprio, rico ecossistema |
| **Alacritty** | Multiplataforma | Minimalista, aceleração GPU, mais rápido |
| **Windows Terminal** | Windows | Nativo Microsoft, tabs, perfis |

### Recomendação por Perfil

| Perfil | Escolha |
|--------|---------|
| Iniciante querendo IA | Warp |
| Usuário macOS nativo | Ghostty |
| Power user tmux | iTerm2 |
| Programador de terminal | WezTerm |
| Minimalista | Alacritty |

### Instalação via Homebrew (macOS)
```bash
# Warp
brew install --cask warp

# Ghostty
brew install --cask ghostty

# iTerm2
brew install --cask iterm2

# WezTerm
brew install --cask wezterm

# Alacritty
brew install --cask alacritty
```

### Configuração do Shell (Zsh + Starship)

#### Instalar Oh-My-Zsh
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

#### Instalar Starship (Prompt Moderno)
```bash
# macOS
brew install starship

# Linux
curl -sS https://starship.rs/install.sh | sh
```

#### Configurar ~/.zshrc
```bash
# Oh-My-Zsh
export ZSH="$HOME/.oh-my-zsh"
ZSH_THEME=""  # Desabilitar tema (Starship assume)

# Plugins essenciais
plugins=(
  git
  zsh-autosuggestions
  zsh-syntax-highlighting
  docker
  kubectl
)

source $ZSH/oh-my-zsh.sh

# Starship
eval "$(starship init zsh)"

# Histórico otimizado
export HISTSIZE=1000000
export SAVEHIST=1000000
setopt HIST_IGNORE_ALL_DUPS
setopt HIST_FIND_NO_DUPS
setopt HIST_REDUCE_BLANKS
```

#### Instalar Plugins Zsh
```bash
# zsh-autosuggestions (sugestões baseadas em histórico)
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# zsh-syntax-highlighting (cores para comandos válidos/inválidos)
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

#### Configurar Starship (~/.config/starship.toml)
```toml
# Adiciona linha em branco entre prompts
add_newline = true

# Timeout para comandos
command_timeout = 10000

[character]
success_symbol = "[❯](bold green)"
error_symbol = "[❯](bold red)"

[directory]
truncation_length = 3
truncate_to_repo = true

[git_branch]
symbol = " "
format = "on [$symbol$branch]($style) "

[git_status]
format = '([$all_status$ahead_behind]($style) )'

[nodejs]
format = "via [ $version](bold green) "

[python]
format = 'via [${symbol}${pyenv_prefix}(${version} )]($style)'

[docker_context]
format = "via [ $context](blue bold) "

[time]
disabled = false
format = '[\[ $time \]]($style) '
```

---

## 6. Fontes para Programação

### Fontes Recomendadas

| Fonte | Ligatures | Melhor Para |
|-------|-----------|-------------|
| **JetBrains Mono** | Sim | IDEs JetBrains, uso geral |
| **Fira Code** | Sim (extensivo) | Quem ama ligatures |
| **Cascadia Code** | Sim | Windows Terminal, VS Code |
| **Source Code Pro** | Não | Estilo neutro, Adobe |
| **Iosevka** | Configurável | Quem quer personalização total |
| **Monaspace** | Sim | Recursos modernos (texture healing) |
| **Hack** | Não | Clareza máxima |

### Nerd Fonts (Obrigatório para Starship)

Nerd Fonts adicionam ícones (Git, linguagens, sistemas) às fontes. Necessário para prompts modernos.

```bash
# macOS via Homebrew
brew tap homebrew/cask-fonts
brew install --cask font-jetbrains-mono-nerd-font
brew install --cask font-fira-code-nerd-font
brew install --cask font-cascadia-code-nerd-font

# Ou baixar manualmente de:
# https://www.nerdfonts.com/font-downloads
```

### Configuração no VS Code (settings.json)
```json
{
  "editor.fontFamily": "'JetBrains Mono', 'Fira Code', monospace",
  "editor.fontSize": 14,
  "editor.fontLigatures": true,
  "editor.lineHeight": 1.6,
  "terminal.integrated.fontFamily": "'JetBrainsMono Nerd Font'",
  "terminal.integrated.fontSize": 13
}
```

---

## 7. Gerenciador de Pacotes

### Homebrew (macOS e Linux)

#### Instalação
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

#### Configurar PATH (adicionar ao ~/.zshrc)
```bash
# Apple Silicon
eval "$(/opt/homebrew/bin/brew shellenv)"

# Intel Mac
eval "$(/usr/local/bin/brew shellenv)"
```

#### Comandos Essenciais

| Comando | Função |
|---------|--------|
| `brew install pacote` | Instalar pacote CLI |
| `brew install --cask app` | Instalar aplicativo GUI |
| `brew upgrade` | Atualizar todos os pacotes |
| `brew cleanup` | Remover versões antigas |
| `brew doctor` | Diagnosticar problemas |
| `brew list` | Listar instalados |
| `brew search termo` | Pesquisar pacotes |
| `brew services list` | Listar serviços |
| `brew bundle dump` | Exportar Brewfile |
| `brew bundle install` | Instalar de Brewfile |

### Pacotes Homebrew Recomendados para Desenvolvedores
```bash
# Ferramentas essenciais
brew install git node python rust go

# Utilitários de terminal
brew install wget curl jq fzf ripgrep bat eza tree htop

# Desenvolvimento
brew install docker docker-compose postgresql redis

# Qualidade de código
brew install shellcheck hadolint

# Produtividade
brew install tmux neovim lazygit gh
```

### Brewfile (para backup e reprodução)
```ruby
# Brewfile
tap "homebrew/cask-fonts"

# CLI tools
brew "git"
brew "node"
brew "python"
brew "fzf"
brew "ripgrep"
brew "bat"
brew "eza"
brew "jq"
brew "gh"
brew "lazygit"
brew "starship"

# Casks (GUI apps)
cask "visual-studio-code"
cask "warp"
cask "raycast"
cask "docker"
cask "font-jetbrains-mono-nerd-font"
```

```bash
# Salvar configuração atual
brew bundle dump --file=~/Brewfile

# Restaurar em nova máquina
brew bundle install --file=~/Brewfile
```

---

## 8. Ferramentas de Produtividade

### Launcher: Raycast vs Alfred

| Aspecto | Raycast | Alfred |
|---------|---------|--------|
| **Preço** | Gratuito (Pro $8/mês) | Gratuito (Powerpack £34) |
| **Interface** | Moderna, polida | Clássica, funcional |
| **Extensões** | Store integrada, fácil | Workflows, mais técnico |
| **IA** | Integrada (Pro) | Plugin separado |
| **Clipboard** | Incluído grátis | Requer Powerpack |
| **Window Management** | Incluído grátis | Não nativo |
| **Velocidade** | Rápido | Mais rápido |
| **Curva de aprendizado** | Baixa | Média |

#### Instalação
```bash
# Raycast (recomendado para iniciantes)
brew install --cask raycast

# Alfred
brew install --cask alfred
```

### Extensões Raycast Essenciais

| Extensão | Função |
|----------|--------|
| GitHub | Gerenciar repos, PRs, issues |
| Linear | Gerenciar tarefas |
| Notion | Buscar e criar páginas |
| 1Password | Acessar senhas |
| Slack | Verificar mensagens |
| Jira | Gerenciar tickets |
| Zoom | Entrar em reuniões |
| Spotify | Controlar música |
| VS Code Projects | Abrir projetos |
| Tailwind CSS | Documentação rápida |

### Outras Ferramentas de Produtividade

| Ferramenta | Função | Instalação |
|------------|--------|------------|
| **Rectangle** | Gerenciamento de janelas (gratuito) | `brew install --cask rectangle` |
| **Maccy** | Histórico de clipboard (gratuito) | `brew install --cask maccy` |
| **Amphetamine** | Impedir suspensão | Mac App Store |
| **Obsidian** | Notas em Markdown | `brew install --cask obsidian` |
| **Notion** | Workspace colaborativo | `brew install --cask notion` |
| **Bitwarden** | Gerenciador de senhas | `brew install --cask bitwarden` |
| **Syncthing** | Sincronização de arquivos | `brew install syncthing` |
| **AppCleaner** | Desinstalar apps completamente | `brew install --cask appcleaner` |

---

## 9. Script de Instalação Automatizada

```bash
#!/bin/bash
# setup-dev-station.sh
# Configuração completa de estação de desenvolvimento

set -e

echo "🚀 Iniciando configuração da estação de desenvolvimento..."

# 1. Instalar Homebrew (se não existir)
if ! command -v brew &> /dev/null; then
    echo "📦 Instalando Homebrew..."
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    eval "$(/opt/homebrew/bin/brew shellenv)"
fi

# 2. Instalar ferramentas CLI essenciais
echo "🔧 Instalando ferramentas CLI..."
brew install git node python rust go
brew install wget curl jq fzf ripgrep bat eza tree htop
brew install gh lazygit starship

# 3. Instalar Oh-My-Zsh
if [ ! -d "$HOME/.oh-my-zsh" ]; then
    echo "🐚 Instalando Oh-My-Zsh..."
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended
fi

# 4. Instalar plugins Zsh
echo "🔌 Instalando plugins Zsh..."
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions 2>/dev/null || true
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting 2>/dev/null || true

# 5. Instalar aplicativos GUI
echo "🖥️ Instalando aplicativos..."
brew install --cask visual-studio-code
brew install --cask warp
brew install --cask raycast
brew install --cask docker
brew install --cask rectangle
brew install --cask obsidian

# 6. Instalar fontes
echo "🔤 Instalando fontes..."
brew tap homebrew/cask-fonts
brew install --cask font-jetbrains-mono-nerd-font
brew install --cask font-fira-code-nerd-font

# 7. Instalar extensões VS Code
echo "📝 Instalando extensões VS Code..."
code --install-extension anthropic.claude-code
code --install-extension esbenp.prettier-vscode
code --install-extension dbaeumer.vscode-eslint
code --install-extension eamodio.gitlens
code --install-extension PKief.material-icon-theme
code --install-extension usernamehw.errorlens
code --install-extension ritwickdey.LiveServer
code --install-extension formulahendry.auto-rename-tag
code --install-extension streetsidesoftware.code-spell-checker
code --install-extension christian-kohler.path-intellisense

# 8. Configurar Starship
echo "⭐ Configurando Starship..."
mkdir -p ~/.config
cat > ~/.config/starship.toml << 'EOF'
add_newline = true
command_timeout = 10000

[character]
success_symbol = "[❯](bold green)"
error_symbol = "[❯](bold red)"

[directory]
truncation_length = 3

[git_branch]
symbol = " "

[nodejs]
format = "via [ $version](bold green) "

[python]
format = 'via [🐍 $version]($style) '
EOF

# 9. Configurar .zshrc
echo "⚙️ Configurando .zshrc..."
cat >> ~/.zshrc << 'EOF'

# Plugins
plugins=(git zsh-autosuggestions zsh-syntax-highlighting docker)

# Starship
eval "$(starship init zsh)"

# Aliases úteis
alias ll="eza -la"
alias cat="bat"
alias grep="rg"
alias tree="eza --tree"
alias gs="git status"
alias gc="git commit"
alias gp="git push"
alias gl="git log --oneline -10"
EOF

echo "✅ Configuração concluída!"
echo "🔄 Reinicie o terminal para aplicar as mudanças."
echo "📚 Leia o guia completo para configurações avançadas."
```

### Execução
```bash
chmod +x setup-dev-station.sh
./setup-dev-station.sh
```

---

## 10. Configurações Recomendadas

### VS Code settings.json
```json
{
  // Editor
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
  "editor.inlineSuggest.enabled": true,
  
  // Terminal
  "terminal.integrated.fontFamily": "'JetBrainsMono Nerd Font'",
  "terminal.integrated.fontSize": 13,
  
  // Files
  "files.autoSave": "onFocusChange",
  "files.trimTrailingWhitespace": true,
  "files.insertFinalNewline": true,
  
  // Git
  "git.autofetch": true,
  "git.confirmSync": false,
  
  // Prettier
  "prettier.singleQuote": true,
  "prettier.trailingComma": "es5",
  
  // ESLint
  "eslint.validate": ["javascript", "typescript", "javascriptreact", "typescriptreact"],
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  },
  
  // GitLens
  "gitlens.hovers.currentLine.over": "line",
  
  // Error Lens
  "errorLens.enabledDiagnosticLevels": ["error", "warning"],
  
  // Workbench
  "workbench.iconTheme": "material-icon-theme",
  "workbench.colorTheme": "Default Dark Modern",
  "workbench.startupEditor": "none"
}
```

### Git Config Global
```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"
git config --global init.defaultBranch main
git config --global pull.rebase true
git config --global core.editor "code --wait"
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.lg "log --oneline --graph --all"
```

### Aliases de Terminal Úteis (~/.zshrc)
```bash
# Navegação
alias ..="cd .."
alias ...="cd ../.."
alias ~="cd ~"

# Listagem moderna (eza)
alias ls="eza"
alias ll="eza -la --icons"
alias lt="eza --tree --level=2 --icons"

# Ferramentas modernas
alias cat="bat"
alias grep="rg"
alias find="fd"
alias du="dust"
alias df="duf"
alias top="htop"

# Git
alias gs="git status"
alias ga="git add"
alias gc="git commit"
alias gp="git push"
alias gpl="git pull"
alias gl="git log --oneline -15"
alias gd="git diff"
alias gco="git checkout"
alias gb="git branch"
alias lg="lazygit"

# Docker
alias dc="docker compose"
alias dps="docker ps"
alias di="docker images"

# VS Code
alias c="code ."
alias cr="code -r ."

# Claude Code
alias cc="claude"
```

---

## Recursos e Links

### Documentação Oficial
- [Claude Code Docs](https://code.claude.com/docs/en/vs-code)
- [VS Code Documentation](https://code.visualstudio.com/docs)
- [Starship Configuration](https://starship.rs/config/)
- [Oh-My-Zsh Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki)
- [Homebrew Documentation](https://docs.brew.sh/)

### Repositórios Úteis
- [awesome-claude-code](https://github.com/jmanhype/awesome-claude-code)
- [awesome-mcp-servers](https://github.com/modelcontextprotocol/servers)
- [Nerd Fonts](https://github.com/ryanoasis/nerd-fonts)

### Comunidades
- [Claude Code Discord](https://discord.gg/anthropic)
- [VS Code GitHub Discussions](https://github.com/microsoft/vscode/discussions)

---

**Última atualização:** Janeiro 2026  
**Autor:** Compilado por Claude para Igor Morais Vasconcelos

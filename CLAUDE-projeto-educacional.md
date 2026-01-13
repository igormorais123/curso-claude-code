# Claude Code Master - Guia de Desenvolvimento

## Visão Geral do Projeto

**Nome:** Claude Code Master — Do Zero ao Agente Especialista
**Tipo:** Aplicativo HTML educacional autocontido (single-file)
**Público-alvo:** Usuário iniciante absoluto (zero programação) no Windows 11
**Idioma:** Português Brasil exclusivo
**Plano assumido:** Claude Max (Opus 4.5)

### Objetivo
Ensinar usuários sem conhecimento técnico a usar o Claude Code para três casos de uso:
1. **Trilha Jurídica:** Petições, análise de processos, jurisprudência
2. **Trilha Manutenção PC:** Diagnóstico, limpeza, otimização, automação
3. **Trilha Entrevistas:** Agentes para pesquisa qualitativa

---

## Estrutura do Projeto

```
claude-code-master/
├── CLAUDE.md           ← Este arquivo (instruções para desenvolvimento)
├── index.html          ← Aplicativo principal (HTML/CSS/JS autocontido)
└── assets/             ← Futuro: screenshots, GIFs (opcional)
```

### Arquitetura do App

O app é um **único arquivo HTML** que contém:
- CSS inline (variáveis, temas, componentes)
- JavaScript inline (estado, navegação, persistência)
- Conteúdo dos módulos como strings no objeto `MODULES`

**Por quê single-file?**
- Usuário iniciante pode abrir direto no navegador
- Funciona offline
- Fácil de compartilhar e hospedar

---

## Estado Atual do Desenvolvimento

### ✅ Implementado

| Componente | Descrição |
|------------|-----------|
| Layout responsivo | Grid com sidebar + main, colapsa em mobile |
| Sistema de temas | Light/dark com CSS variables, persiste em localStorage |
| Navegação | Menu lateral com seções por trilha |
| Progresso | Checkboxes persistentes, barra de progresso global |
| Blocos de código | Syntax highlight básico, botão copiar com feedback |
| Cards expansíveis | Steps com checkbox, priority badge, conteúdo colapsável |
| Checkpoints | Boxes de verificação (sucesso/erro) |
| Glossário visual | Cards com termo, definição, analogia |
| Seletor de trilhas | Cards clicáveis para cada caso de uso |

### ✅ Módulos Completos

| ID | Nome | Conteúdo |
|----|------|----------|
| m0 | O Que É Isso Tudo? | Conceito, glossário, casos de uso, planos, trilhas |
| m1 | Preparando o Windows | Verificar versão, PowerShell, winget |
| m2 | Instalação | VS Code, Claude Code (nativo), extensão |

### 🔄 Módulos Pendentes (Placeholder)

| ID | Nome | Prioridade |
|----|------|------------|
| m3 | Primeira Sessão | 🔴 Alta |
| m4 | Custos e Modelos | 🔴 Alta |
| j1 | Estrutura de Pastas Jurídicas | 🔴 Alta |
| j2 | Memória e Comandos | 🔴 Alta |
| j3 | MCPs Jurídicos | 🟠 Média |
| j4 | Skills e Subagentes | 🟠 Média |
| j5 | Documentos Grandes | 🟠 Média |
| j6 | Exportar para Word | 🟠 Média |
| p1 | Ambiente PC | 🟡 Baixa |
| p2 | Agente Diagnóstico | 🟡 Baixa |
| p3 | Scripts Úteis | 🟡 Baixa |
| e1 | Conceitos Entrevista | 🟡 Baixa |
| e2 | Roteiros e Personas | 🟡 Baixa |
| t1 | Revisão com Codex | 🟢 Opcional |
| t2 | Emergência (Troubleshooting) | 🟠 Média |

---

## Convenções de Código

### CSS

```css
/* Usar CSS variables para tudo */
--bg-primary, --text-primary, --accent-primary, etc.

/* Nomenclatura de classes */
.componente { }
.componente-elemento { }
.componente.modificador { }

/* Prioridades têm cores específicas */
--priority-required: vermelho
--priority-highly: laranja  
--priority-recommended: amarelo
--priority-optional: verde
--priority-tip: azul

/* Trilhas têm cores específicas */
--track-juridico: roxo (#7C3AED)
--track-pc: ciano (#0891B2)
--track-entrevista: rosa (#DB2777)
```

### JavaScript

```javascript
// Estado global
let state = {
    currentModule: 'm0',
    theme: 'light',
    progress: {},        // { 'm0-1': true, 'm0-2': false, ... }
    completedModules: [] // ['m0', 'm1', ...]
};

// Funções principais
loadState()      // Carrega do localStorage
saveState()      // Salva no localStorage
loadModule(id)   // Carrega conteúdo do módulo
toggleStep(id)   // Marca/desmarca checkbox
copyCode(btn, code) // Copia código para clipboard
toggleCard(header)  // Expande/colapsa card
toggleTheme()    // Alterna light/dark
updateProgress() // Atualiza barra e nav
```

### HTML dos Módulos

Cada módulo é uma string no objeto `MODULES`. Estrutura padrão:

```html
<!-- Breadcrumb -->
<nav class="breadcrumb">
    <a class="breadcrumb-link" onclick="loadModule('m0')">Início</a>
    <span>›</span>
    <span class="breadcrumb-current">Nome do Módulo</span>
</nav>

<!-- Header -->
<div class="module-header">
    <span class="module-number">Módulo X</span>
    <h1 class="module-title">Título do Módulo</h1>
    <p class="module-description">Descrição breve.</p>
    <div class="module-meta">
        <div class="meta-item">⏱️ X minutos</div>
        <div class="meta-item">⭐ Dificuldade</div>
    </div>
</div>

<!-- Steps -->
<div class="step-card expanded">
    <div class="step-card-header" onclick="toggleCard(this)">
        <div class="step-checkbox" data-step="mX-1" onclick="event.stopPropagation(); toggleStep('mX-1')">
            <svg>...</svg>
        </div>
        <div class="step-info">
            <div class="step-header-row">
                <span class="step-number">Passo 1</span>
                <span class="priority-badge required">Obrigatório</span>
            </div>
            <h3 class="step-title">Título do Passo</h3>
            <p class="step-summary">Resumo do que será feito</p>
        </div>
        <div class="step-toggle">
            <svg>...</svg>
        </div>
    </div>
    <div class="step-card-body">
        <div class="step-content">
            <!-- Conteúdo aqui -->
        </div>
    </div>
</div>

<!-- Navigation -->
<div class="nav-buttons">
    <a class="nav-btn prev" onclick="loadModule('anterior')">← Anterior</a>
    <a class="nav-btn next" onclick="loadModule('proximo')">Próximo →</a>
</div>
```

---

## Componentes Reutilizáveis

### Bloco de Código

```html
<div class="code-block">
    <div class="code-header">
        <span class="code-lang">PowerShell</span>
        <button class="code-copy" onclick="copyCode(this, 'COMANDO_AQUI')">
            <svg>...</svg>
            Copiar
        </button>
    </div>
    <div class="code-content">
        <pre><code>COMANDO_AQUI</code></pre>
    </div>
</div>
```

### Caixa de Dica

```html
<div class="tip-box tip">  <!-- tip | warning | success | error -->
    <span class="tip-icon">💡</span>
    <div class="tip-content">
        <div class="tip-title">Título da Dica</div>
        <p>Conteúdo da dica.</p>
    </div>
</div>
```

### Checkpoint

```html
<div class="checkpoint">
    <div class="checkpoint-header">
        <span class="checkpoint-icon">🔍</span>
        <span class="checkpoint-title">Checkpoint: Nome</span>
    </div>
    <p>Instrução de verificação.</p>
    <div class="code-block">...</div>
    <div class="checkpoint-result">
        <div class="checkpoint-result-box success">
            <strong>✅ FUNCIONOU</strong>
            <p>O que aparece se deu certo</p>
        </div>
        <div class="checkpoint-result-box error">
            <strong>❌ DEU ERRO</strong>
            <p>O que fazer se deu errado</p>
        </div>
    </div>
</div>
```

### Glossário

```html
<div class="glossary-card">
    <div class="glossary-term">
        <span class="glossary-icon">📟</span>
        Nome do Termo
    </div>
    <p class="glossary-definition">Definição técnica simples.</p>
    <p class="glossary-analogy">Analogia do dia a dia para facilitar.</p>
</div>
```

### Priority Badges

```html
<span class="priority-badge required">Obrigatório</span>
<span class="priority-badge highly">Altamente Recomendado</span>
<span class="priority-badge recommended">Recomendado</span>
<span class="priority-badge optional">Opcional</span>
```

---

## Conteúdo dos Módulos Pendentes

### M3: Primeira Sessão

**Passos a incluir:**
1. Autenticar conta Anthropic (`claude login`)
2. Entender a interface do Claude Code
3. Modos de operação: Edit, Auto, Plan
4. Primeiro `/init` em uma pasta
5. Comandos essenciais: `/clear`, `/cost`, `/model`, `/help`
6. Primeira conversa real

**Checkpoint:** Claude responde corretamente a uma pergunta simples.

### M4: Custos e Modelos

**Passos a incluir:**
1. Diferença entre Opus, Sonnet, Haiku (tabela comparativa)
2. Quando usar cada modelo (casos de uso)
3. Comando `/cost` para monitorar
4. Comando `/model` para trocar
5. Dicas para economizar tokens
6. Configurar modelo padrão no settings.json

**Checkpoint:** Usuário consegue trocar de modelo e verificar custo.

### J1: Estrutura de Pastas Jurídicas

**Passos a incluir:**
1. Criar estrutura de diretórios
   ```
   C:/Juridico/
   ├── .claude/
   │   ├── CLAUDE.md
   │   ├── settings.json
   │   ├── commands/
   │   └── agents/
   ├── base-jurisprudencia/
   ├── templates/
   ├── clientes/
   └── output/
   ```
2. Explicar propósito de cada pasta
3. Criar CLAUDE.md do projeto jurídico
4. Configurar settings.json com permissões

**Checkpoint:** Estrutura criada e `/init` executado com sucesso.

### J2: Memória e Comandos

**Passos a incluir:**
1. Criar CLAUDE.md especializado para advocacia
2. Criar comandos personalizados:
   - `/peticao` - Inicia nova petição
   - `/revisar` - Revisa documento
   - `/jurisprudencia` - Busca precedentes
   - `/formatar` - Formata para ABNT/tribunal
3. Testar cada comando

**Incluir templates completos dos comandos.**

### J3: MCPs Jurídicos

**MCPs a configurar:**
1. `filesystem` - Acesso a arquivos (obrigatório)
2. `context` - Busca semântica em documentos grandes
3. `memory` - Memória persistente entre sessões
4. `playwright` - Pesquisa em tribunais online
5. `sqlite` - Base de jurisprudência local
6. `gdrive` - Google Drive (opcional)

**Incluir comandos de instalação e verificação para cada um.**

### J4: Skills e Subagentes

**Skills a configurar:**
1. Explicar skills nativas (docx, xlsx, pdf)
2. Criar skill personalizada jurídica
3. Criar subagentes:
   - Agente Redator (escreve petições)
   - Agente Revisor (verifica gramática, coerência, citações)
   - Agente Pesquisador (busca jurisprudência)

**Incluir templates completos dos agentes.**

### J5: Documentos Grandes

**Passos a incluir:**
1. Capacidade do Opus (200K tokens ≈ 500 páginas)
2. Técnica de análise incremental
3. Uso do `/compact` para sessões longas
4. Referência com `@arquivo`
5. Estratégias para processos muito grandes

### J6: Exportar para Word

**Passos a incluir:**
1. Usar skill docx nativa
2. Comando para gerar petição em Word
3. Formatação ABNT
4. Adicionar cabeçalho, rodapé, numeração
5. Salvar em local específico

---

## Regras de Desenvolvimento

### Linguagem
- Português Brasil em todo conteúdo
- Tom informal mas profissional
- Explicar TUDO como se fosse para leigo absoluto
- Usar analogias do cotidiano
- Evitar jargão técnico; quando necessário, explicar imediatamente

### UX
- Primeiro card de cada módulo sempre começa expandido (`expanded`)
- Checkpoints SEMPRE após instalações ou configurações críticas
- Blocos de código SEMPRE têm botão copiar
- Nunca mais que 6 passos por módulo
- Incluir "O que esse comando faz?" em comandos complexos

### Testes
- Todos os comandos devem ser testados no Windows 11
- Verificar se copia funciona em todos os navegadores
- Testar tema claro E escuro
- Testar em mobile (responsividade)

### IDs de Steps
- Formato: `{moduleId}-{stepNumber}`
- Exemplo: `m0-1`, `m0-2`, `j1-1`, `j1-2`
- Manter sequência única por módulo

---

## Comandos Úteis para Desenvolvimento

```bash
# Abrir projeto no VS Code
code C:/caminho/para/claude-code-master

# Servir localmente (opcional, para teste)
npx serve .

# Verificar tamanho do arquivo
wc -l index.html

# Buscar por TODO no código
grep -n "TODO" index.html
```

---

## Próximas Tarefas (em ordem de prioridade)

1. [ ] Implementar M3: Primeira Sessão
2. [ ] Implementar M4: Custos e Modelos
3. [ ] Implementar J1: Estrutura de Pastas
4. [ ] Implementar J2: Memória e Comandos
5. [ ] Implementar T2: Emergência (troubleshooting rápido)
6. [ ] Implementar J3-J6 restantes
7. [ ] Implementar P1-P3 (Trilha PC)
8. [ ] Implementar E1-E2 (Trilha Entrevistas)
9. [ ] Implementar T1: Revisão com Codex
10. [ ] Adicionar screenshots/GIFs (opcional)
11. [ ] Adicionar busca no conteúdo
12. [ ] Adicionar sistema de conquistas/marcos

---

## Referências

- Guia Mestre do Ecossistema Claude: `/mnt/user-data/outputs/guia-mestre-ecossistema-claude.md`
- Documentação oficial Claude Code: https://docs.anthropic.com/en/docs/claude-code
- Documentação MCPs: https://modelcontextprotocol.io/

---

## Notas do Desenvolvedor

- O app foi projetado para funcionar 100% offline após o primeiro carregamento
- Todo estado é persistido em localStorage com a chave `claudeCodeMaster`
- O CSS usa variáveis para facilitar temas e customização
- A estrutura modular permite adicionar novos módulos facilmente
- Fonts são carregadas do Google Fonts (única dependência externa)

**Última atualização:** Janeiro 2026
**Versão:** 1.0.0

# PROMPT DE IMPLEMENTAÇÃO - Sistema MemOS (Memória com Ciclo de Sono)

## Como Usar Este Prompt

Copie o conteúdo abaixo da linha divisória e cole no Claude Code dentro da pasta do projeto onde deseja implementar o sistema de memória.

---

# IMPLEMENTAR SISTEMA MEMOS - Memória Biomimética com Ciclo de Sono

## Sua Tarefa

Crie um sistema completo de gestão de memória inspirado no ciclo de sono humano para este projeto. O sistema deve:

1. Registrar todas as interações automaticamente
2. Consolidar memórias importantes (como o sono REM)
3. Esquecer seletivamente informações irrelevantes
4. Permitir acesso multi-agente (Claude, ChatGPT, Codex)

## Estrutura de Pastas a Criar

```
.memoria/
├── INDEX.md                    # Índice navegável de todas as memórias
├── sessoes/                    # Memórias episódicas (curto prazo)
│   └── YYYY-MM-DD_HH-MM.md    # Uma sessão por arquivo
├── consolidado/                # Memórias semânticas (longo prazo)
│   ├── DECISOES.md            # Decisões arquiteturais importantes
│   ├── PADROES.md             # Padrões de código adotados
│   ├── PROBLEMAS_RESOLVIDOS.md # Soluções para problemas recorrentes
│   └── CONTEXTO_PROJETO.md    # Entendimento geral do projeto
├── ciclo/                      # Controle do ciclo de sono
│   ├── ESTADO.json            # Estado atual (vigília/sono/fase)
│   └── METRICAS.json          # Métricas de memória
└── PROTOCOLO.md               # Regras para acesso multi-agente
```

## Conteúdo de Cada Arquivo

### 1. INDEX.md

```markdown
# Índice de Memórias - [Nome do Projeto]

> Sistema MemOS v1.0 - Última atualização: [DATA]

## Status do Sistema
- **Estado atual:** Vigília
- **Sessões registradas:** 0
- **Memórias consolidadas:** 0
- **Última consolidação:** Nunca

## Navegação Rápida

### Sessões Recentes
*Nenhuma sessão registrada ainda*

### Conhecimento Consolidado
- [Decisões Arquiteturais](consolidado/DECISOES.md)
- [Padrões de Código](consolidado/PADROES.md)
- [Problemas Resolvidos](consolidado/PROBLEMAS_RESOLVIDOS.md)
- [Contexto do Projeto](consolidado/CONTEXTO_PROJETO.md)

## Comandos do Sistema

| Comando | Descrição |
|---------|-----------|
| `/memoria status` | Ver estado atual do sistema |
| `/memoria buscar [termo]` | Buscar nas memórias |
| `/memoria consolidar` | Iniciar ciclo de consolidação |
| `/memoria esquecer [id]` | Marcar memória para esquecimento |

## Estatísticas
- Memórias episódicas: 0
- Memórias semânticas: 0
- Taxa de consolidação: 0%
- Importância média: 0
```

### 2. PROTOCOLO.md

```markdown
# Protocolo de Acesso Multi-Agente

## Identificação de Agentes

Cada IA deve se identificar ao acessar este sistema:

| Agente | ID | Permissões |
|--------|-----|------------|
| Claude Code | `claude-code` | Leitura/Escrita/Consolidação |
| ChatGPT | `chatgpt` | Leitura/Escrita |
| GitHub Copilot | `copilot` | Leitura |
| Codex | `codex` | Leitura/Escrita |

## Regras de Escrita

1. **Nunca sobrescrever** - Sempre adicionar, nunca substituir
2. **Identificar fonte** - Toda entrada deve ter `[AGENTE:id]`
3. **Timestamp obrigatório** - Formato ISO 8601
4. **Validação cruzada** - Marcar informações não verificadas com `[?]`

## Formato de Entrada de Memória

```
---
timestamp: YYYY-MM-DDTHH:MM:SS
agente: [id-do-agente]
tipo: [episodica|semantica|reflexao]
importancia: [1-10]
tags: [lista, de, tags]
---

[Conteúdo da memória]
```

## Resolução de Conflitos

1. Memórias com maior `importancia` têm precedência
2. Em empate, a mais recente prevalece
3. Conflitos não resolvidos vão para `consolidado/CONFLITOS.md`

## Ciclo de Sono - Fases

### Fase 1: Hipnagogia (Transição)
- Indexar novas sessões
- Calcular importância inicial
- Duração: ~5% do ciclo

### Fase 2: Sono de Ondas Lentas (Consolidação)
- Mover memórias importantes para `consolidado/`
- Comprimir informações redundantes
- Duração: ~50% do ciclo

### Fase 3: REM (Validação)
- Verificar consistência entre memórias
- Simular cenários com conhecimento atual
- Gerar reflexões e insights
- Duração: ~30% do ciclo

### Fase 4: Despertar (Integração)
- Atualizar INDEX.md
- Limpar sessões antigas (>30 dias)
- Gerar relatório de consolidação
- Duração: ~15% do ciclo
```

### 3. ciclo/ESTADO.json

```json
{
  "versao": "1.0",
  "estado_atual": "vigilia",
  "ultima_mudanca": "TIMESTAMP",
  "ciclos_completos": 0,
  "proxima_consolidacao": null,
  "fase_atual": null,
  "progresso_fase": 0,
  "gatilhos": {
    "sessoes_para_consolidar": 5,
    "horas_desde_ultima": 24,
    "importancia_acumulada": 150
  }
}
```

### 4. ciclo/METRICAS.json

```json
{
  "total_sessoes": 0,
  "total_consolidadas": 0,
  "total_esquecidas": 0,
  "importancia_media": 0,
  "tags_frequentes": {},
  "agentes_ativos": [],
  "ultima_atualizacao": "TIMESTAMP"
}
```

### 5. consolidado/DECISOES.md

```markdown
# Decisões Arquiteturais

> Memórias consolidadas sobre decisões importantes do projeto

## Estrutura

Cada decisão segue o formato ADR (Architecture Decision Record):

---

### [ID] Título da Decisão

**Data:** YYYY-MM-DD
**Status:** [proposta|aceita|rejeitada|obsoleta]
**Importância:** X/10

**Contexto:**
[Por que essa decisão foi necessária]

**Decisão:**
[O que foi decidido]

**Consequências:**
[Impactos positivos e negativos]

**Fontes:**
- Sessão: [link para sessão original]
- Agente: [quem registrou]

---

*Nenhuma decisão registrada ainda*
```

### 6. consolidado/PADROES.md

```markdown
# Padrões de Código

> Convenções e padrões adotados neste projeto

## Nomenclatura
*A definir*

## Estrutura de Arquivos
*A definir*

## Estilo de Código
*A definir*

## Testes
*A definir*

## Documentação
*A definir*

---
*Última consolidação: Nunca*
```

### 7. consolidado/PROBLEMAS_RESOLVIDOS.md

```markdown
# Problemas Resolvidos

> Base de conhecimento de soluções para problemas encontrados

## Formato

### [ID] Título do Problema

**Sintomas:**
[Como o problema se manifestou]

**Causa Raiz:**
[O que causou o problema]

**Solução:**
[Como foi resolvido]

**Prevenção:**
[Como evitar no futuro]

**Tags:** [tag1, tag2]

---

*Nenhum problema registrado ainda*
```

### 8. consolidado/CONTEXTO_PROJETO.md

```markdown
# Contexto do Projeto

> Entendimento consolidado sobre o projeto

## Visão Geral
*A ser preenchido durante as sessões*

## Tecnologias
*A ser identificado*

## Arquitetura
*A ser mapeado*

## Stakeholders
*A ser identificado*

## Objetivos
*A ser definido*

## Restrições
*A ser identificado*

---
*Última atualização: [DATA]*
*Confiança: Baixa (poucas sessões)*
```

### 9. Template de Sessão (sessoes/YYYY-MM-DD_HH-MM.md)

```markdown
# Sessão [DATA] [HORA]

## Metadados
- **Agente:** [id]
- **Duração:** [tempo]
- **Importância calculada:** [1-10]
- **Tags automáticas:** [lista]

## Resumo Executivo
[3-5 linhas sobre o que foi feito]

## Interações Principais

### [HH:MM] Tópico 1
[Detalhes]

### [HH:MM] Tópico 2
[Detalhes]

## Decisões Tomadas
- [ ] Decisão 1 → Consolidar? [S/N]
- [ ] Decisão 2 → Consolidar? [S/N]

## Problemas Encontrados
- [ ] Problema 1 → Resolvido? [S/N]

## Próximos Passos
- [ ] Tarefa 1
- [ ] Tarefa 2

## Notas para Consolidação
[Informações importantes para lembrar]

---
*Gerado automaticamente pelo Sistema MemOS*
```

## Instruções para CLAUDE.md

Adicione esta seção ao CLAUDE.md do projeto:

```markdown
---

## Sistema de Memória (MemOS)

Este projeto usa o Sistema MemOS para gestão de memória com ciclo de sono.

### Comportamento Automático

1. **Início de Sessão**
   - Ler `.memoria/INDEX.md` para contexto
   - Verificar `.memoria/ciclo/ESTADO.json`
   - Criar arquivo de sessão em `.memoria/sessoes/`

2. **Durante a Sessão**
   - Registrar decisões importantes
   - Marcar problemas resolvidos
   - Atualizar contexto quando necessário

3. **Fim de Sessão**
   - Calcular importância da sessão
   - Atualizar métricas
   - Verificar gatilhos de consolidação

### Gatilhos de Consolidação

Iniciar ciclo de sono quando:
- Σ(importância das sessões não consolidadas) > 150
- 5+ sessões sem consolidação
- 24+ horas desde última consolidação
- Comando explícito `/memoria consolidar`

### Fórmula de Importância

```
importancia = α₁·recencia + α₂·relevancia + α₃·frequencia
onde:
  α₁ = 0.3 (peso recência)
  α₂ = 0.5 (peso relevância ao projeto)
  α₃ = 0.2 (peso frequência de acesso)
  recencia = 0.995^(horas_desde_criacao)
```

### Comandos Disponíveis

- `/memoria status` - Estado atual
- `/memoria buscar [termo]` - Buscar memórias
- `/memoria consolidar` - Forçar consolidação
- `/memoria reflexao` - Gerar reflexão sobre sessões recentes
```

## Execução

Após criar toda a estrutura:

1. Crie todos os diretórios e arquivos listados
2. Substitua `[DATA]`, `[TIMESTAMP]` pelos valores atuais
3. Substitua `[Nome do Projeto]` pelo nome real
4. Adicione a seção ao CLAUDE.md existente (ou crie um novo)
5. Confirme a criação listando a estrutura final

**IMPORTANTE:**
- Use a data/hora atual para todos os timestamps
- Mantenha a formatação Markdown correta
- Crie arquivos vazios se necessário para a estrutura

# PLANO MEMOS v2.0 - Sistema de Memória com Ciclo de Sono

> **Arquivo:** `PLANO-MEMOS-v2-FINAL.md`
> **Local:** `C:\Users\igorm\.claude\curso-claude-code\`
> **Data:** 2026-01-20
> **Status:** Versão Final Revisada

---

## 1. OBJETIVO

Sistema de gestão de memória para projetos que imita o ciclo sono/vigília humano:
- Registro automático de interações
- Consolidação de memórias importantes
- Esquecimento seletivo baseado em critérios
- Acesso multi-agente preparado

---

## 2. DECISÕES CONFIRMADAS

| Item | Decisão | Justificativa |
|------|---------|---------------|
| Pasta | `.memoria/` | Português, intuitivo |
| Gatilho sessões | **10 sessões** | Balanceado |
| Gatilho tempo | **24 horas** | Ciclo diário |
| Consolidador atual | Claude Code | Único ativo |
| Consolidador futuro | OpenCode | Em preparação |

---

## 3. ESTRUTURA DE PASTAS

```
.memoria/
├── INDEX.md                      # Portal principal
├── PROTOCOLO.md                  # Regras multi-agente
├── sessoes/                      # Memória EPISÓDICA
│   ├── 2026-01-20_14-30.md      # Sessão individual
│   └── ...
├── consolidado/                  # Memória SEMÂNTICA
│   ├── DECISOES.md              # ADRs
│   ├── PADROES.md               # Convenções
│   ├── PROBLEMAS.md             # Soluções
│   └── CONTEXTO.md              # Visão do projeto
├── ciclo/
│   ├── ESTADO.json              # Estado atual
│   ├── METRICAS.json            # Estatísticas
│   └── HISTORICO.json           # [NOVO] Log de consolidações
└── arquivo/                      # [NOVO] Backup
    └── consolidacoes/            # Snapshots anteriores
```

---

## 4. CICLO DE SONO (4 Fases)

```
┌─────────────────────────────────────────────────────────┐
│                    CICLO DE SONO                        │
├─────────┬───────────────────────────────────┬──────────┤
│  FASE   │           AÇÃO                    │  % TEMPO │
├─────────┼───────────────────────────────────┼──────────┤
│ 1. HIPO │ Indexar sessões, calcular scores  │    5%    │
│ 2. LENT │ Mover importantes → consolidado/  │   50%    │
│ 3. REM  │ Validar, conectar, refletir       │   30%    │
│ 4. DESP │ Limpar, atualizar INDEX, backup   │   15%    │
└─────────┴───────────────────────────────────┴──────────┘
```

### Gatilhos de Entrada em Sono

O sistema inicia consolidação quando **QUALQUER** condição for verdadeira:

1. `sessoes_nao_consolidadas >= 10`
2. `horas_desde_ultima_consolidacao >= 24`
3. Comando explícito no prompt: "consolidar memórias"

---

## 5. FÓRMULA DE IMPORTÂNCIA (Corrigida)

```
SCORE = (0.3 × Recência) + (0.5 × Relevância) + (0.2 × Frequência)

Onde:
├── Recência = 0.995^(horas_desde_criação)
│   └── Exemplo: 24h = 0.887, 48h = 0.786, 168h(1sem) = 0.431
│
├── Relevância = média dos fatores abaixo (0 a 1):
│   ├── Mencionou arquivos do projeto? (+0.3)
│   ├── Contém decisão arquitetural? (+0.4)
│   ├── Resolveu problema/bug? (+0.3)
│   └── Foi referenciado depois? (+bonus dinâmico)
│
└── Frequência = acessos_desta_memoria / total_acessos_todas_memorias
```

### Limiar de Consolidação
- **SCORE >= 0.6:** Consolidar obrigatoriamente
- **SCORE 0.4-0.6:** Revisar durante REM
- **SCORE < 0.4:** Candidato a esquecimento

---

## 6. CRITÉRIOS DE ESQUECIMENTO (NOVO)

Uma memória é esquecida quando **TODAS** as condições forem verdadeiras:

1. `score < 0.3` (baixa importância)
2. `idade > 30 dias` (antiga)
3. `acessos == 0` nos últimos 14 dias
4. `não_referenciada` por outras memórias

**Processo:**
1. Mover para `.memoria/arquivo/esquecidas/`
2. Manter por 60 dias (recuperável)
3. Após 60 dias: deletar permanentemente

---

## 7. ACESSO MULTI-AGENTE

### Tabela de Permissões

| Agente | ID | Ler | Escrever | Consolidar | Lock |
|--------|-----|-----|----------|------------|------|
| Claude Code | `claude-code` | Sim | Sim | Sim | Sim |
| OpenCode | `opencode` | Sim | Sim | Futuro | Não |
| ChatGPT | `chatgpt` | Sim | Sim | Não | Não |
| Copilot | `copilot` | Sim | Não | Não | Não |

### Sistema de Lock (NOVO)

Para evitar conflitos de escrita simultânea:

```json
// .memoria/ciclo/ESTADO.json
{
  "lock": {
    "ativo": false,
    "agente": null,
    "inicio": null,
    "timeout_minutos": 30
  }
}
```

**Regras:**
1. Antes de escrever: verificar `lock.ativo`
2. Se `ativo == true` e `agente != eu`: aguardar ou só ler
3. Se `timeout` expirou: assumir lock abandonado, liberar
4. Após escrita: liberar lock

---

## 8. FORMATO DE SESSÃO (Template Completo)

```markdown
# Sessão [DATA] [HORA]

## Metadados
- **ID:** [UUID ou YYYYMMDD_HHMM]
- **Agente:** [claude-code|opencode|chatgpt]
- **Início:** [ISO 8601]
- **Fim:** [ISO 8601]
- **Score Calculado:** [0.0-1.0]
- **Tags:** [lista, de, tags]
- **Consolidada:** [Não|Sim - data]

---

## Resumo
[2-3 frases sobre o que foi feito]

## Interações Principais

### [HH:MM] Tópico 1
[Detalhes da interação]

**Decisão?** [Sim/Não]
**Problema resolvido?** [Sim/Não]
**Arquivos alterados:** [lista]

---

## Para Consolidação

### Decisões Tomadas
- [ ] [Descrição] → Importância: [1-10]

### Problemas Resolvidos
- [ ] [Descrição] → Causa: [X] → Solução: [Y]

### Padrões Identificados
- [ ] [Descrição do padrão]

### Contexto Aprendido
- [ ] [Novo entendimento sobre o projeto]

---

## Notas
[Observações livres]

---
*Gerado por [AGENTE:id] via Sistema MemOS*
```

---

## 9. ARQUIVOS JSON (Corrigidos)

### ciclo/ESTADO.json

```json
{
  "versao": "2.0",
  "estado_atual": "vigilia",
  "ultima_mudanca": "2026-01-20T14:30:00Z",
  "ciclos_completos": 0,
  "em_consolidacao": false,
  "fase_atual": null,
  "progresso_fase": 0,
  "gatilhos": {
    "sessoes_para_consolidar": 10,
    "horas_desde_ultima": 24
  },
  "lock": {
    "ativo": false,
    "agente": null,
    "inicio": null,
    "timeout_minutos": 30
  },
  "proxima_verificacao": "2026-01-21T14:30:00Z"
}
```

### ciclo/METRICAS.json

```json
{
  "versao": "2.0",
  "ultima_atualizacao": "2026-01-20T14:30:00Z",
  "sessoes": {
    "total": 0,
    "consolidadas": 0,
    "esquecidas": 0,
    "pendentes": 0
  },
  "memorias": {
    "episodicas": 0,
    "semanticas": 0,
    "arquivadas": 0
  },
  "scores": {
    "media": 0,
    "maximo": 0,
    "minimo": 0
  },
  "agentes": {
    "claude-code": { "sessoes": 0, "ultima": null },
    "opencode": { "sessoes": 0, "ultima": null },
    "chatgpt": { "sessoes": 0, "ultima": null }
  },
  "tags_frequentes": {}
}
```

### ciclo/HISTORICO.json (NOVO)

```json
{
  "versao": "1.0",
  "consolidacoes": [
    {
      "id": 1,
      "data": "2026-01-20T14:30:00Z",
      "agente": "claude-code",
      "sessoes_processadas": 10,
      "memorias_consolidadas": 5,
      "memorias_esquecidas": 2,
      "duracao_segundos": 120,
      "backup": "arquivo/consolidacoes/2026-01-20_1430.zip"
    }
  ]
}
```

---

## 10. INTEGRAÇÃO OPENCODE (Preparação)

### Arquivo AGENTS.md

Adicionar ao AGENTS.md do projeto:

```markdown
## Agente: MemOS-Guardian

**Persona:** Guardião da memória do projeto.

**Instruções:**
1. Ao iniciar: ler `.memoria/INDEX.md`
2. Verificar `.memoria/ciclo/ESTADO.json` - lock ativo?
3. Criar sessão em `.memoria/sessoes/`
4. Marcar TODAS entradas com `[AGENTE:opencode]`
5. Ao finalizar: atualizar métricas

**Permissões:**
- Ler: Sim
- Escrever sessões: Sim
- Consolidar: NÃO (reservado para Claude Code)

**Formato de entrada:**
```
[AGENTE:opencode] [2026-01-20T14:30:00Z]
Conteúdo da memória aqui
```
```

### Arquivo opencode.json

```json
{
  "providers": {
    "anthropic": { "enabled": true }
  },
  "mcp": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", ".memoria"]
    }
  },
  "defaults": {
    "agent": "MemOS-Guardian"
  }
}
```

---

## 11. COMPORTAMENTO ESPERADO (para CLAUDE.md)

### Início de Sessão
```
1. Verificar se .memoria/ existe
2. Ler INDEX.md para contexto
3. Verificar ESTADO.json:
   - lock ativo? → apenas ler
   - gatilho atingido? → sugerir consolidação
4. Criar novo arquivo de sessão
5. Informar: "Sessão iniciada. [X] memórias disponíveis."
```

### Durante a Sessão
```
1. Registrar interações relevantes
2. Marcar decisões importantes
3. Anotar problemas resolvidos
4. Identificar padrões
```

### Fim de Sessão
```
1. Calcular score da sessão
2. Atualizar métricas
3. Verificar gatilhos
4. Se gatilho atingido: perguntar "Consolidar agora?"
```

### Consolidação (quando solicitada)
```
1. Adquirir lock
2. Fase 1 - Hipnagogia (5%):
   - Listar todas sessões não consolidadas
   - Calcular scores
3. Fase 2 - Ondas Lentas (50%):
   - Score >= 0.6: mover para consolidado/
   - Atualizar arquivos semânticos
4. Fase 3 - REM (30%):
   - Revisar conexões entre memórias
   - Gerar reflexões
   - Validar consistência
5. Fase 4 - Despertar (15%):
   - Aplicar esquecimento (score < 0.3)
   - Criar backup
   - Atualizar INDEX.md
   - Liberar lock
6. Reportar resultado
```

---

## 12. CHECKLIST DE IMPLEMENTAÇÃO

- [ ] Criar pasta `.memoria/`
- [ ] Criar `INDEX.md`
- [ ] Criar `PROTOCOLO.md`
- [ ] Criar `sessoes/` (vazia)
- [ ] Criar `consolidado/DECISOES.md`
- [ ] Criar `consolidado/PADROES.md`
- [ ] Criar `consolidado/PROBLEMAS.md`
- [ ] Criar `consolidado/CONTEXTO.md`
- [ ] Criar `ciclo/ESTADO.json`
- [ ] Criar `ciclo/METRICAS.json`
- [ ] Criar `ciclo/HISTORICO.json`
- [ ] Criar `arquivo/` (vazia)
- [ ] Atualizar CLAUDE.md com instruções
- [ ] Criar AGENTS.md para OpenCode
- [ ] Testar ciclo completo

---

## 13. VERIFICAÇÃO PÓS-IMPLEMENTAÇÃO

1. Criar estrutura em projeto teste
2. Simular 3 sessões com Claude Code
3. Verificar se sessões foram salvas corretamente
4. Simular 10 sessões (ou aguardar 24h)
5. Executar consolidação manual
6. Verificar se memórias foram consolidadas
7. Verificar se métricas foram atualizadas
8. Testar com OpenCode (apenas leitura/escrita)
9. Verificar se lock funciona

---

## 14. DIFERENÇAS DA v1 PARA v2

| Aspecto | v1 | v2 |
|---------|----|----|
| Gatilho sessões | 5 (inconsistente) | 10 (corrigido) |
| Esquecimento | Não definido | Critérios claros |
| Lock | Ausente | Implementado |
| Backup | Ausente | Pasta arquivo/ |
| Histórico | Ausente | HISTORICO.json |
| Score threshold | Não definido | 0.6/0.4/0.3 |
| Template sessão | Parcial | Completo |
| Relevância | Subjetivo | Fórmula clara |

---

## 15. ARQUIVOS RELACIONADOS

| Arquivo | Local | Descrição |
|---------|-------|-----------|
| Plano v1 (original) | `.claude/plans/radiant-sauteeing-pnueli.md` | Versão inicial |
| Plano v2 (este) | `curso-claude-code/PLANO-MEMOS-v2-FINAL.md` | Versão revisada |
| Prompt implementação | `curso-claude-code/PROMPT-MEMOS-IMPLEMENTACAO.md` | Prompt para criar |
| Ref. OpenCode | `Downloads/Guia Prático do OpenCode...md` | Documentação |

---

**FIM DO PLANO v2.0**

*Revisado com análise crítica em 2026-01-20*

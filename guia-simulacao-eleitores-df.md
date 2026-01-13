# Sistema de Simulação de Eleitores do Distrito Federal
## Guia Completo: Do Conceito à Implementação com Claude Code

---

## Índice

1. [Visão Geral do Projeto](#1-visão-geral-do-projeto)
2. [Fundamentos Teóricos](#2-fundamentos-teóricos)
3. [Análise dos Repositórios Stanford](#3-análise-dos-repositórios-stanford)
4. [Arquitetura do Sistema Proposto](#4-arquitetura-do-sistema-proposto)
5. [Dados Demográficos do Eleitorado do DF](#5-dados-demográficos-do-eleitorado-do-df)
6. [Criando a Amostra de 400 Eleitores](#6-criando-a-amostra-de-400-eleitores)
7. [Implementação Passo a Passo](#7-implementação-passo-a-passo)
8. [Sistema de Entrevistas](#8-sistema-de-entrevistas)
9. [Análise de Impacto de Notícias](#9-análise-de-impacto-de-notícias)
10. [Validação Estatística](#10-validação-estatística)
11. [Código Prático](#11-código-prático)
12. [Custos e Otimização](#12-custos-e-otimização)
13. [Considerações Éticas](#13-considerações-éticas)
14. [Próximos Passos](#14-próximos-passos)

---

## 1. Visão Geral do Projeto

### O Que Você Vai Construir

Um sistema de **Agentes Generativos** que simula 400 eleitores do Distrito Federal, permitindo:

```
┌─────────────────────────────────────────────────────────────────┐
│                    SISTEMA DE SIMULAÇÃO ELEITORAL               │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐         │
│  │   BANCO DE  │    │  MOTOR DE   │    │  PAINEL DE  │         │
│  │   AGENTES   │───▶│  SIMULAÇÃO  │───▶│   ANÁLISE   │         │
│  │  (400 DF)   │    │             │    │             │         │
│  └─────────────┘    └─────────────┘    └─────────────┘         │
│        │                  │                  │                  │
│        │                  │                  │                  │
│        ▼                  ▼                  ▼                  │
│  • Perfis demográficos   • Entrevistas     • Intenção de voto  │
│  • Histórias pessoais    • Reações         • Impacto de temas  │
│  • Memórias              • Debates         • Segmentação       │
│  • Valores/crenças       • Notícias        • Tendências        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Casos de Uso Principais

| Caso de Uso | Descrição | Exemplo Prático |
|-------------|-----------|-----------------|
| **Pré-teste de Mensagens** | Testar como diferentes grupos reagem a mensagens de campanha | "Como eleitores de 25-34 anos de Ceilândia reagem a propostas sobre transporte público?" |
| **Análise de Impacto** | Medir efeito de notícias/escândalos na intenção de voto | "Qual o impacto de uma denúncia de corrupção entre eleitores indecisos?" |
| **Identificação de Temas** | Descobrir quais pautas mobilizam cada segmento | "Quais são as 3 prioridades dos eleitores do Plano Piloto vs Estrutural?" |
| **Simulação de Debates** | Prever reações a posicionamentos em debates | "Como eleitores evangélicos reagem à posição X sobre aborto?" |
| **Teste A/B de Propostas** | Comparar aceitação de diferentes versões de uma proposta | "Proposta A (foco em emprego) vs Proposta B (foco em segurança)" |

### Por Que 400 Agentes?

A escolha de 400 agentes não é arbitrária:

```
CÁLCULO DA AMOSTRA REPRESENTATIVA:
─────────────────────────────────

População do DF: ~2.1 milhões de eleitores
Nível de confiança: 95%
Margem de erro: 5%

Fórmula: n = (Z² × p × q) / E²
Onde:
  Z = 1.96 (95% confiança)
  p = 0.5 (proporção esperada)
  q = 0.5 (1 - p)
  E = 0.05 (margem de erro)

n = (1.96² × 0.5 × 0.5) / 0.05²
n = (3.8416 × 0.25) / 0.0025
n = 0.9604 / 0.0025
n = 384.16 ≈ 385

Arredondando para 400 para facilitar estratificação.
```

**Com 400 agentes bem estratificados**, você obtém resultados estatisticamente válidos comparáveis a pesquisas eleitorais reais.

---

## 2. Fundamentos Teóricos

### 2.1 O Que São Agentes Generativos?

**Agentes Generativos** são programas de computador que usam Modelos de Linguagem (como Claude ou GPT) para simular comportamentos humanos de forma realista.

```
┌─────────────────────────────────────────────────────────────────┐
│              ANATOMIA DE UM AGENTE GENERATIVO                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌───────────────────────────────────────────────────────────┐ │
│  │                     IDENTIDADE (Scratchpad)                │ │
│  │  • Nome, idade, gênero, profissão                         │ │
│  │  • Região administrativa onde mora                         │ │
│  │  • Renda, escolaridade, religião                          │ │
│  │  • Valores, crenças, opiniões políticas                   │ │
│  └───────────────────────────────────────────────────────────┘ │
│                            │                                    │
│                            ▼                                    │
│  ┌───────────────────────────────────────────────────────────┐ │
│  │                    MEMÓRIA (Memory Stream)                 │ │
│  │  • Experiências passadas relevantes                       │ │
│  │  • Interações anteriores                                  │ │
│  │  • Notícias que consumiu                                  │ │
│  │  • Reflexões sobre eventos                                │ │
│  └───────────────────────────────────────────────────────────┘ │
│                            │                                    │
│                            ▼                                    │
│  ┌───────────────────────────────────────────────────────────┐ │
│  │                    COMPORTAMENTO                           │ │
│  │  • Responde a perguntas consistentemente                  │ │
│  │  • Forma opiniões baseadas em identidade + memória        │ │
│  │  • Evolui com novas informações                           │ │
│  └───────────────────────────────────────────────────────────┘ │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 2.2 Arquitetura de Stanford (Generative Agents)

O paper original de Stanford (2023) introduziu três componentes essenciais:

#### Componente 1: Observação (Observation)
```
O agente "observa" o ambiente e registra eventos.

EXEMPLO:
  Agente recebe notícia: "Governador anuncia aumento do passe estudantil"
  Observação registrada: "Vi notícia sobre aumento do passe estudantil 
                          em 12/01/2026 às 14:30"
```

#### Componente 2: Reflexão (Reflection)
```
O agente sintetiza memórias em conclusões de alto nível.

EXEMPLO:
  Memórias:
    - "Pago R$50/mês de transporte para ir ao trabalho"
    - "Meu salário não aumentou nos últimos 2 anos"
    - "Vi notícia sobre aumento do passe estudantil"
  
  Reflexão gerada: "O custo de transporte está pesando cada vez mais 
                    no meu orçamento. Políticas de transporte público 
                    afetam diretamente minha qualidade de vida."
```

#### Componente 3: Planejamento (Planning)
```
O agente planeja ações futuras com base em identidade + memória.

EXEMPLO:
  Dado estímulo: "Você vai votar em qual candidato?"
  
  Processo interno:
    1. Recupera memórias relevantes sobre candidatos
    2. Considera valores pessoais (identidade)
    3. Reflete sobre experiências recentes
    4. Formula resposta coerente
```

### 2.3 Arquitetura de Stanford (GenAgents - 1000 People)

O paper mais recente (2024) trouxe inovações importantes:

```
┌─────────────────────────────────────────────────────────────────┐
│           DIFERENÇAS ENTRE OS DOIS PROJETOS STANFORD            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  GENERATIVE AGENTS (2023)         │  GENAGENTS 1000 (2024)      │
│  ─────────────────────────────────│──────────────────────────── │
│  • Agentes fictícios              │  • Agentes baseados em      │
│  • Baseados em biografias curtas  │    pessoas REAIS            │
│  • Ambiente visual (Smallville)   │  • Baseados em entrevistas  │
│  • Foco em interação entre        │    de 2 horas cada          │
│    agentes                        │  • Foco em replicar         │
│  • Emergência de comportamentos   │    respostas individuais    │
│                                   │  • 85% de precisão vs       │
│                                   │    respostas reais          │
│                                                                 │
│  USAR PARA:                       │  USAR PARA:                 │
│  • Simulações de comunidades      │  • Pesquisas e surveys      │
│  • Jogos e ambientes virtuais     │  • Testes de políticas      │
│  • Estudos de dinâmica social     │  • Simulação de eleitorado  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

**Para seu projeto de eleitores do DF, vamos combinar elementos de ambos:**
- Estrutura de identidade + memória do GenAgents
- Sistema de respostas categóricas e numéricas do GenAgents
- Simplicidade de implementação (sem ambiente visual)

---

## 3. Análise dos Repositórios Stanford

### 3.1 Repositório: generative_agents

**URL:** https://github.com/joonspk-research/generative_agents

#### Estrutura de Arquivos
```
generative_agents/
├── environment/
│   └── frontend_server/          # Interface visual (Django)
│       ├── manage.py
│       ├── static_dirs/assets/   # Mapa, sprites
│       └── storage/              # Simulações salvas
│
├── reverie/
│   └── backend_server/
│       ├── reverie.py            # Motor principal
│       ├── persona/              # Definição de agentes
│       │   ├── persona.py        # Classe Persona
│       │   ├── memory_structures/
│       │   │   ├── associative_memory.py
│       │   │   └── scratch.py    # Identidade do agente
│       │   └── cognitive_modules/
│       │       ├── perceive.py   # Observação
│       │       ├── retrieve.py   # Recuperação de memória
│       │       ├── plan.py       # Planejamento
│       │       └── reflect.py    # Reflexão
│       └── utils.py              # Configurações/API key
│
└── requirements.txt
```

#### Conceitos-Chave para Extrair

**1. Scratch (Identidade)**
```python
# Estrutura simplificada do scratch.py
class Scratch:
    def __init__(self):
        self.name = ""
        self.first_name = ""
        self.last_name = ""
        self.age = 0
        self.innate = ""           # Traços inatos
        self.learned = ""          # Conhecimentos aprendidos
        self.currently = ""        # Estado atual
        self.lifestyle = ""        # Estilo de vida
        self.daily_plan = []       # Plano do dia
```

**2. Associative Memory (Memória)**
```python
# Estrutura simplificada
class AssociativeMemory:
    def __init__(self):
        self.seq_event = []        # Eventos em sequência
        self.seq_thought = []      # Pensamentos
        self.seq_chat = []         # Conversas
        
    def add_event(self, event):
        # Adiciona evento com timestamp e embedding
        pass
        
    def retrieve(self, query, n=5):
        # Recupera n memórias mais relevantes para a query
        pass
```

**3. Reflection (Reflexão)**
```python
# Processo de reflexão
def reflect(persona, anchor):
    # 1. Recupera memórias relacionadas ao anchor
    memories = persona.memory.retrieve(anchor, n=100)
    
    # 2. Gera perguntas sobre as memórias
    questions = generate_questions(memories)
    
    # 3. Para cada pergunta, sintetiza uma reflexão
    for q in questions:
        relevant = persona.memory.retrieve(q, n=5)
        insight = synthesize_insight(relevant)
        persona.memory.add_thought(insight)
```

### 3.2 Repositório: genagents

**URL:** https://github.com/StanfordHCI/genagents

#### Estrutura de Arquivos
```
genagents/
├── genagents/
│   ├── genagents.py              # Classe principal GenerativeAgent
│   └── modules/
│       ├── interaction.py        # Respostas categóricas/numéricas
│       └── memory_stream.py      # Gerenciamento de memória
│
├── simulation_engine/
│   ├── settings.py               # Configurações
│   ├── global_methods.py         # Funções auxiliares
│   ├── gpt_structure.py          # Interface com LLM
│   ├── llm_json_parser.py        # Parser de JSON
│   └── prompt_template/          # Prompts do sistema
│
├── agent_bank/
│   └── populations/
│       ├── gss_agents/           # Agentes baseados em GSS
│       └── single_agent/         # Exemplo de agente
│
└── main.py                       # Exemplo de uso
```

#### Conceitos-Chave para Extrair

**1. GenerativeAgent (Classe Principal)**
```python
from genagents.genagents import GenerativeAgent

# Criar agente
agent = GenerativeAgent()

# Definir identidade
agent.update_scratch({
    "first_name": "Maria",
    "last_name": "Silva",
    "age": 35,
    "occupation": "Professora",
    "location": "Ceilândia, DF",
    "income_range": "3-5 salários mínimos",
    "education": "Superior completo",
    "religion": "Católica",
    "political_leaning": "Centro-esquerda"
})
```

**2. Respostas Categóricas**
```python
# Perguntar com opções de resposta
questions = {
    "Em quem você pretende votar para governador?": [
        "Candidato A",
        "Candidato B", 
        "Candidato C",
        "Nenhum/Branco/Nulo",
        "Ainda não decidi"
    ]
}

response = agent.categorical_resp(questions)
# Retorna: {"responses": {"Em quem você...": "Candidato B"}}
```

**3. Respostas Numéricas**
```python
# Perguntar com escala
questions = {
    "De 0 a 10, como você avalia a gestão atual?": [0, 10]
}

response = agent.numerical_resp(questions, float_resp=False)
# Retorna: {"responses": {"De 0 a 10...": 6}}
```

**4. Respostas Abertas**
```python
# Entrevista aberta
dialogue = [
    ("Entrevistador", "O que você acha da situação do transporte público no DF?"),
]

response = agent.utterance(dialogue)
# Retorna resposta elaborada baseada na identidade do agente
```

**5. Memória e Reflexão**
```python
# Adicionar memória
agent.remember("Vi reportagem sobre escândalo do candidato X", time_step=1)
agent.remember("Perdi o emprego no mês passado", time_step=2)

# Gerar reflexão
agent.reflect(anchor="situação econômica", time_step=3)

# Agora as respostas do agente consideram essas memórias
```

---

## 4. Arquitetura do Sistema Proposto

### 4.1 Visão Geral

```
┌─────────────────────────────────────────────────────────────────┐
│              SISTEMA SIMULADOR DE ELEITORES DF                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    1. BANCO DE AGENTES                   │   │
│  │  ┌─────────┐ ┌─────────┐ ┌─────────┐     ┌─────────┐   │   │
│  │  │Agente 1 │ │Agente 2 │ │Agente 3 │ ... │Agente400│   │   │
│  │  │Ceilândia│ │Pl.Piloto│ │Taguating│     │Samambaia│   │   │
│  │  │35 anos  │ │28 anos  │ │45 anos  │     │52 anos  │   │   │
│  │  └─────────┘ └─────────┘ └─────────┘     └─────────┘   │   │
│  └─────────────────────────────────────────────────────────┘   │
│                              │                                  │
│                              ▼                                  │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    2. MOTOR DE SIMULAÇÃO                 │   │
│  │                                                          │   │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐   │   │
│  │  │   SISTEMA    │  │   SISTEMA    │  │   SISTEMA    │   │   │
│  │  │ ENTREVISTA   │  │  NOTÍCIAS    │  │  REFLEXÃO    │   │   │
│  │  └──────────────┘  └──────────────┘  └──────────────┘   │   │
│  │                                                          │   │
│  │  • Perguntas categóricas    • Injetar notícias          │   │
│  │  • Perguntas numéricas      • Medir impacto             │   │
│  │  • Perguntas abertas        • Gerar memórias            │   │
│  └─────────────────────────────────────────────────────────┘   │
│                              │                                  │
│                              ▼                                  │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    3. PAINEL DE ANÁLISE                  │   │
│  │                                                          │   │
│  │  📊 Gráficos    📈 Tendências    📋 Relatórios          │   │
│  │  • Por RA       • Antes/depois   • Exportar Excel       │   │
│  │  • Por idade    • Séries tempo   • Exportar PDF         │   │
│  │  • Por renda    • Correlações    • Segmentações         │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 4.2 Estrutura de Diretórios do Projeto

```
simulador-eleitores-df/
│
├── CLAUDE.md                     # Instruções para Claude Code
├── requirements.txt              # Dependências Python
├── config.py                     # Configurações (API key, etc)
│
├── core/                         # Núcleo do sistema
│   ├── __init__.py
│   ├── agent.py                  # Classe ElectorAgent
│   ├── memory.py                 # Sistema de memória
│   ├── identity.py               # Gerador de identidades
│   └── llm_interface.py          # Interface com Claude/GPT
│
├── simulation/                   # Motor de simulação
│   ├── __init__.py
│   ├── interviewer.py            # Sistema de entrevistas
│   ├── news_injector.py          # Injetor de notícias
│   ├── reflection.py             # Sistema de reflexão
│   └── batch_processor.py        # Processamento em lote
│
├── data/                         # Dados
│   ├── demographics/             # Dados demográficos do DF
│   │   ├── ibge_df_2022.json
│   │   ├── tse_eleitores_df.json
│   │   └── regioes_admin.json
│   ├── agents/                   # Agentes salvos
│   │   └── population_400/       # População de 400 eleitores
│   ├── templates/                # Templates de identidade
│   │   └── perfis_base.json
│   └── surveys/                  # Questionários
│       ├── intencao_voto.json
│       └── avaliacao_governo.json
│
├── analysis/                     # Análise de resultados
│   ├── __init__.py
│   ├── aggregator.py             # Agregação de respostas
│   ├── visualizer.py             # Geração de gráficos
│   └── reporter.py               # Geração de relatórios
│
├── interface/                    # Interface (opcional)
│   ├── cli.py                    # Interface de linha de comando
│   └── web/                      # Interface web (Streamlit)
│       └── app.py
│
├── tests/                        # Testes
│   ├── test_agent.py
│   └── test_simulation.py
│
└── outputs/                      # Resultados
    ├── reports/
    └── exports/
```

### 4.3 Fluxo de Dados

```
┌─────────────────────────────────────────────────────────────────┐
│                      FLUXO DE DADOS                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. INICIALIZAÇÃO                                               │
│  ─────────────────                                              │
│                                                                 │
│  Dados IBGE/TSE ──▶ Estratificação ──▶ Geração de Identidades  │
│                           │                    │                │
│                           │                    ▼                │
│                           │           ┌─────────────────┐       │
│                           │           │  400 Agentes    │       │
│                           │           │  com identidade │       │
│                           │           │  completa       │       │
│                           │           └─────────────────┘       │
│                           │                    │                │
│                           ▼                    │                │
│                    Validação da               │                │
│                    representatividade          │                │
│                                               │                │
│  2. EXECUÇÃO DE PESQUISA                      ▼                │
│  ────────────────────────                                       │
│                                                                 │
│  Questionário ──▶ Para cada agente:                            │
│                   ├── Recupera identidade                       │
│                   ├── Recupera memórias relevantes              │
│                   ├── Gera resposta via LLM                     │
│                   └── Armazena resposta                         │
│                           │                                     │
│                           ▼                                     │
│                   Agregação estatística                         │
│                           │                                     │
│                           ▼                                     │
│                   Relatório + Visualizações                     │
│                                                                 │
│  3. INJEÇÃO DE NOTÍCIA                                          │
│  ─────────────────────                                          │
│                                                                 │
│  Notícia ──▶ Para cada agente:                                 │
│              ├── Gera memória do evento                         │
│              ├── Gera reflexão sobre o evento                   │
│              └── Atualiza estado interno                        │
│                      │                                          │
│                      ▼                                          │
│              Nova pesquisa (medir impacto)                      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 5. Dados Demográficos do Eleitorado do DF

### 5.1 Regiões Administrativas do DF

Para criar uma amostra representativa, precisamos entender a distribuição do eleitorado por Região Administrativa (RA):

```
┌─────────────────────────────────────────────────────────────────┐
│          DISTRIBUIÇÃO POPULACIONAL POR RA (Aproximada)          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  RA                          Pop.      % Total   Agentes (400)  │
│  ─────────────────────────────────────────────────────────────  │
│  Ceilândia                   490.000    16.5%        66         │
│  Taguatinga                  230.000     7.7%        31         │
│  Samambaia                   270.000     9.1%        36         │
│  Plano Piloto (Asa Sul/Norte) 220.000    7.4%        30         │
│  Águas Claras                160.000     5.4%        22         │
│  Recanto das Emas            150.000     5.0%        20         │
│  Gama                        140.000     4.7%        19         │
│  Santa Maria                 135.000     4.5%        18         │
│  Planaltina                  210.000     7.1%        28         │
│  Sobradinho                  100.000     3.4%        14         │
│  São Sebastião               130.000     4.4%        18         │
│  Vicente Pires                80.000     2.7%        11         │
│  Guará                       150.000     5.0%        20         │
│  Paranoá                      70.000     2.4%        10         │
│  Itapoã                       80.000     2.7%        11         │
│  Outras RAs                  360.000    12.0%        46         │
│  ─────────────────────────────────────────────────────────────  │
│  TOTAL                     2.975.000   100.0%       400         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 5.2 Estratificação Demográfica

Além da RA, precisamos estratificar por outras variáveis:

```
┌─────────────────────────────────────────────────────────────────┐
│              VARIÁVEIS DE ESTRATIFICAÇÃO                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  GÊNERO                                                         │
│  ───────                                                        │
│  • Masculino: 47%    (188 agentes)                              │
│  • Feminino:  53%    (212 agentes)                              │
│                                                                 │
│  FAIXA ETÁRIA                                                   │
│  ────────────                                                   │
│  • 16-24 anos: 15%   (60 agentes)                               │
│  • 25-34 anos: 22%   (88 agentes)                               │
│  • 35-44 anos: 20%   (80 agentes)                               │
│  • 45-54 anos: 18%   (72 agentes)                               │
│  • 55-64 anos: 14%   (56 agentes)                               │
│  • 65+ anos:  11%    (44 agentes)                               │
│                                                                 │
│  ESCOLARIDADE                                                   │
│  ────────────                                                   │
│  • Fundamental incompleto:  12%   (48 agentes)                  │
│  • Fundamental completo:    15%   (60 agentes)                  │
│  • Médio incompleto:        10%   (40 agentes)                  │
│  • Médio completo:          28%   (112 agentes)                 │
│  • Superior incompleto:     12%   (48 agentes)                  │
│  • Superior completo:       23%   (92 agentes)                  │
│                                                                 │
│  RENDA FAMILIAR                                                 │
│  ──────────────                                                 │
│  • Até 1 SM:           15%   (60 agentes)                       │
│  • 1-2 SM:             25%   (100 agentes)                      │
│  • 2-5 SM:             35%   (140 agentes)                      │
│  • 5-10 SM:            15%   (60 agentes)                       │
│  • 10+ SM:             10%   (40 agentes)                       │
│                                                                 │
│  RELIGIÃO                                                       │
│  ────────                                                       │
│  • Católica:           45%   (180 agentes)                      │
│  • Evangélica:         30%   (120 agentes)                      │
│  • Sem religião:       15%   (60 agentes)                       │
│  • Outras:             10%   (40 agentes)                       │
│                                                                 │
│  ORIENTAÇÃO POLÍTICA (estimativa)                               │
│  ─────────────────────────────────                              │
│  • Direita/Centro-direita:   35%   (140 agentes)                │
│  • Centro:                   25%   (100 agentes)                │
│  • Esquerda/Centro-esquerda: 30%   (120 agentes)                │
│  • Sem posição definida:     10%   (40 agentes)                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 5.3 Arquivo de Configuração Demográfica

```json
{
  "regioes_administrativas": [
    {"nome": "Ceilândia", "codigo": "RA_IX", "populacao": 490000, "renda_media": 2.5, "perfil": "popular"},
    {"nome": "Taguatinga", "codigo": "RA_III", "populacao": 230000, "renda_media": 4.0, "perfil": "medio"},
    {"nome": "Plano Piloto", "codigo": "RA_I", "populacao": 220000, "renda_media": 12.0, "perfil": "alta_renda"},
    {"nome": "Samambaia", "codigo": "RA_XII", "populacao": 270000, "renda_media": 2.0, "perfil": "popular"},
    {"nome": "Águas Claras", "codigo": "RA_XX", "populacao": 160000, "renda_media": 8.0, "perfil": "media_alta"}
  ],
  
  "distribuicao_genero": {"masculino": 0.47, "feminino": 0.53},
  
  "distribuicao_idade": [
    {"faixa": "16-24", "proporcao": 0.15},
    {"faixa": "25-34", "proporcao": 0.22},
    {"faixa": "35-44", "proporcao": 0.20},
    {"faixa": "45-54", "proporcao": 0.18},
    {"faixa": "55-64", "proporcao": 0.14},
    {"faixa": "65+", "proporcao": 0.11}
  ],
  
  "distribuicao_escolaridade": [
    {"nivel": "fundamental_incompleto", "proporcao": 0.12},
    {"nivel": "fundamental_completo", "proporcao": 0.15},
    {"nivel": "medio_incompleto", "proporcao": 0.10},
    {"nivel": "medio_completo", "proporcao": 0.28},
    {"nivel": "superior_incompleto", "proporcao": 0.12},
    {"nivel": "superior_completo", "proporcao": 0.23}
  ],
  
  "distribuicao_renda_sm": [
    {"faixa": "ate_1", "proporcao": 0.15},
    {"faixa": "1_a_2", "proporcao": 0.25},
    {"faixa": "2_a_5", "proporcao": 0.35},
    {"faixa": "5_a_10", "proporcao": 0.15},
    {"faixa": "acima_10", "proporcao": 0.10}
  ],
  
  "distribuicao_religiao": [
    {"religiao": "catolica", "proporcao": 0.45},
    {"religiao": "evangelica", "proporcao": 0.30},
    {"religiao": "sem_religiao", "proporcao": 0.15},
    {"religiao": "outras", "proporcao": 0.10}
  ]
}
```

---

## 6. Criando a Amostra de 400 Eleitores

### 6.1 Algoritmo de Geração Estratificada

```python
"""
Algoritmo para gerar 400 agentes representativos do eleitorado do DF.
"""

import random
import json
from dataclasses import dataclass
from typing import List, Dict

@dataclass
class ElectorProfile:
    """Perfil demográfico de um eleitor."""
    id: int
    nome: str
    idade: int
    genero: str
    ra: str                    # Região Administrativa
    escolaridade: str
    renda_sm: float           # Renda em salários mínimos
    religiao: str
    ocupacao: str
    estado_civil: str
    tem_filhos: bool
    orientacao_politica: str
    preocupacoes: List[str]   # Principais preocupações
    historia_pessoal: str     # Narrativa pessoal

class ElectorGenerator:
    """Gerador de perfis de eleitores estratificados."""
    
    def __init__(self, config_path: str):
        with open(config_path) as f:
            self.config = json.load(f)
        
        self.nomes_masculinos = [
            "José", "Carlos", "Paulo", "Pedro", "João", "Lucas", 
            "Marcos", "Antonio", "Francisco", "Rafael", "Bruno",
            "Luiz", "Fernando", "Ricardo", "Marcelo", "Eduardo"
        ]
        self.nomes_femininos = [
            "Maria", "Ana", "Francisca", "Adriana", "Juliana",
            "Márcia", "Fernanda", "Patricia", "Aline", "Amanda",
            "Sandra", "Camila", "Bruna", "Letícia", "Luciana"
        ]
        self.sobrenomes = [
            "Silva", "Santos", "Oliveira", "Souza", "Lima",
            "Pereira", "Costa", "Rodrigues", "Almeida", "Nascimento",
            "Ferreira", "Carvalho", "Gomes", "Ribeiro", "Martins"
        ]
        
        self.ocupacoes_por_escolaridade = {
            "fundamental_incompleto": [
                "Diarista", "Pedreiro", "Servente", "Vendedor ambulante",
                "Auxiliar de serviços gerais", "Cuidador de idosos"
            ],
            "fundamental_completo": [
                "Porteiro", "Vigilante", "Motorista", "Cozinheiro",
                "Eletricista", "Mecânico", "Manicure"
            ],
            "medio_incompleto": [
                "Atendente", "Operador de caixa", "Recepcionista",
                "Auxiliar administrativo", "Vendedor"
            ],
            "medio_completo": [
                "Técnico em enfermagem", "Vendedor", "Assistente administrativo",
                "Motorista de aplicativo", "Comerciante", "Corretor"
            ],
            "superior_incompleto": [
                "Estagiário", "Atendente", "Auxiliar técnico",
                "Freelancer", "Empreendedor"
            ],
            "superior_completo": [
                "Professor", "Engenheiro", "Advogado", "Contador",
                "Enfermeiro", "Administrador", "Servidor público",
                "Analista de sistemas", "Médico", "Psicólogo"
            ]
        }
        
        self.preocupacoes_por_perfil = {
            "popular": [
                "Desemprego", "Custo de vida", "Violência", 
                "Saúde pública", "Transporte público", "Moradia"
            ],
            "medio": [
                "Segurança", "Educação dos filhos", "Impostos",
                "Transporte", "Saúde", "Corrupção"
            ],
            "alta_renda": [
                "Segurança", "Corrupção", "Economia", 
                "Infraestrutura", "Impostos", "Meio ambiente"
            ]
        }
    
    def _gerar_nome(self, genero: str) -> str:
        """Gera nome completo aleatório."""
        if genero == "masculino":
            primeiro = random.choice(self.nomes_masculinos)
        else:
            primeiro = random.choice(self.nomes_femininos)
        sobrenome = random.choice(self.sobrenomes)
        return f"{primeiro} {sobrenome}"
    
    def _gerar_idade(self, faixa: str) -> int:
        """Gera idade dentro da faixa."""
        faixas = {
            "16-24": (16, 24),
            "25-34": (25, 34),
            "35-44": (35, 44),
            "45-54": (45, 54),
            "55-64": (55, 64),
            "65+": (65, 85)
        }
        min_idade, max_idade = faixas[faixa]
        return random.randint(min_idade, max_idade)
    
    def _gerar_renda(self, faixa: str) -> float:
        """Gera renda em salários mínimos."""
        faixas = {
            "ate_1": (0.5, 1.0),
            "1_a_2": (1.0, 2.0),
            "2_a_5": (2.0, 5.0),
            "5_a_10": (5.0, 10.0),
            "acima_10": (10.0, 30.0)
        }
        min_renda, max_renda = faixas[faixa]
        return round(random.uniform(min_renda, max_renda), 1)
    
    def _gerar_historia(self, perfil: ElectorProfile) -> str:
        """Gera narrativa pessoal baseada no perfil."""
        # Esta é uma versão simplificada
        # Na implementação real, use o LLM para gerar histórias ricas
        
        historia = f"{perfil.nome} tem {perfil.idade} anos e mora em {perfil.ra}. "
        historia += f"Trabalha como {perfil.ocupacao} e "
        
        if perfil.renda_sm < 2:
            historia += "enfrenta dificuldades financeiras no dia a dia. "
        elif perfil.renda_sm < 5:
            historia += "consegue manter as contas em dia com esforço. "
        else:
            historia += "tem uma situação financeira estável. "
        
        if perfil.tem_filhos:
            historia += "Tem filhos e se preocupa muito com o futuro deles. "
        
        if perfil.religiao != "sem_religiao":
            historia += f"É {perfil.religiao} praticante. "
        
        historia += f"Suas principais preocupações são: {', '.join(perfil.preocupacoes[:3])}."
        
        return historia
    
    def gerar_populacao(self, n: int = 400) -> List[ElectorProfile]:
        """Gera população estratificada de n eleitores."""
        eleitores = []
        id_counter = 1
        
        # Distribuir por RA proporcionalmente
        for ra_config in self.config["regioes_administrativas"]:
            ra_nome = ra_config["nome"]
            ra_pop = ra_config["populacao"]
            total_pop = sum(r["populacao"] for r in self.config["regioes_administrativas"])
            n_agentes_ra = round(n * (ra_pop / total_pop))
            
            for _ in range(n_agentes_ra):
                # Sortear características demográficas
                genero = random.choices(
                    ["masculino", "feminino"],
                    weights=[0.47, 0.53]
                )[0]
                
                faixa_idade = random.choices(
                    [f["faixa"] for f in self.config["distribuicao_idade"]],
                    weights=[f["proporcao"] for f in self.config["distribuicao_idade"]]
                )[0]
                
                escolaridade = random.choices(
                    [e["nivel"] for e in self.config["distribuicao_escolaridade"]],
                    weights=[e["proporcao"] for e in self.config["distribuicao_escolaridade"]]
                )[0]
                
                faixa_renda = random.choices(
                    [r["faixa"] for r in self.config["distribuicao_renda_sm"]],
                    weights=[r["proporcao"] for r in self.config["distribuicao_renda_sm"]]
                )[0]
                
                religiao = random.choices(
                    [r["religiao"] for r in self.config["distribuicao_religiao"]],
                    weights=[r["proporcao"] for r in self.config["distribuicao_religiao"]]
                )[0]
                
                # Criar perfil
                perfil = ElectorProfile(
                    id=id_counter,
                    nome=self._gerar_nome(genero),
                    idade=self._gerar_idade(faixa_idade),
                    genero=genero,
                    ra=ra_nome,
                    escolaridade=escolaridade,
                    renda_sm=self._gerar_renda(faixa_renda),
                    religiao=religiao,
                    ocupacao=random.choice(self.ocupacoes_por_escolaridade[escolaridade]),
                    estado_civil=random.choice(["solteiro", "casado", "divorciado", "viúvo"]),
                    tem_filhos=random.random() < 0.6,  # 60% tem filhos
                    orientacao_politica=random.choice([
                        "direita", "centro-direita", "centro", 
                        "centro-esquerda", "esquerda", "indefinido"
                    ]),
                    preocupacoes=random.sample(
                        self.preocupacoes_por_perfil[ra_config["perfil"]], 
                        k=4
                    ),
                    historia_pessoal=""
                )
                
                # Gerar história
                perfil.historia_pessoal = self._gerar_historia(perfil)
                
                eleitores.append(perfil)
                id_counter += 1
        
        return eleitores[:n]  # Garantir exatamente n
```

### 6.2 Enriquecimento com LLM

Após gerar a estrutura básica, use o Claude para enriquecer cada perfil:

```python
def enriquecer_perfil_com_llm(perfil: ElectorProfile, client) -> Dict:
    """Usa LLM para criar história rica e memórias iniciais."""
    
    prompt = f"""
    Você é um especialista em criar perfis realistas de eleitores brasileiros.
    
    Dados básicos do eleitor:
    - Nome: {perfil.nome}
    - Idade: {perfil.idade} anos
    - Gênero: {perfil.genero}
    - Mora em: {perfil.ra}, Distrito Federal
    - Escolaridade: {perfil.escolaridade}
    - Renda: {perfil.renda_sm} salários mínimos
    - Ocupação: {perfil.ocupacao}
    - Religião: {perfil.religiao}
    - Estado civil: {perfil.estado_civil}
    - Tem filhos: {"Sim" if perfil.tem_filhos else "Não"}
    - Orientação política: {perfil.orientacao_politica}
    - Principais preocupações: {', '.join(perfil.preocupacoes)}
    
    Crie um perfil detalhado incluindo:
    
    1. HISTÓRIA DE VIDA (3-4 parágrafos)
    Inclua: origem, trajetória de vida, principais marcos, 
    situação atual, sonhos e frustrações.
    
    2. OPINIÕES POLÍTICAS (2-3 parágrafos)
    Inclua: como formou suas opiniões, referências que segue,
    o que valoriza em um político, decepções passadas.
    
    3. MEMÓRIAS RELEVANTES (lista de 5-10 memórias)
    Eventos que moldaram sua visão de mundo, experiências com 
    serviços públicos, situações que reforçaram suas crenças.
    
    4. ESTILO DE COMUNICAÇÃO
    Como essa pessoa se expressa? Usa gírias? É formal?
    É expansiva ou reservada?
    
    Responda em JSON com as chaves: historia_vida, opinioes_politicas, 
    memorias (lista), estilo_comunicacao.
    """
    
    response = client.messages.create(
        model="claude-sonnet-4-5-20250929",
        max_tokens=2000,
        messages=[{"role": "user", "content": prompt}]
    )
    
    return json.loads(response.content[0].text)
```

---

## 7. Implementação Passo a Passo

### 7.1 Configuração Inicial

#### Passo 1: Criar estrutura de projeto

```bash
# No terminal, com Claude Code
mkdir simulador-eleitores-df
cd simulador-eleitores-df

# Criar estrutura
mkdir -p core simulation data/demographics data/agents data/surveys
mkdir -p analysis interface outputs/reports
```

#### Passo 2: Criar requirements.txt

```
# requirements.txt
anthropic>=0.40.0
openai>=1.0.0
pandas>=2.0.0
numpy>=1.24.0
matplotlib>=3.7.0
seaborn>=0.12.0
plotly>=5.15.0
streamlit>=1.25.0
pydantic>=2.0.0
python-dotenv>=1.0.0
tqdm>=4.65.0
```

#### Passo 3: Criar config.py

```python
# config.py
import os
from pathlib import Path
from dotenv import load_dotenv

load_dotenv()

# Diretórios
BASE_DIR = Path(__file__).resolve().parent
DATA_DIR = BASE_DIR / "data"
AGENTS_DIR = DATA_DIR / "agents"
OUTPUTS_DIR = BASE_DIR / "outputs"

# API
ANTHROPIC_API_KEY = os.getenv("ANTHROPIC_API_KEY")
OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")

# Configurações do LLM
DEFAULT_MODEL = "claude-sonnet-4-5-20250929"  # Balanceado custo/qualidade
PREMIUM_MODEL = "claude-opus-4-5-20251101"    # Para tarefas complexas
FAST_MODEL = "claude-haiku-3-5-20241022"      # Para tarefas simples

# Configurações de simulação
POPULATION_SIZE = 400
MAX_CONCURRENT_REQUESTS = 10
REQUEST_DELAY_SECONDS = 0.5
```

### 7.2 Classe Principal: ElectorAgent

```python
# core/agent.py
"""
Agente Generativo representando um eleitor do DF.
Baseado na arquitetura do GenAgents de Stanford.
"""

import json
from dataclasses import dataclass, field
from typing import List, Dict, Any, Optional
from datetime import datetime
import anthropic

@dataclass
class Memory:
    """Uma memória do agente."""
    id: int
    content: str
    timestamp: datetime
    type: str  # "event", "thought", "reflection"
    importance: float  # 0-1
    embedding: Optional[List[float]] = None

@dataclass
class ElectorAgent:
    """
    Agente generativo representando um eleitor do DF.
    """
    # Identidade básica
    id: int
    nome: str
    idade: int
    genero: str
    ra: str  # Região Administrativa
    
    # Dados socioeconômicos
    escolaridade: str
    renda_sm: float
    ocupacao: str
    religiao: str
    estado_civil: str
    tem_filhos: bool
    
    # Perfil político
    orientacao_politica: str
    preocupacoes: List[str]
    
    # Narrativas
    historia_vida: str = ""
    opinioes_politicas: str = ""
    estilo_comunicacao: str = ""
    
    # Sistema de memória
    memorias: List[Memory] = field(default_factory=list)
    reflexoes: List[str] = field(default_factory=list)
    
    # Estado interno
    humor_atual: str = "neutro"
    ultima_atualizacao: datetime = field(default_factory=datetime.now)
    
    # Cliente LLM
    _client: Any = field(default=None, repr=False)
    
    def __post_init__(self):
        """Inicializa cliente após criação."""
        if self._client is None:
            from config import ANTHROPIC_API_KEY
            self._client = anthropic.Anthropic(api_key=ANTHROPIC_API_KEY)
    
    def get_identity_prompt(self) -> str:
        """Retorna prompt descrevendo a identidade do agente."""
        return f"""
Você é {self.nome}, um(a) eleitor(a) do Distrito Federal com as seguintes características:

DADOS PESSOAIS:
- Idade: {self.idade} anos
- Gênero: {self.genero}
- Mora em: {self.ra}, DF
- Escolaridade: {self.escolaridade}
- Ocupação: {self.ocupacao}
- Renda: {self.renda_sm} salários mínimos
- Religião: {self.religiao}
- Estado civil: {self.estado_civil}
- Tem filhos: {"Sim" if self.tem_filhos else "Não"}

PERFIL POLÍTICO:
- Orientação: {self.orientacao_politica}
- Principais preocupações: {', '.join(self.preocupacoes)}

HISTÓRIA DE VIDA:
{self.historia_vida}

OPINIÕES POLÍTICAS:
{self.opinioes_politicas}

ESTILO DE COMUNICAÇÃO:
{self.estilo_comunicacao}

MEMÓRIAS RECENTES:
{self._format_recent_memories()}

Responda SEMPRE como {self.nome} responderia, mantendo consistência com seu perfil, 
história, valores e forma de se expressar. Não quebre o personagem.
"""
    
    def _format_recent_memories(self, n: int = 10) -> str:
        """Formata memórias recentes para o prompt."""
        if not self.memorias:
            return "Nenhuma memória registrada ainda."
        
        recent = sorted(self.memorias, key=lambda m: m.timestamp, reverse=True)[:n]
        return "\n".join([f"- {m.content}" for m in recent])
    
    def remember(self, content: str, importance: float = 0.5, 
                 memory_type: str = "event") -> Memory:
        """Adiciona uma memória ao agente."""
        memory = Memory(
            id=len(self.memorias) + 1,
            content=content,
            timestamp=datetime.now(),
            type=memory_type,
            importance=importance
        )
        self.memorias.append(memory)
        return memory
    
    def reflect(self, anchor: str) -> str:
        """
        Gera reflexão sobre um tema baseado nas memórias.
        """
        relevant_memories = self._retrieve_memories(anchor, n=10)
        
        prompt = f"""
{self.get_identity_prompt()}

Com base nas suas experiências e memórias, reflita sobre: {anchor}

Memórias relevantes:
{chr(10).join([f'- {m.content}' for m in relevant_memories])}

Gere uma reflexão pessoal de 2-3 frases sobre este tema, 
considerando sua história de vida e valores.
"""
        
        response = self._client.messages.create(
            model="claude-sonnet-4-5-20250929",
            max_tokens=300,
            messages=[{"role": "user", "content": prompt}]
        )
        
        reflection = response.content[0].text
        self.reflexoes.append(reflection)
        self.remember(f"Reflexão sobre {anchor}: {reflection}", 
                      importance=0.7, memory_type="reflection")
        
        return reflection
    
    def _retrieve_memories(self, query: str, n: int = 5) -> List[Memory]:
        """Recupera memórias relevantes para uma query."""
        # Versão simplificada: retorna as n mais recentes
        # Na versão completa: usar embeddings para busca semântica
        return sorted(self.memorias, 
                      key=lambda m: m.importance, 
                      reverse=True)[:n]
    
    def categorical_response(self, question: str, 
                            options: List[str]) -> Dict[str, Any]:
        """
        Responde pergunta com opções categóricas.
        Retorna a opção escolhida e justificativa.
        """
        options_str = "\n".join([f"{i+1}. {opt}" for i, opt in enumerate(options)])
        
        prompt = f"""
{self.get_identity_prompt()}

PERGUNTA: {question}

OPÇÕES:
{options_str}

Responda como {self.nome}. Escolha UMA opção e justifique brevemente 
(2-3 frases) por que você escolheu essa opção, considerando sua 
história de vida, valores e experiências.

Responda em JSON:
{{
    "opcao_numero": <número da opção>,
    "opcao_texto": "<texto da opção>",
    "justificativa": "<sua justificativa>"
}}
"""
        
        response = self._client.messages.create(
            model="claude-sonnet-4-5-20250929",
            max_tokens=300,
            messages=[{"role": "user", "content": prompt}]
        )
        
        result = json.loads(response.content[0].text)
        
        # Registrar na memória
        self.remember(
            f"Respondi '{result['opcao_texto']}' para: {question}",
            importance=0.6,
            memory_type="thought"
        )
        
        return result
    
    def numerical_response(self, question: str, 
                          min_val: int, max_val: int) -> Dict[str, Any]:
        """
        Responde pergunta com escala numérica.
        """
        prompt = f"""
{self.get_identity_prompt()}

PERGUNTA: {question}

Responda com um número de {min_val} a {max_val}.
Justifique brevemente (2-3 frases) sua resposta.

Responda em JSON:
{{
    "valor": <número>,
    "justificativa": "<sua justificativa>"
}}
"""
        
        response = self._client.messages.create(
            model="claude-sonnet-4-5-20250929",
            max_tokens=200,
            messages=[{"role": "user", "content": prompt}]
        )
        
        result = json.loads(response.content[0].text)
        
        self.remember(
            f"Avaliei {result['valor']} para: {question}",
            importance=0.5,
            memory_type="thought"
        )
        
        return result
    
    def open_response(self, question: str) -> str:
        """
        Responde pergunta aberta.
        """
        prompt = f"""
{self.get_identity_prompt()}

PERGUNTA: {question}

Responda como {self.nome} responderia em uma conversa informal.
Use seu estilo de comunicação natural.
Resposta de 3-5 frases.
"""
        
        response = self._client.messages.create(
            model="claude-sonnet-4-5-20250929",
            max_tokens=400,
            messages=[{"role": "user", "content": prompt}]
        )
        
        answer = response.content[0].text
        
        self.remember(
            f"Respondi sobre '{question[:50]}...'",
            importance=0.5,
            memory_type="event"
        )
        
        return answer
    
    def react_to_news(self, news: str) -> Dict[str, Any]:
        """
        Reage a uma notícia e atualiza estado interno.
        """
        prompt = f"""
{self.get_identity_prompt()}

Você acabou de ver a seguinte notícia:

"{news}"

Como {self.nome}, reaja a esta notícia:

1. Qual sua reação emocional inicial? (positiva/negativa/neutra/mista)
2. Isso muda sua opinião sobre algum candidato ou partido? Como?
3. Você comentaria isso com amigos/família? O que diria?

Responda em JSON:
{{
    "reacao_emocional": "<positiva|negativa|neutra|mista>",
    "intensidade": <1-10>,
    "muda_opiniao": <true|false>,
    "como_muda": "<descrição ou null>",
    "comentario": "<o que diria para amigos>"
}}
"""
        
        response = self._client.messages.create(
            model="claude-sonnet-4-5-20250929",
            max_tokens=400,
            messages=[{"role": "user", "content": prompt}]
        )
        
        result = json.loads(response.content[0].text)
        
        # Registrar memória do evento
        self.remember(
            f"Vi notícia: {news[:100]}... Reação: {result['reacao_emocional']}",
            importance=0.7 if result['muda_opiniao'] else 0.4,
            memory_type="event"
        )
        
        # Gerar reflexão se a notícia for impactante
        if result['intensidade'] >= 7:
            self.reflect(f"notícia sobre {news[:50]}")
        
        return result
    
    def save(self, path: str):
        """Salva agente em arquivo JSON."""
        data = {
            "id": self.id,
            "nome": self.nome,
            "idade": self.idade,
            "genero": self.genero,
            "ra": self.ra,
            "escolaridade": self.escolaridade,
            "renda_sm": self.renda_sm,
            "ocupacao": self.ocupacao,
            "religiao": self.religiao,
            "estado_civil": self.estado_civil,
            "tem_filhos": self.tem_filhos,
            "orientacao_politica": self.orientacao_politica,
            "preocupacoes": self.preocupacoes,
            "historia_vida": self.historia_vida,
            "opinioes_politicas": self.opinioes_politicas,
            "estilo_comunicacao": self.estilo_comunicacao,
            "memorias": [
                {
                    "id": m.id,
                    "content": m.content,
                    "timestamp": m.timestamp.isoformat(),
                    "type": m.type,
                    "importance": m.importance
                }
                for m in self.memorias
            ],
            "reflexoes": self.reflexoes
        }
        
        with open(path, 'w', encoding='utf-8') as f:
            json.dump(data, f, ensure_ascii=False, indent=2)
    
    @classmethod
    def load(cls, path: str) -> 'ElectorAgent':
        """Carrega agente de arquivo JSON."""
        with open(path, encoding='utf-8') as f:
            data = json.load(f)
        
        memorias = [
            Memory(
                id=m["id"],
                content=m["content"],
                timestamp=datetime.fromisoformat(m["timestamp"]),
                type=m["type"],
                importance=m["importance"]
            )
            for m in data.get("memorias", [])
        ]
        
        agent = cls(
            id=data["id"],
            nome=data["nome"],
            idade=data["idade"],
            genero=data["genero"],
            ra=data["ra"],
            escolaridade=data["escolaridade"],
            renda_sm=data["renda_sm"],
            ocupacao=data["ocupacao"],
            religiao=data["religiao"],
            estado_civil=data["estado_civil"],
            tem_filhos=data["tem_filhos"],
            orientacao_politica=data["orientacao_politica"],
            preocupacoes=data["preocupacoes"],
            historia_vida=data.get("historia_vida", ""),
            opinioes_politicas=data.get("opinioes_politicas", ""),
            estilo_comunicacao=data.get("estilo_comunicacao", ""),
            memorias=memorias,
            reflexoes=data.get("reflexoes", [])
        )
        
        return agent
```

### 7.3 Sistema de Entrevistas em Lote

```python
# simulation/batch_processor.py
"""
Processador em lote para executar pesquisas em todos os agentes.
"""

import asyncio
from typing import List, Dict, Any, Callable
from tqdm import tqdm
import pandas as pd
from concurrent.futures import ThreadPoolExecutor
import time

from core.agent import ElectorAgent
from config import MAX_CONCURRENT_REQUESTS, REQUEST_DELAY_SECONDS

class BatchProcessor:
    """Processa pesquisas em lote para múltiplos agentes."""
    
    def __init__(self, agents: List[ElectorAgent]):
        self.agents = agents
        self.results = []
    
    def run_categorical_survey(self, 
                               questions: Dict[str, List[str]],
                               show_progress: bool = True) -> pd.DataFrame:
        """
        Executa pesquisa categórica em todos os agentes.
        
        Args:
            questions: Dict de {pergunta: [opções]}
            show_progress: Mostrar barra de progresso
        
        Returns:
            DataFrame com respostas de todos os agentes
        """
        results = []
        
        iterator = tqdm(self.agents, desc="Pesquisando") if show_progress else self.agents
        
        for agent in iterator:
            agent_results = {
                "agent_id": agent.id,
                "nome": agent.nome,
                "ra": agent.ra,
                "idade": agent.idade,
                "genero": agent.genero,
                "escolaridade": agent.escolaridade,
                "renda_sm": agent.renda_sm,
                "religiao": agent.religiao,
                "orientacao_politica": agent.orientacao_politica
            }
            
            for question, options in questions.items():
                try:
                    response = agent.categorical_response(question, options)
                    agent_results[f"resp_{question[:30]}"] = response["opcao_texto"]
                    agent_results[f"just_{question[:30]}"] = response["justificativa"]
                except Exception as e:
                    agent_results[f"resp_{question[:30]}"] = "ERRO"
                    agent_results[f"just_{question[:30]}"] = str(e)
                
                # Rate limiting
                time.sleep(REQUEST_DELAY_SECONDS)
            
            results.append(agent_results)
        
        return pd.DataFrame(results)
    
    def run_numerical_survey(self,
                            questions: Dict[str, tuple],
                            show_progress: bool = True) -> pd.DataFrame:
        """
        Executa pesquisa numérica em todos os agentes.
        
        Args:
            questions: Dict de {pergunta: (min, max)}
        """
        results = []
        
        iterator = tqdm(self.agents, desc="Pesquisando") if show_progress else self.agents
        
        for agent in iterator:
            agent_results = {
                "agent_id": agent.id,
                "nome": agent.nome,
                "ra": agent.ra,
                "idade": agent.idade,
                "genero": agent.genero,
                "orientacao_politica": agent.orientacao_politica
            }
            
            for question, (min_val, max_val) in questions.items():
                try:
                    response = agent.numerical_response(question, min_val, max_val)
                    agent_results[f"valor_{question[:30]}"] = response["valor"]
                    agent_results[f"just_{question[:30]}"] = response["justificativa"]
                except Exception as e:
                    agent_results[f"valor_{question[:30]}"] = None
                    agent_results[f"just_{question[:30]}"] = str(e)
                
                time.sleep(REQUEST_DELAY_SECONDS)
            
            results.append(agent_results)
        
        return pd.DataFrame(results)
    
    def inject_news(self, news: str, show_progress: bool = True) -> pd.DataFrame:
        """
        Injeta notícia em todos os agentes e coleta reações.
        """
        results = []
        
        iterator = tqdm(self.agents, desc="Injetando notícia") if show_progress else self.agents
        
        for agent in iterator:
            try:
                reaction = agent.react_to_news(news)
                results.append({
                    "agent_id": agent.id,
                    "nome": agent.nome,
                    "ra": agent.ra,
                    "orientacao_politica": agent.orientacao_politica,
                    "reacao_emocional": reaction["reacao_emocional"],
                    "intensidade": reaction["intensidade"],
                    "muda_opiniao": reaction["muda_opiniao"],
                    "como_muda": reaction.get("como_muda"),
                    "comentario": reaction["comentario"]
                })
            except Exception as e:
                results.append({
                    "agent_id": agent.id,
                    "nome": agent.nome,
                    "erro": str(e)
                })
            
            time.sleep(REQUEST_DELAY_SECONDS)
        
        return pd.DataFrame(results)
```

---

## 8. Sistema de Entrevistas

### 8.1 Questionários Prontos

```json
// data/surveys/intencao_voto.json
{
  "titulo": "Pesquisa de Intenção de Voto - Governador DF 2026",
  "versao": "1.0",
  "perguntas": [
    {
      "id": "p1",
      "tipo": "categorica",
      "texto": "Se as eleições para governador do DF fossem hoje, em quem você votaria?",
      "opcoes": [
        "Candidato A (situação)",
        "Candidato B (oposição)",
        "Candidato C (terceira via)",
        "Votaria branco ou nulo",
        "Ainda não sei"
      ]
    },
    {
      "id": "p2",
      "tipo": "categorica",
      "texto": "Qual sua opinião sobre a atual gestão do governo do DF?",
      "opcoes": [
        "Ótima",
        "Boa",
        "Regular",
        "Ruim",
        "Péssima",
        "Não sei avaliar"
      ]
    },
    {
      "id": "p3",
      "tipo": "numerica",
      "texto": "De 0 a 10, qual nota você dá para a segurança pública no DF?",
      "min": 0,
      "max": 10
    },
    {
      "id": "p4",
      "tipo": "numerica",
      "texto": "De 0 a 10, qual nota você dá para o transporte público no DF?",
      "min": 0,
      "max": 10
    },
    {
      "id": "p5",
      "tipo": "categorica",
      "texto": "Qual tema deveria ser a prioridade do próximo governador?",
      "opcoes": [
        "Segurança pública",
        "Saúde",
        "Educação",
        "Transporte",
        "Emprego e economia",
        "Moradia",
        "Meio ambiente"
      ]
    },
    {
      "id": "p6",
      "tipo": "aberta",
      "texto": "O que você espera do próximo governador do DF?"
    }
  ]
}
```

### 8.2 Executor de Pesquisas

```python
# simulation/interviewer.py
"""
Sistema de entrevistas estruturadas.
"""

import json
from typing import List, Dict, Any
from pathlib import Path
import pandas as pd

from core.agent import ElectorAgent
from simulation.batch_processor import BatchProcessor

class Interviewer:
    """Conduz entrevistas estruturadas com agentes."""
    
    def __init__(self, agents: List[ElectorAgent]):
        self.agents = agents
        self.processor = BatchProcessor(agents)
    
    def load_survey(self, survey_path: str) -> Dict:
        """Carrega questionário de arquivo JSON."""
        with open(survey_path, encoding='utf-8') as f:
            return json.load(f)
    
    def run_survey(self, survey_path: str) -> Dict[str, pd.DataFrame]:
        """
        Executa pesquisa completa.
        
        Returns:
            Dict com DataFrames separados por tipo de pergunta
        """
        survey = self.load_survey(survey_path)
        results = {
            "categoricas": [],
            "numericas": [],
            "abertas": []
        }
        
        # Separar perguntas por tipo
        cat_questions = {}
        num_questions = {}
        open_questions = []
        
        for p in survey["perguntas"]:
            if p["tipo"] == "categorica":
                cat_questions[p["texto"]] = p["opcoes"]
            elif p["tipo"] == "numerica":
                num_questions[p["texto"]] = (p["min"], p["max"])
            elif p["tipo"] == "aberta":
                open_questions.append(p["texto"])
        
        # Executar cada tipo
        if cat_questions:
            results["categoricas"] = self.processor.run_categorical_survey(cat_questions)
        
        if num_questions:
            results["numericas"] = self.processor.run_numerical_survey(num_questions)
        
        if open_questions:
            # Para perguntas abertas, processar individualmente
            open_results = []
            for agent in self.agents:
                agent_result = {"agent_id": agent.id, "nome": agent.nome}
                for q in open_questions:
                    agent_result[f"resp_{q[:30]}"] = agent.open_response(q)
                open_results.append(agent_result)
            results["abertas"] = pd.DataFrame(open_results)
        
        return results
    
    def quick_poll(self, question: str, options: List[str]) -> pd.DataFrame:
        """Pesquisa rápida com uma única pergunta."""
        return self.processor.run_categorical_survey({question: options})
```

---

## 9. Análise de Impacto de Notícias

### 9.1 Fluxo de Análise

```
┌─────────────────────────────────────────────────────────────────┐
│              ANÁLISE DE IMPACTO DE NOTÍCIAS                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. BASELINE                                                    │
│     ─────────                                                   │
│     Executar pesquisa de intenção de voto ANTES da notícia     │
│     Salvar resultados como T0                                   │
│                                                                 │
│  2. INJEÇÃO                                                     │
│     ────────                                                    │
│     Apresentar notícia a todos os agentes                       │
│     Coletar reações imediatas                                   │
│     Gerar memórias e reflexões                                  │
│                                                                 │
│  3. FOLLOW-UP                                                   │
│     ──────────                                                  │
│     Executar mesma pesquisa APÓS a notícia                      │
│     Salvar resultados como T1                                   │
│                                                                 │
│  4. ANÁLISE                                                     │
│     ────────                                                    │
│     Comparar T0 vs T1                                           │
│     Calcular variação por segmento                              │
│     Identificar grupos mais impactados                          │
│     Gerar relatório                                             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 9.2 Implementação

```python
# simulation/news_impact.py
"""
Análise de impacto de notícias no eleitorado simulado.
"""

import pandas as pd
from typing import List, Dict, Any
from datetime import datetime

from core.agent import ElectorAgent
from simulation.interviewer import Interviewer
from simulation.batch_processor import BatchProcessor

class NewsImpactAnalyzer:
    """Analisa impacto de notícias no eleitorado."""
    
    def __init__(self, agents: List[ElectorAgent]):
        self.agents = agents
        self.interviewer = Interviewer(agents)
        self.processor = BatchProcessor(agents)
        self.experiments = []
    
    def run_experiment(self, 
                       news: str,
                       survey_path: str,
                       experiment_name: str) -> Dict[str, Any]:
        """
        Executa experimento completo de impacto de notícia.
        
        Args:
            news: Texto da notícia a ser injetada
            survey_path: Caminho para o questionário
            experiment_name: Nome identificador do experimento
        
        Returns:
            Dicionário com resultados completos
        """
        print(f"=== Experimento: {experiment_name} ===")
        
        # T0: Baseline
        print("1. Coletando baseline (T0)...")
        t0_results = self.interviewer.run_survey(survey_path)
        
        # Injeção da notícia
        print("2. Injetando notícia...")
        reactions = self.processor.inject_news(news)
        
        # T1: Follow-up
        print("3. Coletando follow-up (T1)...")
        t1_results = self.interviewer.run_survey(survey_path)
        
        # Análise
        print("4. Analisando resultados...")
        analysis = self._analyze_impact(t0_results, t1_results, reactions)
        
        experiment = {
            "nome": experiment_name,
            "timestamp": datetime.now().isoformat(),
            "noticia": news,
            "t0": t0_results,
            "t1": t1_results,
            "reacoes": reactions,
            "analise": analysis
        }
        
        self.experiments.append(experiment)
        
        return experiment
    
    def _analyze_impact(self, 
                        t0: Dict[str, pd.DataFrame],
                        t1: Dict[str, pd.DataFrame],
                        reactions: pd.DataFrame) -> Dict[str, Any]:
        """Analisa diferenças entre T0 e T1."""
        analysis = {}
        
        # Comparar respostas categóricas
        if "categoricas" in t0 and "categoricas" in t1:
            # Encontrar colunas de resposta
            resp_cols = [c for c in t0["categoricas"].columns if c.startswith("resp_")]
            
            for col in resp_cols:
                t0_dist = t0["categoricas"][col].value_counts(normalize=True)
                t1_dist = t1["categoricas"][col].value_counts(normalize=True)
                
                # Calcular variação
                variation = {}
                all_options = set(t0_dist.index) | set(t1_dist.index)
                for opt in all_options:
                    t0_val = t0_dist.get(opt, 0)
                    t1_val = t1_dist.get(opt, 0)
                    variation[opt] = {
                        "t0": round(t0_val * 100, 1),
                        "t1": round(t1_val * 100, 1),
                        "delta": round((t1_val - t0_val) * 100, 1)
                    }
                
                analysis[col] = variation
        
        # Análise de reações
        analysis["reacoes_summary"] = {
            "positivas": len(reactions[reactions["reacao_emocional"] == "positiva"]),
            "negativas": len(reactions[reactions["reacao_emocional"] == "negativa"]),
            "neutras": len(reactions[reactions["reacao_emocional"] == "neutra"]),
            "mistas": len(reactions[reactions["reacao_emocional"] == "mista"]),
            "intensidade_media": reactions["intensidade"].mean(),
            "mudaram_opiniao": len(reactions[reactions["muda_opiniao"] == True])
        }
        
        # Análise por segmento
        for segment in ["ra", "orientacao_politica", "genero"]:
            if segment in reactions.columns:
                seg_analysis = reactions.groupby(segment).agg({
                    "reacao_emocional": lambda x: x.value_counts().to_dict(),
                    "intensidade": "mean",
                    "muda_opiniao": "sum"
                }).to_dict()
                analysis[f"por_{segment}"] = seg_analysis
        
        return analysis
    
    def generate_report(self, experiment_name: str) -> str:
        """Gera relatório textual do experimento."""
        exp = next((e for e in self.experiments if e["nome"] == experiment_name), None)
        if not exp:
            return "Experimento não encontrado."
        
        report = f"""
# Relatório de Impacto: {experiment_name}

## Data: {exp['timestamp']}

## Notícia Testada
{exp['noticia']}

## Resumo das Reações
- Reações positivas: {exp['analise']['reacoes_summary']['positivas']}
- Reações negativas: {exp['analise']['reacoes_summary']['negativas']}
- Reações neutras: {exp['analise']['reacoes_summary']['neutras']}
- Reações mistas: {exp['analise']['reacoes_summary']['mistas']}
- Intensidade média: {exp['analise']['reacoes_summary']['intensidade_media']:.1f}/10
- Mudaram de opinião: {exp['analise']['reacoes_summary']['mudaram_opiniao']}

## Variação nas Respostas
"""
        
        for key, value in exp['analise'].items():
            if key.startswith("resp_"):
                report += f"\n### {key[5:]}\n"
                for opt, data in value.items():
                    report += f"- {opt}: {data['t0']}% → {data['t1']}% (Δ {data['delta']:+.1f}%)\n"
        
        return report
```

---

## 10. Validação Estatística

### 10.1 Métricas de Qualidade

```python
# analysis/validator.py
"""
Validação estatística dos resultados.
"""

import numpy as np
import pandas as pd
from scipy import stats
from typing import Dict, Any

class ResultValidator:
    """Valida qualidade estatística dos resultados."""
    
    @staticmethod
    def calculate_margin_of_error(n: int, p: float = 0.5, 
                                  confidence: float = 0.95) -> float:
        """
        Calcula margem de erro.
        
        Args:
            n: Tamanho da amostra
            p: Proporção estimada (0.5 para máxima variância)
            confidence: Nível de confiança
        """
        z = stats.norm.ppf((1 + confidence) / 2)
        return z * np.sqrt(p * (1 - p) / n)
    
    @staticmethod
    def compare_distributions(observed: pd.Series, 
                             expected: Dict[str, float]) -> Dict[str, Any]:
        """
        Compara distribuição observada com esperada usando qui-quadrado.
        """
        obs_counts = observed.value_counts()
        n = len(observed)
        
        # Alinhar categorias
        categories = list(set(obs_counts.index) | set(expected.keys()))
        obs_freq = [obs_counts.get(c, 0) for c in categories]
        exp_freq = [expected.get(c, 0) * n for c in categories]
        
        chi2, p_value = stats.chisquare(obs_freq, exp_freq)
        
        return {
            "chi2": chi2,
            "p_value": p_value,
            "is_representative": p_value > 0.05  # Não rejeita H0
        }
    
    @staticmethod
    def validate_sample_representativeness(agents: pd.DataFrame,
                                           expected_dist: Dict) -> Dict[str, Any]:
        """
        Valida se a amostra é representativa da população.
        """
        results = {}
        
        for variable, expected in expected_dist.items():
            if variable in agents.columns:
                observed = agents[variable]
                results[variable] = ResultValidator.compare_distributions(
                    observed, expected
                )
        
        return results
```

### 10.2 Comparação com Pesquisas Reais

```python
# analysis/benchmark.py
"""
Benchmarking contra pesquisas eleitorais reais.
"""

class PollBenchmark:
    """Compara resultados simulados com pesquisas reais."""
    
    def __init__(self):
        self.real_polls = {}
    
    def add_real_poll(self, name: str, data: Dict):
        """Adiciona pesquisa real para comparação."""
        self.real_polls[name] = data
    
    def compare(self, simulated: pd.DataFrame, 
                poll_name: str,
                question_column: str) -> Dict[str, Any]:
        """
        Compara resultados simulados com pesquisa real.
        """
        if poll_name not in self.real_polls:
            raise ValueError(f"Pesquisa '{poll_name}' não encontrada.")
        
        real = self.real_polls[poll_name]
        
        # Calcular distribuições
        sim_dist = simulated[question_column].value_counts(normalize=True)
        
        # Calcular diferença absoluta média
        all_options = set(sim_dist.index) | set(real.keys())
        differences = []
        
        comparison = {}
        for opt in all_options:
            sim_val = sim_dist.get(opt, 0) * 100
            real_val = real.get(opt, 0)
            diff = abs(sim_val - real_val)
            differences.append(diff)
            comparison[opt] = {
                "simulado": round(sim_val, 1),
                "real": real_val,
                "diferenca": round(diff, 1)
            }
        
        return {
            "comparacao_detalhada": comparison,
            "erro_medio_absoluto": np.mean(differences),
            "erro_maximo": max(differences),
            "correlacao": np.corrcoef(
                [sim_dist.get(k, 0) for k in all_options],
                [real.get(k, 0)/100 for k in all_options]
            )[0, 1]
        }
```

---

## 11. Código Prático

### 11.1 Exemplo Completo de Uso

```python
# main.py
"""
Exemplo completo de uso do sistema de simulação.
"""

import json
from pathlib import Path
from core.agent import ElectorAgent
from simulation.interviewer import Interviewer
from simulation.news_impact import NewsImpactAnalyzer
from analysis.aggregator import ResultAggregator

def main():
    # 1. Carregar ou criar agentes
    agents_dir = Path("data/agents/population_400")
    
    if agents_dir.exists():
        print("Carregando agentes existentes...")
        agents = []
        for f in agents_dir.glob("*.json"):
            agents.append(ElectorAgent.load(str(f)))
    else:
        print("Criando nova população de agentes...")
        from core.identity import ElectorGenerator
        generator = ElectorGenerator("data/demographics/config.json")
        profiles = generator.gerar_populacao(400)
        
        agents_dir.mkdir(parents=True, exist_ok=True)
        agents = []
        for profile in profiles:
            agent = ElectorAgent(**profile.__dict__)
            agent.save(str(agents_dir / f"agent_{agent.id}.json"))
            agents.append(agent)
    
    print(f"Total de agentes: {len(agents)}")
    
    # 2. Executar pesquisa de intenção de voto
    print("\n=== Pesquisa de Intenção de Voto ===")
    interviewer = Interviewer(agents)
    results = interviewer.quick_poll(
        "Se as eleições fossem hoje, em quem você votaria?",
        [
            "Candidato A (situação)",
            "Candidato B (oposição)", 
            "Candidato C (terceira via)",
            "Branco/Nulo",
            "Não sei"
        ]
    )
    
    # Mostrar resultados
    print("\nResultados:")
    col = [c for c in results.columns if c.startswith("resp_")][0]
    print(results[col].value_counts(normalize=True).mul(100).round(1))
    
    # 3. Testar impacto de notícia
    print("\n=== Teste de Impacto de Notícia ===")
    analyzer = NewsImpactAnalyzer(agents)
    
    noticia = """
    URGENTE: Candidato A é acusado de receber propina de R$ 2 milhões 
    de empresa de ônibus durante sua gestão. Documentos vazados mostram 
    transferências para contas de familiares. O candidato nega as acusações 
    e diz que é perseguição política.
    """
    
    experiment = analyzer.run_experiment(
        news=noticia,
        survey_path="data/surveys/intencao_voto.json",
        experiment_name="escandalo_candidato_a"
    )
    
    # Gerar relatório
    report = analyzer.generate_report("escandalo_candidato_a")
    print(report)
    
    # 4. Salvar resultados
    results.to_excel("outputs/pesquisa_intencao_voto.xlsx", index=False)
    
    with open("outputs/reports/impacto_escandalo.md", "w") as f:
        f.write(report)
    
    print("\nResultados salvos em outputs/")

if __name__ == "__main__":
    main()
```

### 11.2 CLAUDE.md para o Projeto

```markdown
# Simulador de Eleitores do DF

## Visão Geral

Sistema de simulação de 400 eleitores do Distrito Federal usando agentes generativos 
baseados em LLM (Claude/GPT). Permite testar mensagens de campanha, analisar impacto 
de notícias e simular pesquisas eleitorais.

## Comandos Frequentes

### Executar pesquisa rápida
```python
from simulation.interviewer import Interviewer
interviewer = Interviewer(agents)
results = interviewer.quick_poll("Pergunta?", ["Opção 1", "Opção 2", "Opção 3"])
```

### Injetar notícia
```python
from simulation.batch_processor import BatchProcessor
processor = BatchProcessor(agents)
reactions = processor.inject_news("Texto da notícia...")
```

### Carregar agentes
```python
from core.agent import ElectorAgent
agent = ElectorAgent.load("data/agents/population_400/agent_1.json")
```

## Estrutura de Arquivos

- `core/agent.py`: Classe principal ElectorAgent
- `core/identity.py`: Gerador de perfis demográficos
- `simulation/interviewer.py`: Sistema de entrevistas
- `simulation/batch_processor.py`: Processamento em lote
- `simulation/news_impact.py`: Análise de impacto de notícias
- `analysis/aggregator.py`: Agregação estatística
- `data/demographics/`: Dados do IBGE/TSE
- `data/agents/`: Agentes salvos
- `data/surveys/`: Questionários em JSON

## Convenções

- Sempre usar modelo Sonnet para tarefas regulares (economia)
- Usar Opus apenas para geração de histórias ricas
- Rate limit: 0.5s entre requisições
- Salvar agentes após modificações significativas

## Custos Estimados

- Criação de 400 agentes com histórias: ~$15-20
- Uma pesquisa completa (6 perguntas): ~$8-12
- Injeção de notícia + follow-up: ~$10-15
```

---

## 12. Custos e Otimização

### 12.1 Estimativa de Custos

```
┌─────────────────────────────────────────────────────────────────┐
│                    ESTIMATIVA DE CUSTOS                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  CRIAÇÃO INICIAL (uma vez)                                      │
│  ─────────────────────────                                      │
│                                                                 │
│  400 agentes × história rica (Sonnet)                           │
│  Tokens por agente: ~2.000 input + ~1.500 output               │
│  Total: 800.000 input + 600.000 output                          │
│  Custo: ~$2.40 + ~$9.00 = ~$11.40                              │
│                                                                 │
│  400 agentes × memórias iniciais (Sonnet)                       │
│  Tokens por agente: ~500 input + ~800 output                   │
│  Total: 200.000 input + 320.000 output                          │
│  Custo: ~$0.60 + ~$4.80 = ~$5.40                               │
│                                                                 │
│  TOTAL CRIAÇÃO: ~$17                                            │
│                                                                 │
│  ─────────────────────────────────────────────────────────────  │
│                                                                 │
│  PESQUISA (por execução)                                        │
│  ────────────────────────                                       │
│                                                                 │
│  400 agentes × 5 perguntas categóricas (Sonnet)                │
│  Tokens por resposta: ~800 input + ~150 output                 │
│  Total por pergunta: 320.000 input + 60.000 output             │
│  Total 5 perguntas: 1.600.000 input + 300.000 output           │
│  Custo: ~$4.80 + ~$4.50 = ~$9.30                               │
│                                                                 │
│  TOTAL POR PESQUISA: ~$10                                       │
│                                                                 │
│  ─────────────────────────────────────────────────────────────  │
│                                                                 │
│  ANÁLISE DE NOTÍCIA (por notícia)                               │
│  ────────────────────────────────                               │
│                                                                 │
│  Injeção: 400 × ~1.000 tokens = $3                             │
│  Pesquisa antes: $10                                            │
│  Pesquisa depois: $10                                           │
│                                                                 │
│  TOTAL POR ANÁLISE: ~$23                                        │
│                                                                 │
│  ─────────────────────────────────────────────────────────────  │
│                                                                 │
│  ORÇAMENTO MENSAL SUGERIDO                                      │
│  ─────────────────────────                                      │
│                                                                 │
│  • 4 pesquisas regulares: $40                                   │
│  • 2 análises de notícia: $46                                   │
│  • Margem/testes: $14                                           │
│                                                                 │
│  TOTAL: ~$100/mês (Plano Max 5x cobre)                         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 12.2 Estratégias de Otimização

```python
# Usar modelos diferentes por tarefa
COST_OPTIMIZED_MODELS = {
    "historia_rica": "claude-opus-4-5-20251101",      # Qualidade máxima
    "resposta_categorica": "claude-sonnet-4-5-20250929",  # Balanceado
    "resposta_simples": "claude-haiku-3-5-20241022",      # Economia
    "reflexao": "claude-sonnet-4-5-20250929"
}

# Batch de perguntas para reduzir overhead
def batch_questions(questions: List[str]) -> str:
    """Agrupa perguntas em uma única requisição."""
    return "\n\n".join([f"{i+1}. {q}" for i, q in enumerate(questions)])

# Cache de respostas similares
from functools import lru_cache

@lru_cache(maxsize=1000)
def get_cached_response(agent_profile_hash: str, question: str) -> str:
    """Cacheia respostas para evitar requisições duplicadas."""
    pass
```

---

## 13. Considerações Éticas

### 13.1 Limitações do Sistema

```
┌─────────────────────────────────────────────────────────────────┐
│                    LIMITAÇÕES IMPORTANTES                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ⚠️  AGENTES NÃO SÃO PESSOAS REAIS                              │
│      • Respostas são aproximações baseadas em estereótipos      │
│      • Podem perpetuar vieses presentes nos dados de treino     │
│      • Não capturam nuances individuais reais                   │
│                                                                 │
│  ⚠️  VALIDADE LIMITADA                                          │
│      • Útil para exploração e hipóteses                         │
│      • NÃO substitui pesquisas com pessoas reais                │
│      • Resultados devem ser validados empiricamente             │
│                                                                 │
│  ⚠️  RISCOS DE MAU USO                                          │
│      • Manipulação baseada em "vulnerabilidades" simuladas      │
│      • Reforço de estereótipos regionais/socioeconômicos        │
│      • Uso para desinformação direcionada                       │
│                                                                 │
│  ✅  BOAS PRÁTICAS                                               │
│      • Sempre validar com pesquisas reais antes de agir         │
│      • Usar para gerar hipóteses, não conclusões                │
│      • Documentar limitações em qualquer relatório              │
│      • Não expor dados individuais de agentes                   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 13.2 Uso Responsável

```markdown
## Checklist de Uso Ético

- [ ] Este uso gera benefício social ou apenas vantagem competitiva?
- [ ] Os resultados serão validados com dados reais?
- [ ] Estou perpetuando estereótipos com os perfis criados?
- [ ] O sistema está sendo usado para manipular ou para entender?
- [ ] Existe transparência sobre a natureza simulada dos dados?
```

---

## 14. Próximos Passos

### 14.1 Roadmap de Implementação

```
┌─────────────────────────────────────────────────────────────────┐
│                    ROADMAP DE IMPLEMENTAÇÃO                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  FASE 1: FUNDAÇÃO (Semana 1-2)                                  │
│  ─────────────────────────────                                  │
│  ☐ Configurar ambiente Python                                   │
│  ☐ Implementar classe ElectorAgent                              │
│  ☐ Criar gerador de perfis demográficos                         │
│  ☐ Gerar 50 agentes de teste                                    │
│  ☐ Testar respostas categóricas/numéricas                       │
│                                                                 │
│  FASE 2: POPULAÇÃO (Semana 3)                                   │
│  ───────────────────────────                                    │
│  ☐ Obter dados demográficos oficiais do DF                      │
│  ☐ Implementar estratificação completa                          │
│  ☐ Gerar 400 agentes com histórias ricas                        │
│  ☐ Validar representatividade da amostra                        │
│                                                                 │
│  FASE 3: SIMULAÇÃO (Semana 4-5)                                 │
│  ─────────────────────────────                                  │
│  ☐ Implementar sistema de entrevistas em lote                   │
│  ☐ Implementar injeção de notícias                              │
│  ☐ Implementar análise de impacto                               │
│  ☐ Criar questionários padrão                                   │
│                                                                 │
│  FASE 4: ANÁLISE (Semana 6)                                     │
│  ─────────────────────────                                      │
│  ☐ Implementar agregação estatística                            │
│  ☐ Criar visualizações (gráficos, mapas)                        │
│  ☐ Implementar geração de relatórios                            │
│  ☐ Comparar com pesquisas reais (benchmarking)                  │
│                                                                 │
│  FASE 5: INTERFACE (Semana 7-8)                                 │
│  ───────────────────────────                                    │
│  ☐ Criar CLI para uso rápido                                    │
│  ☐ Criar dashboard Streamlit (opcional)                         │
│  ☐ Documentar API do sistema                                    │
│  ☐ Escrever guia de uso                                         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 14.2 Comando Inicial no Claude Code

Quando você abrir o projeto no VS Code com Claude Code, comece com:

```
/init

Estou criando um sistema de simulação de eleitores do DF baseado na arquitetura 
de Generative Agents de Stanford. Quero criar 400 agentes representativos do 
eleitorado do DF para testar mensagens de campanha e analisar impacto de notícias.

Leia o CLAUDE.md deste projeto para entender a estrutura completa.

Primeira tarefa: Criar a classe ElectorAgent em core/agent.py com:
- Identidade completa (dados demográficos)
- Sistema de memória
- Métodos para respostas categóricas, numéricas e abertas
- Método para reagir a notícias
- Métodos de save/load

Use a arquitetura do GenAgents de Stanford como referência.
```

---

## Referências

### Papers Acadêmicos

1. **Park, J.S. et al. (2023)** - "Generative Agents: Interactive Simulacra of Human Behavior"
   - https://arxiv.org/abs/2304.03442
   - Arquitetura base: observação, reflexão, planejamento

2. **Park, J.S. et al. (2024)** - "Generative Agent Simulations of 1,000 People"
   - https://arxiv.org/abs/2411.10109
   - 85% de precisão vs respostas reais
   - Entrevistas de 2 horas para criar agentes

### Repositórios

1. **generative_agents** - https://github.com/joonspk-research/generative_agents
2. **genagents** - https://github.com/StanfordHCI/genagents

### Dados Demográficos

- **IBGE Cidades** - https://cidades.ibge.gov.br/brasil/df
- **TSE Estatísticas** - https://www.tse.jus.br/eleicoes/estatisticas
- **CODEPLAN** - http://www.codeplan.df.gov.br/

---

*Documento criado para uso com Claude Code. Última atualização: Janeiro 2026.*

# Trilha de Aprendizagem: Agentes Generativos para Simulação
## Do Zero ao Sistema de Entrevistas com Agentes Simulados

---

## Sobre Este Guia

Este documento é um **currículo de aprendizagem**. Ele não ensina a fazer o sistema - ensina **o que você precisa aprender** para conseguir fazer.

**Público-alvo:** Pessoa com conhecimento básico de computador, sem experiência em programação, que quer aprender a criar sistemas de agentes generativos usando Claude Code.

**Tempo estimado:** 6-10 semanas de estudo (2-3 horas por dia)

**Pré-requisitos:** Saber usar computador, ter Claude Max, VS Code instalado

---

## Mapa de Competências

```
┌─────────────────────────────────────────────────────────────────┐
│            COMPETÊNCIAS NECESSÁRIAS (em ordem)                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  NÍVEL 1: FUNDAMENTOS (Semanas 1-2)                            │
│  ──────────────────────────────────                            │
│  □ Lógica de programação básica                                │
│  □ Python: sintaxe fundamental                                  │
│  □ Estruturas de dados: listas, dicionários                    │
│  □ Funções e módulos                                           │
│  □ Leitura e escrita de arquivos                               │
│                                                                 │
│  NÍVEL 2: INTERMEDIÁRIO (Semanas 3-4)                          │
│  ─────────────────────────────────────                         │
│  □ Classes e Objetos (Programação Orientada a Objetos)         │
│  □ JSON: formato e manipulação                                 │
│  □ APIs: o que são e como consumir                             │
│  □ Bibliotecas externas e pip                                  │
│  □ Tratamento de erros                                         │
│                                                                 │
│  NÍVEL 3: ESPECÍFICO (Semanas 5-6)                             │
│  ──────────────────────────────────                            │
│  □ API da Anthropic (Claude)                                   │
│  □ Engenharia de prompts para agentes                          │
│  □ Padrões de design para agentes                              │
│  □ Gerenciamento de estado e memória                           │
│                                                                 │
│  NÍVEL 4: APLICADO (Semanas 7-8)                               │
│  ────────────────────────────────                              │
│  □ Arquitetura de sistemas multi-agente                        │
│  □ Processamento em lote                                       │
│  □ Análise de dados com Pandas                                 │
│  □ Persistência e banco de dados simples                       │
│                                                                 │
│  NÍVEL 5: DOMÍNIO (Semanas 9-10)                               │
│  ────────────────────────────────                              │
│  □ Validação estatística básica                                │
│  □ Visualização de dados                                       │
│  □ Otimização de custos de API                                 │
│  □ Integração de sistemas                                      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

# NÍVEL 1: FUNDAMENTOS DE PROGRAMAÇÃO

## Módulo 1.1: Lógica de Programação

### O Que É
Lógica de programação é a forma de pensar em passos sequenciais para resolver problemas. Antes de escrever código, você precisa saber **decompor problemas** em instruções simples.

### Por Que Você Precisa Disso
Para criar agentes, você vai precisar pensar:
- "Primeiro o agente lê sua identidade"
- "Depois recupera memórias relevantes"
- "Então formula uma resposta"
- "Por fim, salva a resposta na memória"

Sem lógica de programação, você não consegue estruturar esse fluxo.

### O Que Estudar

| Conceito | Descrição | Exemplo do Mundo Real |
|----------|-----------|----------------------|
| **Variáveis** | Caixas que guardam informações | Nome do eleitor, idade, opinião |
| **Condicionais** | Decisões (se/então/senão) | Se eleitor é jovem, perguntar sobre emprego |
| **Loops** | Repetição de ações | Para cada um dos 400 eleitores, fazer pergunta |
| **Sequência** | Ordem das operações | Primeiro carregar dados, depois processar |

### Exercícios Fundamentais

```
EXERCÍCIO 1: Descreva em passos como você faz café
  1. Pegar a chaleira
  2. Encher com água
  3. Colocar no fogo
  4. Esperar ferver
  5. ... (continue)

EXERCÍCIO 2: Descreva em passos como você decide em quem votar
  1. Identificar candidatos
  2. Para cada candidato:
     a. Ver propostas
     b. Verificar histórico
     c. Comparar com meus valores
  3. Escolher o mais alinhado

EXERCÍCIO 3: Descreva em passos como um robô faria uma pesquisa eleitoral
  1. Carregar lista de eleitores
  2. Para cada eleitor:
     a. Ler perfil do eleitor
     b. Fazer pergunta
     c. Registrar resposta
  3. Contar respostas
  4. Gerar relatório
```

### Recursos de Estudo

**Gratuitos:**
- Curso em Vídeo: Lógica de Programação (YouTube) - Gustavo Guanabara
- Codecademy: Intro to Programming (em inglês)

**Com Claude Code:**
```
Peça: "Me ensine lógica de programação do zero. 
       Comece explicando o que são variáveis 
       com exemplos práticos do dia a dia."
```

### Checkpoint de Aprendizagem
Você dominou este módulo quando conseguir:
- [ ] Descrever qualquer tarefa do dia a dia em passos lógicos
- [ ] Identificar onde há decisões (condicionais) em um processo
- [ ] Identificar onde há repetições (loops) em um processo
- [ ] Explicar o que é uma variável com suas próprias palavras

---

## Módulo 1.2: Python Básico - Sintaxe Fundamental

### O Que É
Python é a linguagem de programação mais usada para trabalhar com Inteligência Artificial. É conhecida por ser fácil de ler e escrever.

### Por Que Você Precisa Disso
- A API do Claude (Anthropic) tem biblioteca oficial em Python
- Os repositórios de Stanford que você quer replicar são em Python
- Python é a "língua franca" da IA

### O Que Estudar

#### 1. Variáveis e Tipos de Dados

```python
# O que você precisa saber:

# Texto (string)
nome = "Maria Silva"
regiao = "Ceilândia"

# Números inteiros
idade = 35
numero_filhos = 2

# Números decimais
renda = 2850.50

# Verdadeiro/Falso (booleano)
tem_emprego = True
votou_antes = False

# Verificar tipo
type(nome)      # <class 'str'>
type(idade)     # <class 'int'>
type(renda)     # <class 'float'>
type(tem_emprego)  # <class 'bool'>
```

**Por que isso importa para agentes:**
Cada eleitor simulado terá variáveis como nome, idade, região, opinião política. Você precisa saber armazenar e manipular esses dados.

#### 2. Operações Básicas

```python
# Matemática
soma = 10 + 5           # 15
media = (8 + 7 + 9) / 3 # 8.0
porcentagem = 45 / 100  # 0.45

# Texto
nome_completo = "Maria" + " " + "Silva"  # "Maria Silva"
grito = "atenção".upper()                 # "ATENÇÃO"
tamanho = len("Ceilândia")                # 9

# Comparações (retornam True ou False)
idade > 18              # True se maior de idade
renda <= 1500           # True se renda até 1500
regiao == "Plano Piloto"  # True se mora no Plano
```

#### 3. Condicionais (if/elif/else)

```python
# Estrutura básica
idade = 25

if idade < 18:
    print("Menor de idade - não vota")
elif idade < 70:
    print("Voto obrigatório")
else:
    print("Voto facultativo")

# Exemplo real para agentes:
orientacao = "esquerda"
proposta = "privatização"

if orientacao == "esquerda":
    if proposta == "privatização":
        reacao = "negativa"
    else:
        reacao = "analisar"
elif orientacao == "direita":
    if proposta == "privatização":
        reacao = "positiva"
    else:
        reacao = "analisar"
```

**Por que isso importa:**
Agentes tomam decisões baseadas em condições. "SE o eleitor é evangélico E a notícia é sobre aborto, ENTÃO a reação será intensa."

#### 4. Loops (for/while)

```python
# Loop FOR - quando você sabe quantas vezes repetir
eleitores = ["Maria", "João", "Ana", "Pedro"]

for eleitor in eleitores:
    print(f"Entrevistando {eleitor}...")

# Loop FOR com range - repetir N vezes
for i in range(5):
    print(f"Pergunta {i + 1}")

# Loop WHILE - enquanto condição for verdadeira
respostas_coletadas = 0
while respostas_coletadas < 400:
    # coletar resposta
    respostas_coletadas = respostas_coletadas + 1
```

**Por que isso importa:**
Você vai precisar processar 400 agentes. Loops permitem executar a mesma ação para cada um deles automaticamente.

#### 5. Print e Input

```python
# Mostrar informações
print("Olá, mundo!")
print(f"O eleitor {nome} tem {idade} anos")

# Receber informações (menos usado com agentes, mas útil para testes)
resposta = input("Digite sua opinião: ")
```

### Exercícios Práticos

```
EXERCÍCIO 1: Crie variáveis para um eleitor fictício
  - nome, idade, região, profissão, renda, religião

EXERCÍCIO 2: Escreva um IF que classifica o eleitor por faixa etária
  - Jovem (16-24), Adulto (25-59), Idoso (60+)

EXERCÍCIO 3: Escreva um FOR que imprime "Eleitor 1", "Eleitor 2"... até "Eleitor 10"

EXERCÍCIO 4: Combine tudo - crie 5 eleitores com idades diferentes
  e classifique cada um por faixa etária usando loop + condicional
```

### Recursos de Estudo

**Gratuitos:**
- Python.org Tutorial Oficial (em inglês)
- Curso em Vídeo: Python (YouTube) - 40 horas completo
- Real Python: Basics (artigos)

**Com Claude Code:**
```
Peça: "Estou aprendendo Python do zero. Me ensine sobre 
       [variáveis/condicionais/loops] com exercícios práticos.
       Corrija meus erros e explique o que fiz de errado."
```

### Checkpoint de Aprendizagem
- [ ] Criar variáveis de diferentes tipos (texto, número, booleano)
- [ ] Escrever condicionais if/elif/else sem erros de sintaxe
- [ ] Escrever loops for que percorrem listas
- [ ] Combinar condicionais dentro de loops
- [ ] Usar f-strings para formatar texto com variáveis

---

## Módulo 1.3: Estruturas de Dados - Listas e Dicionários

### O Que É
Estruturas de dados são formas de organizar múltiplos valores. As duas mais importantes em Python são **listas** (coleções ordenadas) e **dicionários** (pares chave-valor).

### Por Que Você Precisa Disso
- Lista de 400 eleitores
- Cada eleitor é um dicionário com nome, idade, região, memórias...
- Memórias são listas de eventos
- Respostas de pesquisa são dicionários

Praticamente TUDO em sistemas de agentes usa listas e dicionários.

### O Que Estudar

#### 1. Listas

```python
# Criar lista
eleitores = ["Maria", "João", "Ana"]
idades = [35, 42, 28]
preocupacoes = ["saúde", "segurança", "emprego", "educação"]

# Acessar elementos (índice começa em 0!)
primeiro = eleitores[0]    # "Maria"
ultimo = eleitores[-1]     # "Ana"

# Adicionar elementos
eleitores.append("Pedro")  # Adiciona no final
eleitores.insert(0, "Carlos")  # Adiciona na posição 0

# Remover elementos
eleitores.remove("João")   # Remove por valor
del eleitores[0]           # Remove por posição

# Tamanho da lista
quantidade = len(eleitores)  # Quantos elementos

# Verificar se existe
if "Maria" in eleitores:
    print("Maria está na lista")

# Percorrer lista
for eleitor in eleitores:
    print(eleitor)

# Percorrer com índice
for i, eleitor in enumerate(eleitores):
    print(f"{i+1}. {eleitor}")
```

**Exemplo real - Lista de memórias de um agente:**
```python
memorias = [
    "Vi notícia sobre aumento do gás em 15/01/2026",
    "Perdi emprego em dezembro de 2025",
    "Filho passou no vestibular",
    "Assaltado no ônibus mês passado"
]

# Adicionar nova memória
memorias.append("Governador visitou minha região hoje")

# Últimas 3 memórias
recentes = memorias[-3:]
```

#### 2. Dicionários

```python
# Criar dicionário
eleitor = {
    "nome": "Maria Silva",
    "idade": 35,
    "regiao": "Ceilândia",
    "profissao": "Professora",
    "renda": 3500.00,
    "tem_filhos": True,
    "preocupacoes": ["educação", "saúde", "segurança"]
}

# Acessar valores
nome = eleitor["nome"]           # "Maria Silva"
idade = eleitor["idade"]         # 35
primeira_preocupacao = eleitor["preocupacoes"][0]  # "educação"

# Acessar com get (não dá erro se não existir)
religiao = eleitor.get("religiao", "não informada")

# Adicionar/modificar
eleitor["religiao"] = "católica"
eleitor["idade"] = 36  # Aniversário!

# Verificar se chave existe
if "renda" in eleitor:
    print(f"Renda: R$ {eleitor['renda']}")

# Percorrer dicionário
for chave, valor in eleitor.items():
    print(f"{chave}: {valor}")

# Só as chaves
for chave in eleitor.keys():
    print(chave)

# Só os valores
for valor in eleitor.values():
    print(valor)
```

**Exemplo real - Perfil completo de um agente:**
```python
agente = {
    "id": 1,
    "identidade": {
        "nome": "José Carlos Oliveira",
        "idade": 52,
        "genero": "masculino",
        "regiao": "Taguatinga",
        "escolaridade": "médio completo",
        "profissao": "comerciante",
        "renda_sm": 4.5,
        "religiao": "evangélica",
        "orientacao_politica": "direita"
    },
    "memorias": [
        {"evento": "Abri minha loja em 2010", "importancia": 0.8},
        {"evento": "Fui assaltado em 2023", "importancia": 0.9},
        {"evento": "Meu filho se formou", "importancia": 0.7}
    ],
    "opiniao_atual": {
        "governo": "ruim",
        "candidato_preferido": "Candidato B"
    }
}

# Acessar dados aninhados
nome = agente["identidade"]["nome"]
ultima_memoria = agente["memorias"][-1]["evento"]
opiniao_governo = agente["opiniao_atual"]["governo"]
```

#### 3. Lista de Dicionários (o mais comum!)

```python
# Base de 400 eleitores seria assim:
eleitores = [
    {"id": 1, "nome": "Maria", "idade": 35, "regiao": "Ceilândia"},
    {"id": 2, "nome": "João", "idade": 42, "regiao": "Plano Piloto"},
    {"id": 3, "nome": "Ana", "idade": 28, "regiao": "Taguatinga"},
    # ... mais 397 eleitores
]

# Percorrer todos
for eleitor in eleitores:
    print(f"{eleitor['nome']} mora em {eleitor['regiao']}")

# Filtrar por condição
jovens = [e for e in eleitores if e["idade"] < 30]
ceilandia = [e for e in eleitores if e["regiao"] == "Ceilândia"]

# Contar por região
from collections import Counter
regioes = [e["regiao"] for e in eleitores]
contagem = Counter(regioes)
# {"Ceilândia": 66, "Plano Piloto": 30, ...}
```

### Exercícios Práticos

```
EXERCÍCIO 1: Crie uma lista com 5 regiões do DF

EXERCÍCIO 2: Crie um dicionário representando você como eleitor
  (nome, idade, região, profissão, 3 preocupações)

EXERCÍCIO 3: Crie uma lista de 3 eleitores (cada um é um dicionário)
  Percorra a lista e imprima "Nome tem X anos e mora em Região"

EXERCÍCIO 4: Adicione uma memória a cada eleitor do exercício 3
  Dica: cada eleitor precisa ter uma chave "memorias" com uma lista

EXERCÍCIO 5: Filtre os eleitores maiores de 30 anos em uma nova lista
```

### Checkpoint de Aprendizagem
- [ ] Criar, acessar e modificar listas
- [ ] Criar, acessar e modificar dicionários
- [ ] Aninhar estruturas (lista dentro de dicionário, dicionário dentro de lista)
- [ ] Percorrer lista de dicionários com for
- [ ] Filtrar lista de dicionários por condição

---

## Módulo 1.4: Funções

### O Que É
Funções são blocos de código reutilizáveis. Em vez de repetir o mesmo código várias vezes, você cria uma função e chama ela quando precisar.

### Por Que Você Precisa Disso
- `criar_eleitor()` - cria um novo agente
- `fazer_pergunta(eleitor, pergunta)` - faz pergunta para um agente
- `salvar_resposta(eleitor, resposta)` - salva resposta na memória
- `gerar_relatorio(respostas)` - gera relatório final

Sem funções, seu código seria uma bagunça impossível de manter.

### O Que Estudar

#### 1. Funções Básicas

```python
# Definir função
def saudacao():
    print("Olá! Bem-vindo à pesquisa eleitoral.")

# Chamar função
saudacao()

# Função com parâmetro
def saudar_eleitor(nome):
    print(f"Olá, {nome}! Obrigado por participar.")

saudar_eleitor("Maria")  # "Olá, Maria! Obrigado por participar."

# Função com retorno
def calcular_idade_em_2030(idade_atual):
    return idade_atual + (2030 - 2026)

idade_futura = calcular_idade_em_2030(35)  # 39
```

#### 2. Funções com Múltiplos Parâmetros

```python
def criar_eleitor(nome, idade, regiao):
    eleitor = {
        "nome": nome,
        "idade": idade,
        "regiao": regiao,
        "memorias": []
    }
    return eleitor

maria = criar_eleitor("Maria Silva", 35, "Ceilândia")
joao = criar_eleitor("João Santos", 42, "Plano Piloto")
```

#### 3. Parâmetros com Valor Padrão

```python
def criar_eleitor(nome, idade, regiao, religiao="não informada"):
    return {
        "nome": nome,
        "idade": idade,
        "regiao": regiao,
        "religiao": religiao
    }

# Pode chamar sem religião
maria = criar_eleitor("Maria", 35, "Ceilândia")

# Ou com religião
joao = criar_eleitor("João", 42, "Plano Piloto", "católica")
```

#### 4. Funções que Modificam Dados

```python
def adicionar_memoria(eleitor, memoria):
    """Adiciona uma memória ao eleitor."""
    eleitor["memorias"].append(memoria)

def atualizar_opiniao(eleitor, topico, opiniao):
    """Atualiza opinião do eleitor sobre um tópico."""
    if "opinioes" not in eleitor:
        eleitor["opinioes"] = {}
    eleitor["opinioes"][topico] = opiniao

# Uso
maria = criar_eleitor("Maria", 35, "Ceilândia")
adicionar_memoria(maria, "Perdi emprego em janeiro")
atualizar_opiniao(maria, "economia", "pessimista")
```

#### 5. Funções que Processam Listas

```python
def entrevistar_todos(eleitores, pergunta):
    """Faz uma pergunta para todos os eleitores."""
    respostas = []
    for eleitor in eleitores:
        # Aqui entraria a lógica de obter resposta
        resposta = {
            "eleitor": eleitor["nome"],
            "pergunta": pergunta,
            "resposta": "simulada"  # Por enquanto
        }
        respostas.append(resposta)
    return respostas

def filtrar_por_regiao(eleitores, regiao):
    """Retorna apenas eleitores de uma região específica."""
    return [e for e in eleitores if e["regiao"] == regiao]

def contar_por_faixa_etaria(eleitores):
    """Conta eleitores por faixa etária."""
    contagem = {"jovem": 0, "adulto": 0, "idoso": 0}
    for e in eleitores:
        if e["idade"] < 25:
            contagem["jovem"] += 1
        elif e["idade"] < 60:
            contagem["adulto"] += 1
        else:
            contagem["idoso"] += 1
    return contagem
```

### Boas Práticas

```python
# 1. Nomes descritivos
# Ruim:
def f(x):
    return x * 2

# Bom:
def dobrar_valor(numero):
    return numero * 2

# 2. Docstrings (documentação)
def calcular_margem_erro(n_amostras, confianca=0.95):
    """
    Calcula margem de erro para pesquisa eleitoral.
    
    Args:
        n_amostras: Número de eleitores na amostra
        confianca: Nível de confiança (padrão 95%)
    
    Returns:
        Margem de erro em porcentagem
    """
    # implementação aqui
    pass

# 3. Uma função = uma responsabilidade
# Ruim: função que faz tudo
def processar_eleitor(dados):
    # valida, salva, envia email, gera relatório...
    pass

# Bom: funções separadas
def validar_eleitor(dados):
    pass

def salvar_eleitor(eleitor):
    pass

def notificar_eleitor(eleitor):
    pass
```

### Exercícios Práticos

```
EXERCÍCIO 1: Crie função que recebe nome e idade, retorna dicionário de eleitor

EXERCÍCIO 2: Crie função que recebe eleitor e retorna sua faixa etária ("jovem"/"adulto"/"idoso")

EXERCÍCIO 3: Crie função que recebe lista de eleitores e região, 
             retorna apenas eleitores daquela região

EXERCÍCIO 4: Crie função que recebe lista de eleitores e retorna
             dicionário com contagem por região

EXERCÍCIO 5: Crie função que adiciona memória a um eleitor
             (recebe eleitor e texto da memória)
```

### Checkpoint de Aprendizagem
- [ ] Criar funções com e sem parâmetros
- [ ] Criar funções que retornam valores
- [ ] Usar parâmetros com valores padrão
- [ ] Escrever docstrings explicativas
- [ ] Criar funções que processam listas de dicionários

---

## Módulo 1.5: Arquivos - Leitura e Escrita

### O Que É
Ler e escrever arquivos permite que seu programa salve dados permanentemente e carregue dados que foram salvos antes.

### Por Que Você Precisa Disso
- Salvar os 400 eleitores criados (para não perder)
- Carregar eleitores salvos quando reiniciar o programa
- Salvar resultados de pesquisas
- Carregar questionários de arquivos

### O Que Estudar

#### 1. Arquivos de Texto Simples

```python
# Escrever em arquivo
with open("resultado.txt", "w", encoding="utf-8") as arquivo:
    arquivo.write("Resultado da pesquisa\n")
    arquivo.write("Candidato A: 45%\n")
    arquivo.write("Candidato B: 35%\n")

# Ler arquivo inteiro
with open("resultado.txt", "r", encoding="utf-8") as arquivo:
    conteudo = arquivo.read()
    print(conteudo)

# Ler linha por linha
with open("resultado.txt", "r", encoding="utf-8") as arquivo:
    for linha in arquivo:
        print(linha.strip())  # strip remove \n do final

# Adicionar ao arquivo (sem apagar)
with open("resultado.txt", "a", encoding="utf-8") as arquivo:
    arquivo.write("Indecisos: 20%\n")
```

#### 2. Arquivos JSON (o mais importante!)

JSON é o formato mais usado para salvar dados estruturados. Listas e dicionários Python viram JSON facilmente.

```python
import json

# Dicionário Python
eleitor = {
    "nome": "Maria Silva",
    "idade": 35,
    "regiao": "Ceilândia",
    "memorias": ["evento 1", "evento 2"]
}

# Salvar como JSON
with open("eleitor.json", "w", encoding="utf-8") as arquivo:
    json.dump(eleitor, arquivo, ensure_ascii=False, indent=2)

# O arquivo fica assim:
# {
#   "nome": "Maria Silva",
#   "idade": 35,
#   "regiao": "Ceilândia",
#   "memorias": ["evento 1", "evento 2"]
# }

# Carregar JSON
with open("eleitor.json", "r", encoding="utf-8") as arquivo:
    eleitor_carregado = json.load(arquivo)

print(eleitor_carregado["nome"])  # "Maria Silva"
```

#### 3. Salvar Lista de Eleitores

```python
import json

eleitores = [
    {"id": 1, "nome": "Maria", "idade": 35},
    {"id": 2, "nome": "João", "idade": 42},
    {"id": 3, "nome": "Ana", "idade": 28}
]

# Salvar todos
with open("eleitores.json", "w", encoding="utf-8") as arquivo:
    json.dump(eleitores, arquivo, ensure_ascii=False, indent=2)

# Carregar todos
with open("eleitores.json", "r", encoding="utf-8") as arquivo:
    eleitores = json.load(arquivo)

# Agora eleitores é uma lista de dicionários novamente
for e in eleitores:
    print(e["nome"])
```

#### 4. Funções de Salvar/Carregar Reutilizáveis

```python
import json
from pathlib import Path

def salvar_eleitores(eleitores, caminho):
    """Salva lista de eleitores em arquivo JSON."""
    with open(caminho, "w", encoding="utf-8") as f:
        json.dump(eleitores, f, ensure_ascii=False, indent=2)
    print(f"Salvos {len(eleitores)} eleitores em {caminho}")

def carregar_eleitores(caminho):
    """Carrega lista de eleitores de arquivo JSON."""
    with open(caminho, "r", encoding="utf-8") as f:
        eleitores = json.load(f)
    print(f"Carregados {len(eleitores)} eleitores de {caminho}")
    return eleitores

def arquivo_existe(caminho):
    """Verifica se arquivo existe."""
    return Path(caminho).exists()

# Uso
if arquivo_existe("eleitores.json"):
    eleitores = carregar_eleitores("eleitores.json")
else:
    eleitores = []  # Começa vazio
    print("Arquivo não encontrado. Iniciando lista vazia.")
```

#### 5. Organização em Pastas

```python
from pathlib import Path

# Criar pasta se não existir
pasta_dados = Path("dados/eleitores")
pasta_dados.mkdir(parents=True, exist_ok=True)

# Salvar cada eleitor em arquivo separado
for eleitor in eleitores:
    caminho = pasta_dados / f"eleitor_{eleitor['id']}.json"
    with open(caminho, "w", encoding="utf-8") as f:
        json.dump(eleitor, f, ensure_ascii=False, indent=2)

# Carregar todos os eleitores da pasta
eleitores = []
for arquivo in pasta_dados.glob("*.json"):
    with open(arquivo, "r", encoding="utf-8") as f:
        eleitor = json.load(f)
        eleitores.append(eleitor)
```

### Exercícios Práticos

```
EXERCÍCIO 1: Crie um dicionário de eleitor e salve em arquivo JSON

EXERCÍCIO 2: Carregue o eleitor do exercício 1 e imprima o nome

EXERCÍCIO 3: Crie lista com 3 eleitores, salve em JSON, 
             carregue de volta e imprima todos os nomes

EXERCÍCIO 4: Crie funções salvar_eleitor() e carregar_eleitor()

EXERCÍCIO 5: Crie uma pasta "meus_eleitores" e salve cada eleitor
             em um arquivo separado (eleitor_1.json, eleitor_2.json, etc)
```

### Checkpoint de Aprendizagem
- [ ] Ler e escrever arquivos de texto
- [ ] Salvar dicionários e listas como JSON
- [ ] Carregar dados de arquivos JSON
- [ ] Usar `with open()` corretamente
- [ ] Verificar se arquivo existe antes de tentar carregar
- [ ] Organizar arquivos em pastas

---

# NÍVEL 2: INTERMEDIÁRIO

## Módulo 2.1: Classes e Objetos

### O Que É
Programação Orientada a Objetos (POO) permite criar "moldes" (classes) para criar objetos com características e comportamentos próprios.

### Por Que Você Precisa Disso
Cada eleitor simulado é um **objeto** com:
- Atributos (nome, idade, memórias)
- Comportamentos (responder pergunta, reagir a notícia, refletir)

Classes permitem organizar tudo isso de forma elegante.

### O Que Estudar

#### 1. Conceito de Classe e Objeto

```python
# CLASSE = Molde/Receita
# OBJETO = Coisa criada a partir do molde

# Analogia: Classe é a forma de bolo, Objeto é o bolo

# Sem classe (como fazíamos antes):
eleitor1 = {"nome": "Maria", "idade": 35}
eleitor2 = {"nome": "João", "idade": 42}

# Com classe:
class Eleitor:
    pass  # Por enquanto vazia

maria = Eleitor()  # maria é um OBJETO da classe Eleitor
joao = Eleitor()   # joao é outro OBJETO
```

#### 2. Atributos (características)

```python
class Eleitor:
    def __init__(self, nome, idade, regiao):
        # __init__ é chamado automaticamente ao criar objeto
        # self se refere ao objeto sendo criado
        self.nome = nome
        self.idade = idade
        self.regiao = regiao
        self.memorias = []  # Lista vazia para cada eleitor

# Criar objetos
maria = Eleitor("Maria Silva", 35, "Ceilândia")
joao = Eleitor("João Santos", 42, "Plano Piloto")

# Acessar atributos
print(maria.nome)    # "Maria Silva"
print(joao.idade)    # 42
print(maria.regiao)  # "Ceilândia"
```

#### 3. Métodos (comportamentos)

```python
class Eleitor:
    def __init__(self, nome, idade, regiao):
        self.nome = nome
        self.idade = idade
        self.regiao = regiao
        self.memorias = []
    
    def adicionar_memoria(self, memoria):
        """Adiciona uma memória ao eleitor."""
        self.memorias.append(memoria)
    
    def faixa_etaria(self):
        """Retorna a faixa etária do eleitor."""
        if self.idade < 25:
            return "jovem"
        elif self.idade < 60:
            return "adulto"
        else:
            return "idoso"
    
    def apresentar(self):
        """Retorna apresentação do eleitor."""
        return f"Sou {self.nome}, {self.idade} anos, moro em {self.regiao}"

# Usar métodos
maria = Eleitor("Maria", 35, "Ceilândia")
maria.adicionar_memoria("Perdi emprego em janeiro")
maria.adicionar_memoria("Filho nasceu em março")

print(maria.faixa_etaria())  # "adulto"
print(maria.apresentar())    # "Sou Maria, 35 anos, moro em Ceilândia"
print(maria.memorias)        # ["Perdi emprego...", "Filho nasceu..."]
```

#### 4. Classe Completa de Eleitor

```python
class Eleitor:
    """Representa um eleitor simulado."""
    
    def __init__(self, id, nome, idade, genero, regiao, 
                 escolaridade, renda, religiao, orientacao_politica):
        # Identidade
        self.id = id
        self.nome = nome
        self.idade = idade
        self.genero = genero
        self.regiao = regiao
        self.escolaridade = escolaridade
        self.renda = renda
        self.religiao = religiao
        self.orientacao_politica = orientacao_politica
        
        # Estado interno
        self.memorias = []
        self.opinioes = {}
        self.humor = "neutro"
    
    def adicionar_memoria(self, texto, importancia=0.5):
        """Adiciona memória com nível de importância."""
        memoria = {
            "texto": texto,
            "importancia": importancia
        }
        self.memorias.append(memoria)
    
    def atualizar_opiniao(self, topico, opiniao):
        """Atualiza opinião sobre um tópico."""
        self.opinioes[topico] = opiniao
    
    def memorias_recentes(self, n=5):
        """Retorna as N memórias mais recentes."""
        return self.memorias[-n:]
    
    def para_dicionario(self):
        """Converte para dicionário (útil para salvar em JSON)."""
        return {
            "id": self.id,
            "nome": self.nome,
            "idade": self.idade,
            "genero": self.genero,
            "regiao": self.regiao,
            "escolaridade": self.escolaridade,
            "renda": self.renda,
            "religiao": self.religiao,
            "orientacao_politica": self.orientacao_politica,
            "memorias": self.memorias,
            "opinioes": self.opinioes
        }
    
    @classmethod
    def de_dicionario(cls, dados):
        """Cria eleitor a partir de dicionário (útil para carregar de JSON)."""
        eleitor = cls(
            id=dados["id"],
            nome=dados["nome"],
            idade=dados["idade"],
            genero=dados["genero"],
            regiao=dados["regiao"],
            escolaridade=dados["escolaridade"],
            renda=dados["renda"],
            religiao=dados["religiao"],
            orientacao_politica=dados["orientacao_politica"]
        )
        eleitor.memorias = dados.get("memorias", [])
        eleitor.opinioes = dados.get("opinioes", {})
        return eleitor
    
    def __str__(self):
        """Representação em texto do eleitor."""
        return f"Eleitor({self.nome}, {self.idade} anos, {self.regiao})"
```

#### 5. Usando a Classe

```python
# Criar eleitor
maria = Eleitor(
    id=1,
    nome="Maria Silva",
    idade=35,
    genero="feminino",
    regiao="Ceilândia",
    escolaridade="superior",
    renda=3500,
    religiao="católica",
    orientacao_politica="centro-esquerda"
)

# Usar métodos
maria.adicionar_memoria("Perdi emprego", importancia=0.8)
maria.adicionar_memoria("Filho passou no ENEM", importancia=0.7)
maria.atualizar_opiniao("economia", "pessimista")
maria.atualizar_opiniao("educação", "preocupada")

# Salvar em JSON
import json
with open("maria.json", "w", encoding="utf-8") as f:
    json.dump(maria.para_dicionario(), f, ensure_ascii=False, indent=2)

# Carregar de JSON
with open("maria.json", "r", encoding="utf-8") as f:
    dados = json.load(f)
maria_carregada = Eleitor.de_dicionario(dados)

print(maria_carregada.nome)  # "Maria Silva"
```

### Por Que Classe é Melhor que Dicionário Puro

```
DICIONÁRIO:
- Não tem validação (pode colocar qualquer coisa)
- Não tem comportamentos (só dados)
- Fácil esquecer chaves necessárias
- Difícil manter código organizado

CLASSE:
- Valida na criação (__init__ define o que precisa)
- Tem comportamentos (métodos)
- IDE ajuda com autocomplete (maria. mostra opções)
- Código organizado e reutilizável
```

### Exercícios Práticos

```
EXERCÍCIO 1: Crie classe Eleitor simples com nome, idade, regiao

EXERCÍCIO 2: Adicione método faixa_etaria() que retorna "jovem"/"adulto"/"idoso"

EXERCÍCIO 3: Adicione lista de memórias e método adicionar_memoria()

EXERCÍCIO 4: Adicione métodos para_dicionario() e de_dicionario()

EXERCÍCIO 5: Crie 3 eleitores, salve em JSON, carregue de volta
```

### Checkpoint de Aprendizagem
- [ ] Entender diferença entre classe e objeto
- [ ] Criar classe com `__init__` e atributos
- [ ] Criar métodos que usam e modificam atributos
- [ ] Usar `self` corretamente
- [ ] Converter objeto para dicionário e vice-versa
- [ ] Entender quando usar classe vs dicionário

---

## Módulo 2.2: APIs - O Que São e Como Usar

### O Que É
API (Interface de Programação de Aplicações) é uma forma de programas conversarem entre si. Quando seu código Python "conversa" com o Claude, ele usa a API da Anthropic.

### Por Que Você Precisa Disso
**Isso é FUNDAMENTAL.** Seu sistema de agentes vai usar a API do Claude para:
- Gerar respostas dos eleitores
- Criar histórias de vida
- Simular reflexões
- Reagir a notícias

Sem entender APIs, você não consegue criar agentes.

### O Que Estudar

#### 1. Conceito de API

```
SUA APLICAÇÃO                    SERVIÇO EXTERNO
(seu código Python)              (servidores do Claude)
                                 
     ┌─────────┐                 ┌─────────────────┐
     │ Código  │ ──── REQUEST ──▶│                 │
     │ Python  │                 │  API Anthropic  │
     │         │ ◀── RESPONSE ───│                 │
     └─────────┘                 └─────────────────┘
     
REQUEST (pedido):
- "Olá Claude, finja ser um eleitor chamado João..."

RESPONSE (resposta):
- "Como João, eu diria que a segurança é minha maior preocupação..."
```

#### 2. Biblioteca requests (APIs genéricas)

```python
import requests

# Exemplo: API pública de CEP
cep = "70040-010"
url = f"https://viacep.com.br/ws/{cep}/json/"

resposta = requests.get(url)

if resposta.status_code == 200:  # 200 = sucesso
    dados = resposta.json()
    print(dados["logradouro"])  # Nome da rua
    print(dados["bairro"])      # Bairro
else:
    print(f"Erro: {resposta.status_code}")
```

#### 3. API da Anthropic (Claude)

```python
# Instalar: pip install anthropic

import anthropic

# Criar cliente (conexão com a API)
client = anthropic.Anthropic(
    api_key="sua-chave-aqui"  # Obter em console.anthropic.com
)

# Fazer uma pergunta
resposta = client.messages.create(
    model="claude-sonnet-4-5-20250929",
    max_tokens=500,
    messages=[
        {"role": "user", "content": "Qual a capital do Brasil?"}
    ]
)

# Extrair texto da resposta
texto = resposta.content[0].text
print(texto)  # "A capital do Brasil é Brasília..."
```

#### 4. Estrutura de uma Requisição para Claude

```python
resposta = client.messages.create(
    # Qual modelo usar
    model="claude-sonnet-4-5-20250929",  # ou opus, haiku
    
    # Limite de tokens na resposta
    max_tokens=1000,
    
    # Mensagens da conversa
    messages=[
        # Pode ter várias mensagens (conversa)
        {"role": "user", "content": "Primeira pergunta"},
        {"role": "assistant", "content": "Primeira resposta"},
        {"role": "user", "content": "Segunda pergunta"}
    ],
    
    # Opcional: instruções do sistema
    system="Você é um assistente prestativo que responde em português."
)
```

#### 5. System Prompt (Instruções do Sistema)

O system prompt define o "papel" que o Claude vai assumir:

```python
# Para simular um eleitor:
system_prompt = """
Você é João Silva, um eleitor de 45 anos que mora em Ceilândia, DF.

Perfil:
- Profissão: Comerciante
- Renda: 4 salários mínimos
- Religião: Evangélico
- Escolaridade: Ensino médio completo
- Estado civil: Casado, 2 filhos
- Principais preocupações: Segurança, economia

Responda sempre como João responderia, mantendo consistência
com seu perfil, valores e forma de falar.
"""

resposta = client.messages.create(
    model="claude-sonnet-4-5-20250929",
    max_tokens=300,
    system=system_prompt,
    messages=[
        {"role": "user", "content": "Em quem você pretende votar para governador?"}
    ]
)

print(resposta.content[0].text)
# "Olha, eu ainda tô pensando... Segurança é o que mais me preocupa..."
```

#### 6. Conversa com Múltiplas Mensagens

```python
# Simular entrevista com eleitor
system = "Você é Maria, eleitora de 35 anos de Taguatinga..."

mensagens = [
    {"role": "user", "content": "Qual sua opinião sobre o transporte público?"}
]

# Primeira pergunta
resp1 = client.messages.create(
    model="claude-sonnet-4-5-20250929",
    max_tokens=300,
    system=system,
    messages=mensagens
)

resposta_maria = resp1.content[0].text
print(f"Maria: {resposta_maria}")

# Adicionar resposta e fazer pergunta de acompanhamento
mensagens.append({"role": "assistant", "content": resposta_maria})
mensagens.append({"role": "user", "content": "E a saúde pública, como você avalia?"})

# Segunda pergunta
resp2 = client.messages.create(
    model="claude-sonnet-4-5-20250929",
    max_tokens=300,
    system=system,
    messages=mensagens
)

print(f"Maria: {resp2.content[0].text}")
```

#### 7. Tratamento de Erros

```python
import anthropic
from anthropic import APIError, RateLimitError

try:
    resposta = client.messages.create(
        model="claude-sonnet-4-5-20250929",
        max_tokens=300,
        messages=[{"role": "user", "content": "Olá!"}]
    )
    print(resposta.content[0].text)

except RateLimitError:
    print("Muitas requisições! Aguarde um momento...")
    
except APIError as e:
    print(f"Erro da API: {e}")
    
except Exception as e:
    print(f"Erro inesperado: {e}")
```

### Conceitos Importantes

```
MODELO: Qual versão do Claude usar
  - claude-opus-4-5-20251101 (mais inteligente, mais caro)
  - claude-sonnet-4-5-20250929 (balanceado)
  - claude-haiku-3-5-20241022 (mais rápido, mais barato)

TOKENS: Unidades de texto (≈ 4 caracteres ou ¾ de palavra)
  - max_tokens limita tamanho da resposta
  - Você paga por tokens de entrada + saída

MENSAGENS: Histórico da conversa
  - role: "user" (você) ou "assistant" (Claude)
  - content: texto da mensagem

SYSTEM: Instruções que definem comportamento
  - Define persona, regras, contexto
  - Não aparece na conversa, mas influencia respostas
```

### Exercícios Práticos

```
EXERCÍCIO 1: Faça uma pergunta simples ao Claude via API
             e imprima a resposta

EXERCÍCIO 2: Use system prompt para fazer Claude responder
             sempre em português formal

EXERCÍCIO 3: Crie system prompt de um eleitor fictício
             e faça 3 perguntas em sequência (conversa)

EXERCÍCIO 4: Adicione tratamento de erros ao código

EXERCÍCIO 5: Crie função perguntar_eleitor(system, pergunta)
             que encapsula a chamada à API
```

### Checkpoint de Aprendizagem
- [ ] Entender o conceito de API (request/response)
- [ ] Instalar e usar biblioteca anthropic
- [ ] Fazer chamadas básicas ao Claude
- [ ] Usar system prompt para definir persona
- [ ] Manter conversa com múltiplas mensagens
- [ ] Tratar erros de API

---

## Módulo 2.3: Engenharia de Prompts para Agentes

### O Que É
Engenharia de prompts é a arte de escrever instruções claras para o modelo de linguagem. Para agentes, isso significa criar prompts que fazem o Claude "ser" consistentemente um personagem específico.

### Por Que Você Precisa Disso
A qualidade das respostas dos seus agentes depende 90% da qualidade dos prompts. Um prompt ruim gera respostas genéricas. Um prompt bom gera respostas realistas e consistentes.

### O Que Estudar

#### 1. Estrutura de um Prompt de Agente

```
PROMPT DE AGENTE = IDENTIDADE + CONTEXTO + MEMÓRIAS + INSTRUÇÃO

┌─────────────────────────────────────────────────────────────────┐
│                      SYSTEM PROMPT                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  IDENTIDADE                                                     │
│  Você é [NOME], um(a) [descrição demográfica].                 │
│                                                                 │
│  DADOS PESSOAIS                                                 │
│  - Idade: X anos                                               │
│  - Mora em: [local]                                            │
│  - Profissão: [profissão]                                      │
│  - ... outros dados                                            │
│                                                                 │
│  HISTÓRIA DE VIDA                                               │
│  [narrativa pessoal de 2-3 parágrafos]                         │
│                                                                 │
│  MEMÓRIAS RECENTES                                              │
│  - [evento 1]                                                  │
│  - [evento 2]                                                  │
│  - [evento 3]                                                  │
│                                                                 │
│  INSTRUÇÕES                                                     │
│  Responda SEMPRE como [NOME] responderia...                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### 2. Prompt Ruim vs Prompt Bom

```python
# ❌ PROMPT RUIM
prompt_ruim = "Finja ser um eleitor do DF e responda perguntas"

# Problemas:
# - Muito vago
# - Sem identidade definida
# - Sem contexto de vida
# - Respostas serão genéricas

# ✅ PROMPT BOM
prompt_bom = """
Você é José Carlos Ferreira, um eleitor de 52 anos do Distrito Federal.

DADOS PESSOAIS:
- Idade: 52 anos
- Gênero: Masculino
- Mora em: Taguatinga Norte, DF
- Escolaridade: Ensino médio completo
- Profissão: Dono de uma pequena loja de materiais de construção
- Renda familiar: Cerca de R$ 6.000/mês
- Estado civil: Casado há 28 anos com Dona Marlene
- Filhos: 2 filhos adultos (Pedro, 26, e Carla, 23)
- Religião: Evangélico (Igreja Batista), frequenta culto aos domingos

HISTÓRIA DE VIDA:
José Carlos nasceu em Ceilândia, filho de migrantes nordestinos que vieram 
para Brasília na construção da cidade. Trabalhou como pedreiro na juventude,
economizou durante 15 anos e abriu sua loja de materiais em 2005. 
Já passou por duas crises econômicas que quase fecharam seu negócio.
É uma pessoa trabalhadora, acorda às 5h da manhã, valoriza a família 
e a fé acima de tudo. Desconfia de políticos, mas vota sempre.

OPINIÕES POLÍTICAS:
- Votou em Bolsonaro em 2018 e 2022
- Se decepcionou com alguns aspectos do governo, mas ainda se identifica com a direita
- Considera segurança e economia suas prioridades
- É contra aborto e drogas por convicção religiosa
- Acha que "tem muito vagabundo que não quer trabalhar"
- Defende que "o governo tem que deixar o povo trabalhar"

MEMÓRIAS RECENTES:
- Mês passado sua loja foi assaltada pela terceira vez em 2 anos
- Seu filho Pedro está desempregado há 8 meses
- Viu notícia sobre aumento do diesel afetando preço dos materiais
- Pastor da igreja comentou sobre candidatos nas eleições

FORMA DE FALAR:
- Usa linguagem simples e direta
- Às vezes usa expressões como "rapaz", "olha só", "te falo"
- Não gosta de enrolação, vai direto ao ponto
- Quando fala de política fica mais exaltado
- Usa exemplos da própria vida para ilustrar opiniões

INSTRUÇÕES:
Responda SEMPRE como José Carlos responderia. Mantenha total consistência
com seu perfil, história, valores e forma de se expressar. Não quebre 
o personagem em nenhum momento. Use a primeira pessoa.
"""

# Agora as respostas serão realistas e consistentes!
```

#### 3. Técnicas de Prompt para Agentes

**Técnica 1: Forçar Formato de Resposta**
```python
prompt = """
[identidade do eleitor]

Responda à pergunta em JSON com o seguinte formato:
{
    "opcao_escolhida": "texto da opção",
    "justificativa": "explicação de 2-3 frases",
    "nivel_certeza": "alto/medio/baixo"
}

Pergunta: Em quem você votaria para governador?
Opções: 
1. Candidato A
2. Candidato B
3. Nenhum/Branco
4. Ainda não decidi
"""
```

**Técnica 2: Memórias Relevantes**
```python
prompt = """
[identidade do eleitor]

MEMÓRIAS RELEVANTES PARA ESTA PERGUNTA:
(recuperadas automaticamente do banco de memórias)
- Há 2 meses: "Vi reportagem sobre escândalo de corrupção do Candidato A"
- Há 1 mês: "Candidato B visitou meu bairro e prometeu mais policiamento"
- Semana passada: "Meu vizinho disse que Candidato B é 'mais do mesmo'"

Com base em quem você é e nas suas experiências, responda:
Em quem você votaria hoje?
"""
```

**Técnica 3: Reação a Notícia**
```python
prompt = """
[identidade do eleitor]

Você acabou de ver a seguinte notícia no seu celular:

"URGENTE: Candidato A é flagrado recebendo dinheiro de empreiteira.
Vídeo mostra maços de dinheiro sendo entregues em escritório.
Candidato nega e diz que vídeo é montagem."

Reaja a essa notícia como {nome} reagiria:
1. Qual sua reação emocional imediata?
2. Você acredita ou desconfia da notícia? Por quê?
3. Isso muda sua intenção de voto? Como?
4. O que você comentaria com sua família sobre isso?

Responda em primeira pessoa, mantendo seu jeito de falar.
"""
```

**Técnica 4: Escala com Justificativa**
```python
prompt = """
[identidade do eleitor]

De 0 a 10, avalie a gestão atual do governo do DF.

Considere:
- Sua experiência pessoal com serviços públicos
- Situação do seu bairro
- Impacto na sua vida e da sua família

Responda no formato:
NOTA: [número]
JUSTIFICATIVA: [explicação de 3-4 frases baseada na sua vida]
"""
```

#### 4. Erros Comuns e Como Evitar

```
❌ ERRO 1: Prompt genérico demais
   "Seja um eleitor e responda"
   
✅ SOLUÇÃO: Dar identidade completa e específica


❌ ERRO 2: Não dar contexto de vida
   "Maria, 35 anos, mora em Ceilândia"
   
✅ SOLUÇÃO: Incluir história, experiências, memórias


❌ ERRO 3: Não definir forma de falar
   Resultado: todos os agentes falam igual, formal demais
   
✅ SOLUÇÃO: Descrever linguagem, expressões típicas, nível de formalidade


❌ ERRO 4: Não ancorar em experiências
   "O que você acha da economia?"
   
✅ SOLUÇÃO: "Considerando sua loja e o preço dos materiais..."


❌ ERRO 5: Permitir que "quebre" o personagem
   Agente responde "Como IA, não tenho opinião..."
   
✅ SOLUÇÃO: Instruir explicitamente para nunca quebrar personagem
```

### Exercícios Práticos

```
EXERCÍCIO 1: Escreva prompt de identidade para um eleitor jovem (20 anos)
             de Águas Claras, classe média, estudante universitário

EXERCÍCIO 2: Escreva prompt para eleitor idoso (68 anos) de Ceilândia,
             aposentado, ex-metalúrgico, 6 filhos

EXERCÍCIO 3: Adicione "forma de falar" aos dois prompts anteriores

EXERCÍCIO 4: Crie prompt que força resposta em JSON com opção + justificativa

EXERCÍCIO 5: Crie prompt de reação a notícia negativa sobre um candidato
```

### Checkpoint de Aprendizagem
- [ ] Criar prompt de identidade completo (dados + história + opiniões)
- [ ] Incluir memórias relevantes no prompt
- [ ] Definir forma de falar do personagem
- [ ] Forçar formato de resposta (JSON, escala, etc)
- [ ] Evitar respostas genéricas
- [ ] Testar consistência do personagem com múltiplas perguntas

---

# NÍVEL 3: ESPECÍFICO PARA AGENTES

## Módulo 3.1: Arquitetura de Agentes Generativos

### O Que É
A arquitetura de agentes generativos é o "projeto" de como um agente funciona. Define como ele armazena informações, processa perguntas e gera respostas consistentes.

### Por Que Você Precisa Disso
Sem arquitetura, você teria apenas um "chatbot com persona". Com arquitetura, você tem um agente que:
- Lembra do passado
- Evolui com novas informações
- Mantém consistência ao longo do tempo
- Reflete sobre experiências

### O Que Estudar

#### 1. Componentes de um Agente (Stanford)

```
┌─────────────────────────────────────────────────────────────────┐
│                   ARQUITETURA DE AGENTE                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌───────────────────────────────────────────────────────────┐ │
│  │                    1. IDENTIDADE (Scratch)                 │ │
│  │  Dados fixos: nome, idade, região, valores, história      │ │
│  │  → Não muda (ou muda raramente)                           │ │
│  └───────────────────────────────────────────────────────────┘ │
│                              │                                  │
│                              ▼                                  │
│  ┌───────────────────────────────────────────────────────────┐ │
│  │                    2. MEMÓRIA (Memory Stream)              │ │
│  │  Eventos, experiências, observações                        │ │
│  │  → Cresce com o tempo, tem peso de importância            │ │
│  └───────────────────────────────────────────────────────────┘ │
│                              │                                  │
│                              ▼                                  │
│  ┌───────────────────────────────────────────────────────────┐ │
│  │                    3. REFLEXÃO (Reflection)                │ │
│  │  Síntese de memórias em insights de alto nível            │ │
│  │  → Gerado periodicamente a partir das memórias            │ │
│  └───────────────────────────────────────────────────────────┘ │
│                              │                                  │
│                              ▼                                  │
│  ┌───────────────────────────────────────────────────────────┐ │
│  │                    4. RECUPERAÇÃO (Retrieval)              │ │
│  │  Busca memórias relevantes para uma pergunta              │ │
│  │  → Usa recência, importância e relevância                 │ │
│  └───────────────────────────────────────────────────────────┘ │
│                              │                                  │
│                              ▼                                  │
│  ┌───────────────────────────────────────────────────────────┐ │
│  │                    5. RESPOSTA (Response)                  │ │
│  │  Gera resposta baseada em identidade + memórias           │ │
│  │  → Usa LLM com contexto completo                          │ │
│  └───────────────────────────────────────────────────────────┘ │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### 2. Identidade (Scratch)

```python
class Identidade:
    """Dados fixos do agente que definem quem ele é."""
    
    def __init__(self):
        # Dados demográficos
        self.nome = ""
        self.idade = 0
        self.genero = ""
        self.regiao = ""
        self.escolaridade = ""
        self.profissao = ""
        self.renda = 0
        self.religiao = ""
        self.estado_civil = ""
        
        # Traços de personalidade
        self.tracos_inatos = []  # Ex: ["introvertido", "cauteloso"]
        self.valores = []        # Ex: ["família", "trabalho", "fé"]
        
        # Narrativa
        self.historia_vida = ""
        self.opinioes_politicas = ""
        self.forma_de_falar = ""
```

#### 3. Memória (Memory Stream)

```python
from datetime import datetime

class Memoria:
    """Uma única memória do agente."""
    
    def __init__(self, conteudo, tipo="observacao", importancia=0.5):
        self.id = None  # Definido ao adicionar
        self.conteudo = conteudo
        self.tipo = tipo  # "observacao", "pensamento", "reflexao"
        self.importancia = importancia  # 0.0 a 1.0
        self.timestamp = datetime.now()
        self.acessos = 0  # Quantas vezes foi recuperada

class BancoDeMemoria:
    """Gerencia todas as memórias do agente."""
    
    def __init__(self):
        self.memorias = []
        self.proximo_id = 1
    
    def adicionar(self, conteudo, tipo="observacao", importancia=0.5):
        """Adiciona nova memória."""
        memoria = Memoria(conteudo, tipo, importancia)
        memoria.id = self.proximo_id
        self.proximo_id += 1
        self.memorias.append(memoria)
        return memoria
    
    def recuperar_recentes(self, n=10):
        """Retorna as N memórias mais recentes."""
        ordenadas = sorted(self.memorias, 
                          key=lambda m: m.timestamp, 
                          reverse=True)
        return ordenadas[:n]
    
    def recuperar_importantes(self, n=10):
        """Retorna as N memórias mais importantes."""
        ordenadas = sorted(self.memorias,
                          key=lambda m: m.importancia,
                          reverse=True)
        return ordenadas[:n]
    
    def recuperar_por_relevancia(self, query, n=5):
        """
        Retorna memórias relevantes para uma query.
        Versão simplificada: busca por palavras-chave.
        Versão avançada: usaria embeddings e similaridade.
        """
        palavras_query = set(query.lower().split())
        
        scores = []
        for mem in self.memorias:
            palavras_mem = set(mem.conteudo.lower().split())
            overlap = len(palavras_query & palavras_mem)
            # Score combina relevância, importância e recência
            score = (overlap * 0.5 + 
                    mem.importancia * 0.3 + 
                    (1 / (datetime.now() - mem.timestamp).days + 1) * 0.2)
            scores.append((mem, score))
        
        scores.sort(key=lambda x: x[1], reverse=True)
        return [mem for mem, score in scores[:n]]
```

#### 4. Reflexão (Reflection)

```python
def gerar_reflexao(agente, ancora, client):
    """
    Gera reflexão de alto nível sobre um tema.
    
    Reflexões são sínteses de múltiplas memórias em insights.
    Ex: Várias memórias sobre problemas financeiros →
        Reflexão: "Minha situação econômica está cada vez mais difícil"
    """
    
    # 1. Recuperar memórias relevantes
    memorias_relevantes = agente.memoria.recuperar_por_relevancia(ancora, n=10)
    
    # 2. Formatar memórias para o prompt
    memorias_texto = "\n".join([
        f"- {m.conteudo} (importância: {m.importancia})"
        for m in memorias_relevantes
    ])
    
    # 3. Pedir para o LLM gerar reflexão
    prompt = f"""
    Você é {agente.identidade.nome}.
    
    Suas memórias relacionadas a "{ancora}":
    {memorias_texto}
    
    Com base nessas experiências, gere UMA reflexão pessoal
    (2-3 frases) que sintetiza o que você aprendeu ou sente
    sobre este tema. Use primeira pessoa.
    """
    
    resposta = client.messages.create(
        model="claude-sonnet-4-5-20250929",
        max_tokens=200,
        messages=[{"role": "user", "content": prompt}]
    )
    
    reflexao = resposta.content[0].text
    
    # 4. Salvar reflexão como nova memória de alta importância
    agente.memoria.adicionar(
        conteudo=f"Reflexão sobre {ancora}: {reflexao}",
        tipo="reflexao",
        importancia=0.8
    )
    
    return reflexao
```

#### 5. Fluxo Completo de Resposta

```python
def responder_pergunta(agente, pergunta, client):
    """
    Fluxo completo para gerar resposta de um agente.
    """
    
    # 1. Recuperar memórias relevantes para a pergunta
    memorias = agente.memoria.recuperar_por_relevancia(pergunta, n=5)
    memorias_texto = "\n".join([f"- {m.conteudo}" for m in memorias])
    
    # 2. Montar prompt completo
    prompt = f"""
    Você é {agente.identidade.nome}, {agente.identidade.idade} anos,
    mora em {agente.identidade.regiao}.
    
    SOBRE VOCÊ:
    {agente.identidade.historia_vida}
    
    SUAS OPINIÕES POLÍTICAS:
    {agente.identidade.opinioes_politicas}
    
    MEMÓRIAS RELEVANTES:
    {memorias_texto}
    
    FORMA DE FALAR:
    {agente.identidade.forma_de_falar}
    
    ---
    
    PERGUNTA: {pergunta}
    
    Responda como {agente.identidade.nome} responderia,
    mantendo total consistência com quem você é.
    """
    
    # 3. Gerar resposta
    resposta = client.messages.create(
        model="claude-sonnet-4-5-20250929",
        max_tokens=400,
        messages=[{"role": "user", "content": prompt}]
    )
    
    texto_resposta = resposta.content[0].text
    
    # 4. Registrar na memória
    agente.memoria.adicionar(
        conteudo=f"Respondi sobre '{pergunta[:50]}...'",
        tipo="observacao",
        importancia=0.4
    )
    
    return texto_resposta
```

### Exercícios Práticos

```
EXERCÍCIO 1: Implemente classe Identidade com todos os campos necessários

EXERCÍCIO 2: Implemente classe Memoria e BancoDeMemoria

EXERCÍCIO 3: Crie função que adiciona memória e retorna as 5 mais recentes

EXERCÍCIO 4: Implemente recuperação por palavras-chave

EXERCÍCIO 5: Crie fluxo completo: identidade + memória + resposta via API
```

### Checkpoint de Aprendizagem
- [ ] Entender os 5 componentes de um agente (identidade, memória, reflexão, recuperação, resposta)
- [ ] Implementar sistema básico de memória
- [ ] Implementar recuperação de memórias relevantes
- [ ] Integrar memórias no prompt de resposta
- [ ] Gerar reflexões a partir de memórias

---

## Módulo 3.2: Processamento em Lote

### O Que É
Processamento em lote é executar a mesma operação em muitos itens de uma vez. Para agentes, significa fazer a mesma pergunta para todos os 400 eleitores de forma eficiente.

### Por Que Você Precisa Disso
- Pesquisa com 400 agentes = 400 chamadas à API
- Sem otimização, pode demorar horas e custar muito
- Precisa lidar com erros sem perder progresso
- Precisa respeitar limites de taxa da API

### O Que Estudar

#### 1. Loop Simples com Progresso

```python
from tqdm import tqdm  # pip install tqdm
import time

def entrevistar_todos(eleitores, pergunta, client):
    """Faz pergunta para todos os eleitores com barra de progresso."""
    
    respostas = []
    
    # tqdm mostra barra de progresso
    for eleitor in tqdm(eleitores, desc="Entrevistando"):
        try:
            resposta = responder_pergunta(eleitor, pergunta, client)
            respostas.append({
                "eleitor_id": eleitor.id,
                "nome": eleitor.identidade.nome,
                "resposta": resposta
            })
        except Exception as e:
            respostas.append({
                "eleitor_id": eleitor.id,
                "nome": eleitor.identidade.nome,
                "erro": str(e)
            })
        
        # Respeitar limite de taxa
        time.sleep(0.5)  # 0.5 segundo entre requisições
    
    return respostas
```

#### 2. Salvamento Incremental

```python
import json
from pathlib import Path

def entrevistar_com_salvamento(eleitores, pergunta, client, arquivo_saida):
    """Salva progresso a cada resposta para não perder se der erro."""
    
    # Carregar progresso existente
    if Path(arquivo_saida).exists():
        with open(arquivo_saida, "r") as f:
            respostas = json.load(f)
        ids_processados = {r["eleitor_id"] for r in respostas}
    else:
        respostas = []
        ids_processados = set()
    
    # Processar apenas os que faltam
    eleitores_faltando = [e for e in eleitores if e.id not in ids_processados]
    print(f"Já processados: {len(ids_processados)}")
    print(f"Faltam: {len(eleitores_faltando)}")
    
    for eleitor in tqdm(eleitores_faltando, desc="Entrevistando"):
        try:
            resposta = responder_pergunta(eleitor, pergunta, client)
            respostas.append({
                "eleitor_id": eleitor.id,
                "nome": eleitor.identidade.nome,
                "resposta": resposta
            })
        except Exception as e:
            respostas.append({
                "eleitor_id": eleitor.id,
                "erro": str(e)
            })
        
        # Salvar após cada resposta
        with open(arquivo_saida, "w", encoding="utf-8") as f:
            json.dump(respostas, f, ensure_ascii=False, indent=2)
        
        time.sleep(0.5)
    
    return respostas
```

#### 3. Retry com Exponential Backoff

```python
import time
import random

def chamar_api_com_retry(func, max_tentativas=3):
    """
    Tenta chamar função várias vezes com espera crescente.
    Útil quando API está sobrecarregada.
    """
    
    for tentativa in range(max_tentativas):
        try:
            return func()
        except Exception as e:
            if tentativa == max_tentativas - 1:
                raise e  # Última tentativa, propagar erro
            
            # Espera crescente: 1s, 2s, 4s... + aleatoriedade
            espera = (2 ** tentativa) + random.uniform(0, 1)
            print(f"Erro: {e}. Tentando novamente em {espera:.1f}s...")
            time.sleep(espera)

# Uso
def fazer_pergunta():
    return client.messages.create(...)

resposta = chamar_api_com_retry(fazer_pergunta)
```

#### 4. Processamento Paralelo (Avançado)

```python
from concurrent.futures import ThreadPoolExecutor, as_completed
import threading

# Lock para escrita segura no arquivo
lock = threading.Lock()

def processar_eleitor(eleitor, pergunta, client):
    """Processa um único eleitor."""
    try:
        resposta = responder_pergunta(eleitor, pergunta, client)
        return {"eleitor_id": eleitor.id, "resposta": resposta, "erro": None}
    except Exception as e:
        return {"eleitor_id": eleitor.id, "resposta": None, "erro": str(e)}

def entrevistar_paralelo(eleitores, pergunta, client, max_workers=5):
    """
    Processa múltiplos eleitores em paralelo.
    CUIDADO: Respeitar limites de taxa da API!
    """
    
    respostas = []
    
    with ThreadPoolExecutor(max_workers=max_workers) as executor:
        # Submeter todas as tarefas
        futures = {
            executor.submit(processar_eleitor, e, pergunta, client): e
            for e in eleitores
        }
        
        # Coletar resultados conforme ficam prontos
        for future in tqdm(as_completed(futures), total=len(eleitores)):
            resultado = future.result()
            respostas.append(resultado)
            time.sleep(0.2)  # Rate limiting entre resultados
    
    return respostas
```

### Exercícios Práticos

```
EXERCÍCIO 1: Crie loop que processa lista de eleitores com barra de progresso

EXERCÍCIO 2: Adicione salvamento incremental em arquivo JSON

EXERCÍCIO 3: Implemente retry com exponential backoff

EXERCÍCIO 4: Crie função que retoma processamento de onde parou

EXERCÍCIO 5: (Avançado) Implemente processamento paralelo básico
```

### Checkpoint de Aprendizagem
- [ ] Usar tqdm para mostrar progresso
- [ ] Salvar resultados incrementalmente
- [ ] Implementar retry para erros de API
- [ ] Retomar processamento de onde parou
- [ ] Respeitar limites de taxa (rate limiting)

---

# NÍVEL 4: APLICADO

## Módulo 4.1: Pandas para Análise de Dados

### O Que É
Pandas é a biblioteca Python para análise de dados. Permite trabalhar com tabelas (DataFrames) de forma poderosa.

### Por Que Você Precisa Disso
- Analisar respostas de 400 eleitores
- Filtrar por região, idade, renda
- Calcular porcentagens e estatísticas
- Exportar para Excel

### O Que Estudar (Resumo)

```python
import pandas as pd

# Criar DataFrame de respostas
respostas = pd.DataFrame([
    {"nome": "Maria", "regiao": "Ceilândia", "voto": "Candidato A", "idade": 35},
    {"nome": "João", "regiao": "Plano Piloto", "voto": "Candidato B", "idade": 42},
    # ... mais 398 linhas
])

# Contar votos
contagem = respostas["voto"].value_counts()
porcentagem = respostas["voto"].value_counts(normalize=True) * 100

# Filtrar por região
ceilandia = respostas[respostas["regiao"] == "Ceilândia"]

# Agrupar por região
por_regiao = respostas.groupby("regiao")["voto"].value_counts()

# Pivot table
tabela = pd.pivot_table(respostas, 
                        values="nome", 
                        index="regiao", 
                        columns="voto", 
                        aggfunc="count")

# Exportar para Excel
respostas.to_excel("resultados.xlsx", index=False)
```

### O Que Focar

1. Criar DataFrame de lista de dicionários
2. Filtrar linhas por condição
3. Agrupar e contar (groupby + value_counts)
4. Calcular porcentagens
5. Exportar para Excel/CSV

---

## Módulo 4.2: Visualização com Matplotlib/Plotly

### O Que É
Bibliotecas para criar gráficos a partir dos dados.

### Por Que Você Precisa Disso
- Gráficos de pizza (intenção de voto)
- Gráficos de barras (por região)
- Comparativos antes/depois de notícia

### O Que Estudar (Resumo)

```python
import matplotlib.pyplot as plt

# Gráfico de pizza
votos = {"Candidato A": 45, "Candidato B": 35, "Indecisos": 20}
plt.pie(votos.values(), labels=votos.keys(), autopct='%1.1f%%')
plt.title("Intenção de Voto")
plt.savefig("grafico_votos.png")
plt.show()

# Gráfico de barras
plt.bar(votos.keys(), votos.values())
plt.title("Intenção de Voto")
plt.ylabel("Porcentagem")
plt.savefig("barras_votos.png")
plt.show()
```

---

# RESUMO: Ordem de Estudo

```
┌─────────────────────────────────────────────────────────────────┐
│                    ORDEM RECOMENDADA DE ESTUDO                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  SEMANA 1-2: FUNDAMENTOS                                        │
│  ☐ Lógica de programação (2-3 dias)                            │
│  ☐ Python básico: variáveis, condicionais, loops (3-4 dias)    │
│  ☐ Listas e dicionários (2-3 dias)                             │
│  ☐ Funções (2 dias)                                            │
│  ☐ Arquivos JSON (1-2 dias)                                    │
│                                                                 │
│  SEMANA 3-4: INTERMEDIÁRIO                                      │
│  ☐ Classes e objetos (3-4 dias)                                │
│  ☐ API da Anthropic (2-3 dias)                                 │
│  ☐ Engenharia de prompts (3-4 dias)                            │
│  ☐ Tratamento de erros (1-2 dias)                              │
│                                                                 │
│  SEMANA 5-6: ESPECÍFICO                                         │
│  ☐ Arquitetura de agentes (4-5 dias)                           │
│  ☐ Sistema de memória (2-3 dias)                               │
│  ☐ Processamento em lote (2-3 dias)                            │
│  ☐ Integrar tudo em classe Agente (3-4 dias)                   │
│                                                                 │
│  SEMANA 7-8: APLICADO                                           │
│  ☐ Pandas básico (2-3 dias)                                    │
│  ☐ Visualização básica (2 dias)                                │
│  ☐ Projeto piloto: 10 agentes (4-5 dias)                       │
│  ☐ Escalar para 400 agentes (2-3 dias)                         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

# RECURSOS DE ESTUDO

## Para Cada Módulo

| Módulo | Recurso Gratuito | Com Claude Code |
|--------|------------------|-----------------|
| Lógica | Curso em Vídeo (YouTube) | "Me ensine lógica de programação" |
| Python Básico | Python.org Tutorial | "Me ensine Python do zero" |
| Listas/Dicts | Real Python (artigos) | "Exercícios de listas Python" |
| Classes | Corey Schafer (YouTube) | "Me ensine POO em Python" |
| APIs | Documentação Anthropic | "Como usar a API do Claude" |
| Prompts | Documentação Anthropic | "Me ajude a criar prompt de agente" |
| Pandas | Pandas Documentation | "Analise estes dados com Pandas" |

## Estratégia com Claude Code

```
PARA CADA CONCEITO:

1. Peça explicação:
   "Explique [conceito] para iniciante com exemplos práticos"

2. Peça exercícios:
   "Me dê 5 exercícios de [conceito] do fácil ao difícil"

3. Tente fazer sozinho

4. Peça correção:
   "Corrija meu código e explique o que errei: [código]"

5. Peça projeto prático:
   "Me dê um mini-projeto que use [conceito] no contexto de agentes"
```

---

# COMO USAR ESTE GUIA

1. **Siga a ordem** - Cada módulo depende dos anteriores
2. **Faça os exercícios** - Ler não é suficiente, tem que praticar
3. **Use Claude Code** - Peça ajuda, tire dúvidas, peça mais exercícios
4. **Marque os checkpoints** - Só avance quando dominar cada módulo
5. **Construa projetos pequenos** - Aplique cada conceito em mini-projetos
6. **Seja paciente** - 6-10 semanas é realista para quem está começando

---

*Este guia é o currículo para a Trilha de Agentes do seu aplicativo educacional.*
*Cada módulo pode virar uma aula/seção do app.*

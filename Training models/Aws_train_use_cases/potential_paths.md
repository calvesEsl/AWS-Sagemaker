# Escolhendo um recurso no Amazon SageMaker Training

Nesta etapa, estamos entendendo **como escolher a melhor forma de treinar modelos no SageMaker**, de acordo com o nosso cenário de uso.

O SageMaker apresenta **3 casos de uso principais** para treinamento de modelos de Machine Learning, e para cada caso ele recomenda um conjunto de recursos/ferramentas.

A ideia é simples:

- se eu quero **rapidez e simplicidade**, uso uma abordagem mais visual/low-code;
- se eu quero **mais controle técnico**, uso SDK + algoritmos prontos/modelos prontos;
- se eu preciso de **máxima flexibilidade e escala**, uso scripts próprios ou contêineres customizados.

---

## Visão geral dos 3 casos de uso

### Use case 1
**Desenvolver um modelo em ambiente low-code ou no-code.**

Esse cenário é voltado para quem quer começar rápido, testar hipóteses e criar modelos sem precisar programar muito.

---

### Use case 2
**Usar código para desenvolver modelos com mais flexibilidade e controle.**

Esse é um cenário intermediário (e muito comum em estudos e projetos reais), onde eu já quero:
- configurar melhor o treinamento,
- controlar hiperparâmetros,
- escolher algoritmos/modelos,
- e usar o SageMaker de forma mais técnica, mas ainda com produtividade.

---

### Use case 3
**Desenvolver modelos em escala com máxima flexibilidade e controle.**

Aqui o foco é produção/escala:
- infraestrutura mais avançada,
- múltiplas instâncias,
- treinamento distribuído,
- código e ambiente totalmente customizados.

---

# Recursos recomendados por caso de uso (Recommended features)

A tabela de “Recommended features” mostra, para cada caso de uso:

- qual recurso do SageMaker é recomendado;
- a descrição da abordagem;
- para que ela é otimizada;
- e pontos de atenção (considerations).

---

## Use case 1 — Amazon SageMaker Canvas

### Recurso recomendado
**Build a model using Amazon SageMaker Canvas**

### O que isso significa
O **SageMaker Canvas** é a opção visual / low-code / no-code do SageMaker para criação de modelos.

Você leva seus dados e o SageMaker ajuda com:
- construção do modelo,
- configuração do treinamento,
- e parte da infraestrutura necessária.

### Descrição prática
Essa opção é ideal quando o objetivo é:
- testar rápido,
- aprender o fluxo de ML,
- gerar um primeiro modelo,
- sem entrar em muito detalhe técnico.

### Otimizado para
- desenvolvimento guiado por interface (UI)
- baixa ou nenhuma codificação
- experimentação rápida com dataset de treino

### Observação importante
Embora seja muito bom para começar, ele oferece **menos flexibilidade** para customizações avançadas.

---

## Use case 2 — Built-in algorithms / JumpStart + SageMaker Python SDK

### Recurso recomendado
Treinar um modelo usando:
- **SageMaker built-in ML algorithms** (ex.: XGBoost)
- ou **Task-Specific models via SageMaker JumpStart**
- com o **SageMaker Python SDK**

### O que isso significa (cenário do print)
Nesse caso, eu continuo usando os recursos do SageMaker para facilitar o treinamento, mas já passo a trabalhar com **código** e **configuração mais detalhada**.

Eu posso:
- levar meus dados,
- escolher um algoritmo pronto do SageMaker (como XGBoost),
- ou usar um modelo pré-configurado pelo JumpStart,
- configurar hiperparâmetros,
- definir métricas de saída,
- ajustar parâmetros básicos de infraestrutura,
- e iniciar o treinamento usando o **SageMaker Python SDK**.

### Papel do SageMaker Python SDK aqui
O SDK funciona como uma camada prática para interagir com o SageMaker via Python, permitindo:
- configurar jobs de treino,
- apontar dados no S3,
- escolher algoritmo/imagem de treino,
- definir instâncias,
- iniciar e monitorar o job.

Ou seja: você tem **mais controle que no Canvas**, mas sem precisar montar tudo do zero.

### Built-in algorithms (o que são)
São **algoritmos pré-empacotados** e otimizados pelo SageMaker para tarefas comuns de ML.

Exemplos clássicos:
- **XGBoost** (muito usado para classificação/regressão em dados tabulares)
- outros algoritmos prontos dependendo do tipo de tarefa

Esses algoritmos já vêm preparados para rodar no ecossistema do SageMaker, o que reduz esforço de setup.

### JumpStart (neste contexto)
O **SageMaker JumpStart** oferece modelos e soluções prontas para acelerar o início do projeto.

No caso do print, ele aparece como opção para usar:
- **Task-Specific models**
- com suporte do **Python SDK**

Isso ajuda quando você quer começar com algo mais estruturado sem sair do fluxo de treino do SageMaker.

### Otimizado para
Esse cenário é otimizado para:
- treinamento com **customização de hiperparâmetros** em nível alto,
- ajustes de infraestrutura,
- uso de frameworks e scripts de entrada com maior flexibilidade,
- uso de algoritmos built-in, modelos pré-treinados e modelos do JumpStart.

### Quando faz sentido usar (na prática)
Esse é um ótimo meio-termo para:
- quem já programa em Python
- quer aprender o SageMaker “de verdade”
- mas ainda quer produtividade
- sem ir direto para contêiner customizado

### Considerações
- exige mais conhecimento técnico do que Canvas;
- você já precisa entender melhor dados, treino e algumas configurações;
- porém ainda é uma abordagem bem produtiva para estudo e projetos reais.

---

## Use case 3 — Script mode / Custom containers

### Recurso recomendado
Treinar em escala com máxima flexibilidade usando:
- **script mode**
- ou **custom containers** no SageMaker

### O que isso significa
Nesse cenário, você desenvolve seu próprio código de ML e leva para o SageMaker como:
- script de treino (script mode)
- ou contêiner Docker customizado (custom container)

Isso permite:
- controlar dependências,
- controlar ambiente de execução,
- usar arquitetura própria,
- e configurar workloads em escala.

### Descrição prática
A plataforma SageMaker continua ajudando no provisionamento da infraestrutura, mas agora a responsabilidade do usuário sobre a solução aumenta bastante.

É a opção mais poderosa — e também a mais avançada.

### Otimizado para
- workloads de treinamento em escala
- múltiplas instâncias
- máxima flexibilidade
- treinamento distribuído
- cenários de produção mais complexos

### Considerações
Esse cenário exige mais conhecimento em:
- AWS
- infraestrutura
- treinamento distribuído
- Docker/containers
- configuração de jobs de forma mais avançada

---

# Comparação prática (resumo rápido)

## Caso 1 — Canvas
- **Perfil:** iniciante / negócio / analista
- **Foco:** rapidez
- **Código:** pouco ou nenhum
- **Flexibilidade:** baixa/média

## Caso 2 — Built-in + JumpStart + SDK
- **Perfil:** dev / cientista de dados em evolução
- **Foco:** equilíbrio entre produtividade e controle
- **Código:** sim (Python SDK)
- **Flexibilidade:** média/alta

## Caso 3 — Script mode / Custom container
- **Perfil:** avançado / produção / MLOps
- **Foco:** escala e customização máxima
- **Código:** total
- **Flexibilidade:** muito alta

---

# Como escolher (regra simples)

Uma forma prática de decidir:

- **Quero aprender rápido / prototipar** → **Canvas**
- **Quero treinar com mais controle usando Python** → **Built-in algorithms / JumpStart + Python SDK**
- **Quero produção em escala e ambiente customizado** → **Script mode / Custom containers**

---

# Observação importante sobre estudos

Para estudos (como este repositório), o **Use case 2** costuma ser excelente porque:
- já ensina o uso do **SageMaker Python SDK**,
- permite treinar modelos de forma mais realista,
- e ainda não exige toda a complexidade de contêiner customizado.

Isso ajuda a criar uma base sólida antes de avançar para cenários de produção em escala.

---

# Conceitos citados nesta etapa

## Built-in Algorithms
Algoritmos prontos fornecidos pelo SageMaker, otimizados para tarefas de ML.

#

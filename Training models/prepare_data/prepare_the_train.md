# Preparando o treino do modelo no SageMaker Studio (JupyterLab)

Aqui iremos preparar o treino do nosso modelo utilizando o **JupyterLab no SageMaker Studio**.  
Para isso, tenha em mãos um **Space** rodando no JupyterLab.

O dataset utilizado será o **Employee.csv**, disponível em:

* `Training models/datasets/Employee.csv`

Nele, temos registros de funcionários de uma empresa.

Gostaríamos de prever se esse funcionário **de fato deixou a empresa** ou **ainda está na empresa**.  
É muito importante para a empresa saber se um funcionário deixaria a empresa ou não, e em que nível essa possibilidade se encontra (probabilidade de saída).

---

## Teste para quem estiver lendo

Consegue me dizer qual tipo de aprendizado supervisionado iremos aplicar nesse caso de uso?

### Resposta
Utilizaremos **classificação binária**, pois temos duas saídas possíveis:

* funcionário saiu
* funcionário não saiu

Usaremos o **XGBoost**, portanto utilizaremos um **Built-in Algorithm** do SageMaker.

### O que é XGBoost?
O **XGBoost (eXtreme Gradient Boosting)** é um algoritmo muito utilizado em problemas de:

* **classificação**
* **regressão**

Ele é baseado em **árvores de decisão** e utiliza a técnica de **boosting**, em que várias árvores são criadas em sequência, e cada nova árvore tenta corrigir os erros da anterior.

Ele é muito usado porque:

* tem ótimo desempenho em dados tabulares
* costuma treinar rápido
* possui boa capacidade preditiva
* permite ajuste de hiperparâmetros

### O que são Built-in Algorithms?
São algoritmos prontos e otimizados fornecidos pelo SageMaker para tarefas comuns de Machine Learning, como:

* classificação
* regressão
* clustering
* detecção de anomalias

Eles facilitam o uso porque já vêm integrados ao ecossistema do SageMaker.

---

## 01 - Upload do dataset e do notebook no JupyterLab

No nosso espaço do JupyterLab, irei fazer o upload:

* do dataset de funcionários
* e do notebook utilizado para estudo: `Training models/notebook/SageMaker_Employee_Attrition_Demo.ipynb`

Esse notebook será usado como base para seguir o fluxo de preparação e treino do modelo.

![alt text](/Training%20models/images/prepare_data/training-00.png)

---

## 02 - Upload dos dados de treinamento para um bucket S3

Também iremos fazer o upload dos nossos dados de treinamento em um bucket S3.  
Como já vimos esse processo em passos anteriores, irei pular a demonstração detalhada.

Basicamente:

* criamos uma pasta `input-data` no nosso bucket
* adicionamos nosso dataset dentro dela (`Employee.csv`)

Esse passo é importante porque o SageMaker normalmente utiliza o **Amazon S3** como origem dos dados de treino.

![alt text](/Training%20models/images/prepare_data/training-01.png)
---

## 03 - SETUP

Agora voltamos para o nosso notebook de estudo, onde temos as importações das seguintes bibliotecas:

` ` `python
import sagemaker
from sagemaker import get_execution_role
import boto3
import pandas as pd
` ` `

**O que cada uma faz?**

* **sagemaker:** SDK do SageMaker para Python. Usamos para interagir com recursos do SageMaker, como treinamento, estimadores, Feature Store e jobs.
* **get_execution_role:** Função que recupera o IAM Role de execução do ambiente (Studio/Notebook), usado para permitir acesso a serviços AWS (como S3 e SageMaker).
* **boto3:** SDK da AWS para Python. Permite criar clientes e chamar APIs da AWS diretamente (por exemplo: S3, SageMaker, Feature Store Runtime).
* **pandas (pd):** Biblioteca para manipulação de dados tabulares (DataFrame). Usamos para carregar, transformar e preparar os dados.

**Ajuste importante no bucket**

Lembre-se de ajustar o nome do seu bucket no trecho onde existe o comentário:

S3 bucket for storing data
bucket = 'nome-do-seu-bucket'

Substitua pelo nome do bucket que você criou. Depois disso, podemos rodar a primeira célula.

![alt text](/Training%20models/images/prepare_data/training-02.png)

---

## 04 - Data preparation

Aqui iremos preparar nossos dados para um problema de classificação.

Como estamos usando XGBoost, precisamos tratar alguns pontos antes do treino:

* O XGBoost não trabalha diretamente com dados categóricos em texto, então precisamos convertê-los em dados numéricos (encoding).
* Garantir que não teremos valores nulos nas colunas importantes.
* Ajustar o formato esperado pelo algoritmo.

Além disso, moveremos a coluna `LeaveOrNot`, pois o algoritmo espera que a coluna alvo (label) seja a primeira coluna no formato CSV de treino usado com XGBoost no SageMaker.

**Por que isso é importante?**
A etapa de preparação de dados impacta diretamente o resultado do modelo. Mesmo um bom algoritmo pode ter desempenho ruim se os dados estiverem mal preparados.

Podemos rodar essa célula.

![alt text](/Training%20models/images/prepare_data/training-03.png)


---

## 05 - Create a Feature Group

Também queremos estudar rapidamente como podemos usar o Feature Store, que é uma boa prática no pipeline de treinamento.

**O que é o Feature Store?**
O Amazon SageMaker Feature Store é um repositório para armazenar, versionar e reutilizar features (atributos/variáveis) usadas em treino e inferência.

**Por que ele é útil?**
* Reutilização de features entre projetos.
* Consistência entre treino e produção.
* Armazenamento histórico (offline).
* Consulta rápida para inferência em tempo real (online).

Como já vimos em uma seção desse repositório (`Feature Store/create_with_notebook`), lembre-se de configurar permissão de acesso ao bucket para o role que você está utilizando, como visto no passo 04 do arquivo:

`Ground Truth/labeling_jobs/create_labeling_jobs.md`

Podemos rodar essa célula e a célula "Check the status of the Feature Group" para checarmos o status do nosso grupo.

![alt text](/Training%20models/images/prepare_data/training-04.png)


> **Observação:** a criação do Feature Group pode levar alguns instantes (é assíncrona). O ideal é aguardar o status ficar como `Created` antes de seguir para ingestão/consulta.

---

## 06 - Initialize the SageMaker Feature Store runtime client

Aqui temos a demonstração de que também podemos recuperar os dados que armazenamos no Feature Store para utilizar em nosso treinamento.

Para isso, usamos a API `GetRecord` do SageMaker Feature Store Runtime.

**O que é a API GetRecord?**
A operação `GetRecord` busca um registro no Feature Store com base em:

* nome do Feature Group
* identificador do registro (record identifier)
* lista de features desejadas (opcional)

Esse passo demonstra como consultar dados armazenados no Feature Store antes de seguir com outras etapas do pipeline.

**Conceito importante: Online Store x Offline Store**

* **Online Store:** Usado para leitura rápida (baixa latência), geralmente em inferência em tempo real.
* **Offline Store:** Usado para histórico e análise em lote, geralmente em treinamento, analytics e consultas via S3/Athena/Glue.

Neste passo, estamos usando a consulta como demonstração de recuperação dos dados.

![alt text](/Training%20models/images/prepare_data/training-05.png)


---

## Conclusão desta etapa

Com os dados preparados, o ambiente configurado e a demonstração de uso do Feature Store, estamos prontos para treinar nosso modelo.
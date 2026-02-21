# Treinando o modelo no SageMaker Studio com XGBoost

Nesta etapa, entraremos de fato no **treinamento do modelo**, separando os dados em conjuntos de **treinamento** e **validação** e executando o treino do algoritmo com **XGBoost**.

O objetivo principal aqui é **entender o fluxo do pipeline de treinamento**, e não necessariamente detalhar cada linha do notebook neste momento.  
Por isso, a recomendação é:

* **debugar/analisar o código**, como foi feito nas etapas anteriores;
* entender o que cada bloco está fazendo;
* evitar apenas executar as células sem interpretação.

---

## 01 - Train the Model Using Local Data with S3 Mode (Default)

Nesta etapa, iniciamos o treino do modelo utilizando os dados armazenados no **Amazon S3**. O notebook irá gerar **dois arquivos**:
* um arquivo para **treinamento**
* um arquivo para **validação**

Após executar a célula, esses arquivos também ficarão disponíveis no seu bucket S3, dentro da pasta `input-data` (criada na etapa de preparação dos dados).

Podemos rodar essa célula.

![alt text](/Training%20models/images/train/train_model-00.png)
![alt text](/Training%20models/images/train/train_model-01.png)

---

## 02 - Configuração do treinamento (hiperparâmetros, imagem e paths)

Na última célula desta seção é onde **de fato iniciamos o treinamento** do modelo. Aqui definimos as bibliotecas, os hiperparâmetros e os caminhos de entrada e saída.

### Bibliotecas principais utilizadas

` ` `python
import sagemaker
import boto3
from sagemaker import image_uris
from sagemaker.inputs import TrainingInput
` ` `

**O que cada uma faz?**
* **sagemaker:** SDK do SageMaker para Python. Usado para criar e gerenciar jobs de treinamento, modelos e endpoints.
* **boto3:** SDK da AWS para Python. Permite interagir diretamente com serviços AWS via API (como S3).
* **image_uris:** Utilitário para recuperar a imagem (container Docker) correta do algoritmo (XGBoost) de acordo com a região e versão.
* **TrainingInput:** Classe que define os canais de dados (onde o SageMaker deve buscar os arquivos de treino e validação no S3).

### Hiperparâmetros do XGBoost

Os hiperparâmetros são ajustes que controlam como o modelo aprende. Diferente dos parâmetros (que o modelo aprende sozinho), esses nós definimos manualmente.

` ` `python
hyperparameters = {
        "max_depth":"5",
        "eta":"0.2",
        "gamma":"4",
        "min_child_weight":"6",
        "subsample":"0.7",
        "objective":"reg:squarederror",
        "num_round":"50"}
` ` `

**O que cada hiperparâmetro faz?**
* **max_depth:** Define a profundidade máxima da árvore. Árvores muito profundas podem causar *overfitting* (decorar os dados).
* **eta:** É a taxa de aprendizado. Controla o peso de cada nova árvore no resultado final.
* **gamma:** Define o ganho mínimo necessário para criar um novo "galho" na árvore (ajuda no controle de complexidade).
* **min_child_weight:** Peso mínimo necessário em um nó para que ele continue sendo dividido.
* **subsample:** Percentual de dados usados para treinar cada árvore (ajuda a tornar o modelo mais generalista).
* **objective:** Define o objetivo do treino. `reg:squarederror` é usado para problemas onde queremos prever um valor numérico (regressão).
* **num_round:** Quantidade de rodadas de treinamento (número total de árvores criadas).

---

## 03 - Execução do job de treinamento

Ao executar a célula, podemos observar que o job de treinamento foi iniciado. Também é possível confirmar isso no console do **SageMaker Studio**, onde o job aparece listado com o status **"In progress"**.

![alt text](/Training%20models/images/train/train_model-02.png)

![alt text](/Training%20models/images/train/train_model-03.png)

---

## 04 - Revisando o treinamento do modelo

Após a conclusão, podemos revisar a avaliação do treinamento no job criado. Aqui observamos métricas fundamentais:

* **MSE (Mean Squared Error):** Erro quadrático médio. Ele calcula a média da diferença entre o valor real e o previsto elevada ao quadrado. Útil para penalizar erros grandes.
* **RMSE (Root Mean Squared Error):** É a raiz quadrada do MSE. É mais fácil de ler pois está na mesma unidade do nosso dado original.

![alt text](/Training%20models/images/train/train_model-04.png)

### Artefatos do modelo (Model Artifacts)

Também podemos visualizar os **artefatos**. No SageMaker, artefatos são os arquivos gerados após o treino (geralmente um arquivo `.tar.gz`) que contêm tudo o que o modelo aprendeu. Eles são salvos no seu bucket S3 e são essenciais para fazer o deploy do modelo depois.

![alt text](/Training%20models/images/train/train_model-05.png)
![alt text](/Training%20models/images/train/train_model-06.png)

### Configurações do job (Aba Configuration)

Na aba **Configuration**, é possível revisar os hiperparâmetros e configurações de infraestrutura utilizados. Analisar esses dados é importante porque, em testes futuros, podemos alterar esses valores para tentar alcançar um desempenho ainda melhor.

---
# Hyperparameter Tuning no SageMaker Studio com XGBoost

Nesta seção, entraremos na etapa de **Hyperparameter Tuning** (ajuste de hiperparâmetros) utilizando o **mesmo modelo/notebook da aula anterior**, com a adição de novos scripts para alcançar esse objetivo.

O script utilizado está disponível em:

- `hyperparameters_tuning/script/Hyperparameter+Tuning.txt`

Para facilitar o entendimento, ele foi dividido em etapas com a marcação:

- `////////`

A ideia é estudar o processo em partes, entendendo o que cada bloco faz.

---

## Por que o Hyperparameter Tuning é importante?

O desempenho de um modelo de Machine Learning não depende apenas dos dados e do algoritmo escolhido, mas também dos **hiperparâmetros** configurados.

No XGBoost, por exemplo, hiperparâmetros como:

- profundidade da árvore (`max_depth`)
- taxa de aprendizado (`eta`)
- regularização (`gamma`)
- número de rodadas (`num_round`)

podem impactar diretamente:

- a capacidade de generalização do modelo
- o risco de overfitting/underfitting
- a qualidade das previsões
- o tempo de treinamento

O **Hyperparameter Tuning** busca encontrar automaticamente uma combinação de valores que produza um melhor resultado para a métrica definida.

---

## Objetivo desta seção

Nesta etapa, utilizaremos ferramentas do **SageMaker Studio** para:

- definir faixas de valores (ranges) para hiperparâmetros
- iniciar múltiplos jobs de treinamento automaticamente
- comparar os resultados
- identificar o **best tuning job**
- reaproveitar os melhores hiperparâmetros em um novo treinamento

> Importante: este estudo tem foco em **entender o processo de ML**, e não apenas executar código.  
> Sempre analise/debugue o código antes de rodar as células.

---

## 01 - Setup inicial e configuração do tuning job

Na primeira etapa do script, temos:

- importações necessárias
- inicialização da sessão do SageMaker
- recuperação do **IAM Role** de execução
- definição dos **ranges de hiperparâmetros** (intervalos de busca)

Esses ranges são importantes porque dizem ao SageMaker **quais valores testar** para encontrar o melhor ajuste.

### O que acontece nessa etapa?

De forma geral, o script prepara:

- o estimador (XGBoost)
- os dados de entrada (train/validation)
- a métrica objetivo (ex.: `validation:rmse`)
- a estratégia de tuning
- o número máximo de jobs e jobs paralelos

Depois disso, o SageMaker começa a criar e executar vários jobs de treinamento automaticamente.

![Setup do tuning - parte 1](/Training%20models/images/tuning/tuning-00.png)
![Setup do tuning - parte 2](/Training%20models/images/tuning/tuning-01.png)

Após rodar, o SageMaker exibe informações sobre os jobs criados/em execução.  
Também podemos acompanhar isso pela interface do **SageMaker Studio** em:

- **Training**
- **Tuning jobs**

![Tuning jobs em execução](/Training%20models/images/tuning/tuning-02.png)

---

## 02 - Buscando o Best Tuning Job

Após a execução de todos os jobs, podemos identificar o **best tuning job**, ou seja, o job que teve o melhor desempenho com base na métrica objetivo configurada.

Para isso, utilizamos a segunda parte do script em uma nova célula.

![Buscando o best tuning job](/Training%20models/images/tuning/tuning-03.png)
![Buscando o best tuning job](/Training%20models/images/tuning/tuning-05.png)

No meu caso, o melhor job foi:

- `xgb-tuning-job-2-032-eb187fa3`

Na saída do script, podemos observar métricas importantes desse job, por exemplo:

Metric Name: ObjectiveMetric, Value: 0.313620001077652
Metric Name: train:rmse, Value: 0.32798001170158386
Metric Name: validation:rmse, Value: 0.313620001077652

## O que essas métricas representam?

### `ObjectiveMetric`

É a métrica principal usada pelo SageMaker para decidir qual job foi o melhor.

- Pode ser **RMSE**, **AUC**, **Accuracy**, etc.
- Depende da configuração do tuning job

### `train:rmse`

Erro do modelo nos dados de treino (**RMSE = Root Mean Squared Error**).

### `validation:rmse`

Erro do modelo nos dados de validação (**RMSE**).

Em problemas de regressão com RMSE, normalmente **quanto menor, melhor**.

---

## Revisando o job na interface do SageMaker Studio

Voltando à listagem de **Training Jobs**, podemos localizar o job escolhido como melhor e revisar seus detalhes, como:

- métricas registradas
- local de saída (artefatos no S3)
- hiperparâmetros utilizados
- configurações do job

![Buscando o best tuning job](/Training%20models/images/tuning/tuning-04.png)
![Buscando o best tuning job](/Training%20models/images/tuning/tuning-06.png)
Essa análise é importante para entendermos quais combinações de hiperparâmetros geraram melhor desempenho.

---

## 03 - Reaproveitando os melhores hiperparâmetros no treinamento

Também podemos utilizar a terceira e última parte do script para:

- extrair os hiperparâmetros do **best tuning job**
- aplicar esses valores em um novo treinamento
- treinar novamente o modelo, agora com hiperparâmetros ajustados

![Buscando o best tuning job](/Training%20models/images/tuning/tuning-07.png)

Essa etapa é muito útil porque nos permite transformar o resultado do tuning em um treinamento final mais otimizado.

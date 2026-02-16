Nesta seção, adicionaremos a parte de análise em nosso fluxo de dados. Com a análise, podemos ter uma visão geral do comportamento dos nossos dados, observar correlação entre variáveis, visualizar diferentes tipos de gráficos, detectar possíveis outliers, entre outros insights importantes para orientar as próximas etapas do preparo dos dados e do Machine Learning.

---

## 01 - Criando uma análise no fluxo

Primeiro, clicamos no ícone de **"+"** no segundo passo do nosso workflow **"data types"**.  
Ao clicar, você poderá selecionar entre diferentes opções, como adicionar transformação de dados, gerar uma análise dos dados e até utilizar NLP para interagir com um chatBot que pode trazer insights sobre o dataset.

Para este estudo, selecionaremos a opção **"Get data inights"**.

![alt text](/Data%20Wrangler/images/data_analyses/analyses-01.png)

---

## 02 - Configurando a análise

Na tela a seguir, podemos selecionar e configurar a nossa análise.

No campo **"Analysis type"**, podemos escolher entre vários tipos de análises. Eu irei selecionar a opção **"Feature correlation"** para observar a correlação entre nossos dados e, no tipo da correlação, irei escolher **"linear"**.  
Sinta-se à vontade para explorar e observar as demais opções, pois elas ajudam a entender melhor os dados antes de iniciar as transformações e o treinamento.

Clique em **"Create"** para criar a nossa análise. Caso algum erro ocorra, basta clicar em **"Preview"**.

![alt text](/Data%20Wrangler/images/data_analyses/analyses-02.png)

---

## 03 - Interpretando os resultados

A aba principal será atualizada com a análise criada.

Na análise de correlação, observamos que é apresentada a taxa de correlação entre nossas features e uma feature específica (dependendo da configuração). Isso ajuda a identificar:
- quais variáveis tendem a se mover juntas
- possíveis relações fortes (positivas ou negativas)
- variáveis com baixa relevância (pouca correlação, dependendo do contexto)
- sinais de multicolinearidade (features muito parecidas, que podem atrapalhar alguns modelos)

Também temos a opção de observar a **matriz de correlação**, mostrando como cada feature se comporta em relação às demais.

![alt text](/Data%20Wrangler/images/data_analyses/analyses-03.png)

![alt text](/Data%20Wrangler/images/data_analyses/analyses-03-01.png)

### Benefício de adicionar análises no dataflow
Adicionar análises dentro do dataflow traz vantagens importantes:
- cria um histórico visual do “antes e depois” (ajuda a entender o impacto das transformações)
- facilita detectar problemas cedo (outliers, colunas inconsistentes, colunas redundantes)
- melhora a tomada de decisão sobre quais features manter, ajustar ou remover
- ajuda a direcionar a feature engineering com base em evidências
- deixa o fluxo mais organizado e reproduzível (documenta o raciocínio junto do processo)

---

## 04 - Análise registrada no data flow

Tudo feito. Agora podemos voltar ao nosso **data flow** e observar que a nossa análise foi registrada como parte do fluxo.

![alt text](/Data%20Wrangler/images/data_analyses/analyses-04.png)

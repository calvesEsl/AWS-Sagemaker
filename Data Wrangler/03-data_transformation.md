Nesta seção, iremos adicionar transformações aos nossos dados, como limpeza, remoção de outliers, detecção e tratamento de valores nulos, ajustes de formatação, entre outras correções.

### Importância da transformação de dados
A etapa de transformação é essencial porque dados do mundo real quase nunca chegam “prontos” para análise ou Machine Learning. Ao transformar os dados, nós:
- aumentamos a consistência do dataset (mesmo padrão de escrita e formatação)
- reduzimos ruídos (outliers e erros que podem distorcer métricas e modelos)
- tratamos valores ausentes (evitando falhas e melhorando a qualidade do treino)
- deixamos o dataset mais confiável para análises e para a criação de features
- melhoramos a qualidade dos insights e o desempenho de modelos no futuro

Em resumo: um bom modelo começa com um bom preparo de dados.

---

## 01 - Adicionando uma nova transformação no dataflow

Primeiro, clicamos no ícone de **"+"** no segundo passo do nosso workflow **"data types"**.  
Ao clicar, você poderá selecionar entre diferentes opções, como adicionar transformação de dados, gerar uma análise dos dados e até utilizar NLP para interagir com um chatBot que pode trazer insights sobre o dataset.

Para este estudo, selecionaremos a opção **"Add tranform"** -> **"Add new"** para adicionarmos uma nova transformação de dados ao nosso dataflow.

![alt text](/Data%20Wrangler/images/transform/transform-01.png)

---

## 02 - Tela de transformação e escolha do tipo

Na página desta etapa, podemos:
- visualizar os nossos dados
- interagir com o **"chat for data prep"** no canto superior esquerdo
- adicionar uma transformação

![alt text](/Data%20Wrangler/images/transform/transform-02.png)

![alt text](/Data%20Wrangler/images/transform/transform-02-01.png)

Na configuração de transformação dos nossos dados, podemos selecionar entre múltiplas formas de manipular o dataset, como remoção de outliers, remoção de colunas, tratamento de valores vazios, substituição de valores, ajustes de texto, etc.

A opção que irei selecionar é **"Handle outliers"**, para removermos valores discrepantes que não condizem com nossos dados ou com o mundo real. No nosso caso, a coluna **"Age"** é um exemplo claro, pois existem registros com valores como **170**, o que indica um outlier.

![alt text](/Data%20Wrangler/images/transform/transform-02-02.png)

Como a imagem acima mostra, podemos adicionar configurações específicas, como:
- o modo de ajuste para outliers
- a coluna que queremos tratar os outliers
- configurações avançadas, como o tipo de ajuste (no meu caso, vou deletar o registro atípico)
- valores mínimos e máximos aceitos, entre outros parâmetros

Eu irei selecionar a opção de **detectar e corrigir valores atípicos em características numéricas usando estatísticas robustas a valores atípicos**.

Depois, clique em **"Add"** e siga para a próxima etapa.

---

## 03 - Validando o resultado da transformação

Na nossa listagem, podemos ver que a transformação foi aplicada com sucesso. O registro com valor de idade **170** foi deletado do nosso dataset.

![alt text](/Data%20Wrangler/images/transform/transform-03.png)

---

## 04 - Transformação registrada no dataflow

Voltando para nosso dataflow, vemos que a nossa transformação foi adicionada.

Além disso, eu também fiz outras transformações nos dados como exercício, por exemplo:
- retirei valores vazios
- ajustei erros de escrita na coluna workclass (**Prvt -> Private**)
- e outras transformações que identifiquei durante a análise

Essas transformações ajudam a deixar o dataset mais consistente para os próximos passos do fluxo.

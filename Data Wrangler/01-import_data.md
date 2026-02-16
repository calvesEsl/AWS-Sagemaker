Aqui, aprenderemos como importar um arquivo para começarmos nossas análises. Utilizaremos o arquivo `income_data.csv`, disponível na nossa pasta de datasets.

O intuito deste dataset é praticar **limpeza**, **transformação** e **observação** dos dados. As colunas apresentam **valores vazios**, **erros de ortografia** e **formatos diferentes** dos demais valores dentro da mesma coluna (inconsistências comuns em dados reais).

---

## 01 - Acessando o Studio e abrindo o Canvas

Ao acessar nosso Studio, utilizaremos a ferramenta do **SageMaker canvas** para iniciar nossa importação de dados e aguardaremos alguns minutos para que a nossa instância do espaço de trabalho seja inicializada. Após a inicialização, podemos clicar em **"Open canvas"** para acessar.

### Conceito do Canvas
O **SageMaker canvas** é uma ferramenta visual (no/low-code) do SageMaker que ajuda a trabalhar com dados e Machine Learning de forma mais guiada, sem precisar programar. Ele permite importar dados, explorar datasets e utilizar recursos integrados (como o **data wrangler**) para preparar dados e apoiar o fluxo de ML.

![alt text](/Data%20Wrangler/images/import_data/studio-01.png)

---

## 02 - Acessando o data wrangler no Canvas

Na página inicial do Canvas, podemos ver a listagem dos recursos e ferramentas ao lado esquerdo. Iremos utilizar o **data wrangler** para nosso estudo atual.

### Conceito do data wrangler
O **data wrangler** (SageMaker Data Wrangler) é uma ferramenta do SageMaker para **simplificar a preparação de dados** para Machine Learning, com um fluxo bem “de ponta a ponta”. Com ele, conseguimos:
- importar dados de diversas fontes
- limpar e transformar dados (padronização, ajustes de tipos, tratamento de nulos, etc.)
- visualizar distribuições e obter insights
- realizar feature engineering (criar e modificar features)
- exportar o dataset e/ou o fluxo para uso no SageMaker e outros serviços AWS

![alt text](/Data%20Wrangler/images/import_data/studio-02.png)

---

## 03 - Iniciando a importação em Dataflow

Na aba **dataflow** do **data wrangler** podemos listar e observar nossos fluxos de trabalho. Vamos importar o nosso dataset com a opção **"import And prepare"**, selecionando a opção de **dados tubulares**.

![alt text](/Data%20Wrangler/images/import_data/studio-03.png)

![alt text](/Data%20Wrangler/images/import_data/studio-03-01.png)

---

## 04 - Selecionando a fonte dos dados (data source)

Na tela de importação de dados tubulares, clicamos na opção de selecionar um **data source** localizado no canto superior esquerdo. Iremos utilizar a opção de **"Local upload"**.

![alt text](/Data%20Wrangler/images/import_data/studio-04.png)

### Outras opções de importação (S3, Athena e Redshift)
Além do **"Local upload"**, existem outras opções comuns de importação:

- **S3**  
  Indicado quando seu dataset está armazenado em um bucket. É um caminho muito usado em cenários reais porque facilita reutilização, versionamento e automação do fluxo.

- **Athena**  
  Permite importar dados a partir de consultas SQL (normalmente dados no S3 via Glue Data Catalog). É útil quando você já consulta seus dados por SQL e quer trazer o resultado direto para o data wrangler.

- **Redshift**  
  Permite importar dados diretamente do data warehouse. É útil quando os dados oficiais/operacionais da organização estão no Redshift e você precisa preparar features a partir deles.

Após selecionarmos a opção local, basta clicar em **"Select files from your computer"** ou arrastar o arquivo para a área.  
Ao lado, estará a listagem do nosso arquivo, indicando que está pronto para importação. Em seguida, clicamos em **next**.

![alt text](/Data%20Wrangler/images/import_data/passo-04-01.png)

---

## 05 - Pré-visualização do dataset e importação

Aqui veremos uma pré visualização do nosso dataset. Podemos confirmar valores, configurar nome e outras configurações de importação. Deixaremos tudo como default e clicaremos em **"import"**.

![alt text](/Data%20Wrangler/images/import_data/studio-05.png)

---

## 06 - Data flow criado com sucesso

Tudo certo até aqui. Seremos direcionados para a tela do nosso **data flow**, onde podemos visualizar o primeiro passo (**Source**) efetuado com sucesso.

![alt text](/Data%20Wrangler/images/import_data/studio-06.png)

### O que é o dataflow no data wrangler?
O **dataflow** é o “fluxo de trabalho” visual do data wrangler. Ele representa, em etapas, tudo o que estamos fazendo com o dataset, por exemplo:
- **Source** (a origem do dado)
- etapas de **transformação/limpeza**
- etapas de **feature engineering**
- e, futuramente, etapas de **exportação**

A principal vantagem do dataflow é que ele ajuda a organizar e documentar o processo, deixando claro o que foi feito nos dados e permitindo repetir o mesmo fluxo depois.

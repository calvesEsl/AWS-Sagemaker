Nesta seção, iremos aprender como exportar dados do nosso dataflow para um bucket S3 para futuramente utilizarmos em um notebook.

### Importância da exportação para uso em treinamento de modelos
Exportar o resultado do nosso dataflow é uma etapa essencial, porque é nesse momento que transformamos todo o trabalho de preparação (limpeza, correções e feature engineering) em um artefato reutilizável. Isso permite:
- usar o dataset preparado em **notebooks** para explorar, treinar e avaliar modelos
- garantir consistência, evitando refazer manualmente as transformações a cada teste
- reaproveitar o mesmo fluxo em diferentes execuções (padrão e reprodutibilidade)
- facilitar a integração com pipelines e etapas de treinamento no SageMaker
- manter uma versão do processo de preparação junto com o resultado (boa prática em projetos de ML)

Em resumo: exportar é o que conecta o preparo de dados ao treinamento e à experimentação de modelos.

---

## 01 - Exportando via ações do dataflow

No nosso dataflow, iremos selecionar a opção de **"export"** nas ações. Aqui irá conter várias formas de exportar, incluindo `.csv` para um bucket S3 e outros formatos e destinos.

Eu irei selecionar a opção de **"Export via jupyter notebook"**, para salvarmos um arquivo `.ipynb` em um bucket S3.

![alt text](/Data%20Wrangler/images/data_export/export-02.png)

---

## 02 - Export dataflow as notebook

Irá abrir um modal de **"export dataflow as notebook"**, onde você pode selecionar a opção de download local de uma cópia ou exportar para um bucket S3.

Eu irei selecionar a opção do bucket S3 e clicar em **"Browse"** para selecionar um bucket específico para esse nosso estudo.

![alt text](/Data%20Wrangler/images/data_export/export-03.png)

---

## 03 - Escolhendo o bucket

Irá ser apresentada uma tela para a escolha de um bucket, onde estarão listados os seus buckets disponíveis.

![alt text](/Data%20Wrangler/images/data_export/export-04.png)

---

## 04 - Concluindo a exportação

Com o bucket selecionado, podemos clicar em **"export"** para concluir a nossa exportação.

![alt text](/Data%20Wrangler/images/data_export/export-05.png)

---

## 05 - Validando o arquivo exportado no S3

Na página do serviço **S3 -> buckets -> bucket** que selecionamos, podemos ver que a exportação foi concluída com sucesso, gerando um arquivo `.ipynb` para utilizarmos em nossos testes.

![alt text](/Data%20Wrangler/images/data_export/export-06.png)

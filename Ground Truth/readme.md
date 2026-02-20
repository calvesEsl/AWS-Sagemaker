# SageMaker Ground Truth — Estudos

Nesta pasta estão meus estudos práticos do **Amazon SageMaker Ground Truth**, focados em rotulagem de dados para Machine Learning (ex.: **classificação de imagens**).

## O que fizemos aqui (resumo)

- Upload de um dataset de imagens no **S3** (organizando em pastas de **input/output**)
- Criação de um **Labeling Workforce** (Private team + workers)
- Criação de um **Labeling Job** de **Image Classification (Single Label)**
- Rotulagem das imagens no **Labeling portal**
- Validação dos resultados no **S3**, principalmente via arquivos **.manifest** (outputs do job)

> **Manifest (.manifest):** é um arquivo de “metadados + registros” que lista os objetos do dataset (ex.: caminhos das imagens no S3) e, após a rotulagem, passa a incluir também as **anotações/labels** geradas pelo Ground Truth. Ele é o formato principal para “transportar” dataset + rótulos para treino/avaliação.

## Estrutura da pasta

- `config_data/`
  - `images/` — prints do processo de upload/organização do dataset no S3 e o dataset que foi ultilizado
  - `create_bucket.md` — guia para criar/abrir bucket, fazer upload do dataset e deixar os dados prontos para rotulagem

- `setting_up_workforce/`
  - `images/` — prints da criação/configuração do workforce (equipe)
  - `config_workforce.md` — guia para criar um **Labeling workforce** (ex.: private team + workers) e habilitar acesso ao portal de rotulagem

- `labeling_jobs/`
  - `images/` — prints da criação do job, IAM role, manifests e portal do worker
  - `create_labeling_jobs.md` — guia para criar um **Labeling job** (ex.: Image Classification), configurar input/output no S3, selecionar workers e executar a rotulagem

## Resultado final
Ao final, o Ground Truth gera arquivos de **output** no S3 (incluindo **.manifest**) com:
- quais imagens foram rotuladas
- quais labels foram atribuídos
- onde os resultados estão, para usar depois em **treino/validação de modelos**

## Observação
O objetivo é estudo/teste, mantendo configurações default sempre que possível.

---

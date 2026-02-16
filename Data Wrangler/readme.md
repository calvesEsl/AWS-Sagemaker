# SageMaker — Data Wrangler

Esta pasta reúne materiais e exemplos sobre o **Amazon SageMaker Data Wrangler**, uma ferramenta que **simplifica a preparação de dados para Machine Learning** com um fluxo “de ponta a ponta”, desde a importação até a exportação do processamento para o SageMaker.

A proposta aqui é manter um conteúdo prático e direto, focado em como configurar e utilizar o Data Wrangler para acelerar o trabalho de tratamento de dados e criação de features.

---

## O que é o Data Wrangler

O **SageMaker Data Wrangler** é uma interface visual (com suporte a transformações e pipelines) para:

- importar dados de diferentes fontes
- limpar e transformar datasets
- visualizar e entender padrões
- criar e ajustar features (feature engineering)
- exportar o fluxo para consumo em jobs do SageMaker ou outros serviços da AWS

---

## Fluxo principal (end-to-end)

### 1) Importar dados
Conecta e traz dados de fontes comuns como:
- **Amazon S3**
- **Amazon Redshift**
- **Amazon EMR**
- **SageMaker Feature Store**

### 2) Preparar e limpar dados
Permite aplicar transformações de forma guiada, como:
- normalização/padronização
- remoção de nulos e duplicados
- correção de tipos de dados
- filtros, joins e agregações

### 3) Visualizar dados
Ajuda a obter insights rapidamente:
- distribuição de valores
- estatísticas descritivas
- identificação de outliers e padrões

### 4) Feature Engineering
Cria e modifica features para melhorar o desempenho de modelos:
- geração de colunas derivadas
- encoding/categorias
- binning, escalonamento e transformações
- seleção e ajustes de variáveis

### 5) Exportar dados e fluxo
Exporta o dataset final e/ou o fluxo de transformações para:
- **SageMaker (training jobs, pipelines, etc.)**
- outros serviços AWS integrados ao seu workflow

---

## Objetivo desta pasta

- Consolidar **conceitos e práticas** do Data Wrangler
- Guardar **passos de setup**, prints e observações úteis
- Organizar **demos reproduzíveis** para estudo e referência

---

# SageMaker — Feature Store

Nesta pasta estudaremos o **Amazon SageMaker Feature Store**, que é um repositório gerenciado para **armazenar, versionar, compartilhar e servir features** (variáveis) usadas em modelos de Machine Learning.

A ideia do Feature Store é resolver um problema bem comum em ML:  
**as features usadas no treino precisam ser as mesmas usadas na inferência**, com consistência, governança e reuso.

---

## O que é o Feature Store?

O **Feature Store** organiza features em **Feature Groups** (grupos de features), que funcionam como uma “tabela” lógica de registros (ex.: clientes, pedidos, transações).

Um **Feature Group** normalmente possui:
- **Record identifier**: a chave do registro (ex.: `customer_id`)
- **Event time feature**: a coluna de tempo do evento (ex.: `EventTime`)
- **Feature definitions**: as features e seus tipos (String, Integral, Fractional)
- Armazenamento **Online**, **Offline**, ou **Online & Offline**

---

## Online store vs Offline store (quando usar)

- **Online store**: quando você precisa buscar features em **tempo real** para **inferência com baixa latência**  
  (ex.: sua API consulta as features do cliente e gera uma previsão na hora).

- **Offline store**: quando você precisa usar features para **treinamento** e **análises**.  
  Os dados ficam no **S3** e integram com **AWS Glue Data Catalog** e consultas via **Athena**  
  (ótimo para montar datasets históricos, validações e analytics).

- **Online & Offline storage**: quando você quer **treino + inferência** usando a mesma fonte de verdade  
  (padrão comum em projetos de ML).

---

## O que você vai encontrar aqui

Este conteúdo foca no “hands-on”:

- Criação de **Feature Group** via interface (Studio)
- Explicação dos campos principais (nome, storage, record identifier, event time)
- Configuração **Online/Offline**
- Ingestão de dados e validação do status
- Notebook de referência para criação e ingestão

---

## Arquivos desta pasta

- `create_group.md`  
  Passo a passo (com prints) de como criar um **Feature Group** no SageMaker Studio.

- `Feature Store/create_with_notebook/SageMaker_Feature_Store_Notebook_With_Docs.ipynb`  
  Notebook de estudo com criação de Feature Groups e ingestão de dados.

- `images/`  
  Imagens utilizadas no guia (`create_group-00.png`, `create_group-01.png`, etc).

---

## Observações importantes

- **Custos**: Online Store pode gerar custo dependendo de uso/volume.  
  Ao finalizar o lab, revise os recursos criados para evitar cobranças desnecessárias.

---

## Próximos passos (Feature Store/create_with_notebook/SageMaker_Feature_Store_Notebook_With_Docs.ipynb)

- Criar o Feature Group (UI)
- Ingerir dados (Notebook)
- Consultar dados no Offline Store via Athena (Glue Catalog)
- Buscar features no Online Store para simular inferência em tempo real

---

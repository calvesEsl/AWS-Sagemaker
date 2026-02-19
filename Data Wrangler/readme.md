# AWS SageMaker — Estudos e Demos (Setup, Configuração e Uso)

Este repositório reúne anotações, passos de configuração e demonstrações práticas de como configurar, setar e utilizar ferramentas do Amazon SageMaker.

O objetivo é duplo:
- Reforçar meus estudos na trilha de Machine Learning na AWS (hands-on + conceitos).
- Ajudar outras pessoas que também estão aprendendo SageMaker, com um guia prático e reproduzível.

---

## O que você vai encontrar aqui

Conteúdos focados em “como fazer” (hands-on), com passo a passo, prints e exercícios, incluindo:

- SageMaker Studio
  - Como criar um domínio e acessar o Studio
- SageMaker Canvas
  - Uso do Canvas como porta de entrada para fluxos de preparação de dados
- Data Wrangler
  - Importação de dados (Local upload, S3, Athena, Redshift)
  - Dataflow (criação e organização do fluxo)
  - Análises no dataflow (ex.: "Get data inights" -> "Feature correlation")
  - Transformações (ex.: "Add tranform" -> "Add new", "Handle outliers", tratamento de nulos e ajustes de valores)
  - Exportação do dataflow (ex.: "export" -> "Export via jupyter notebook" para S3)

A ideia é manter tudo de forma simples e direta: do “zero” (setup) até ter dados preparados e exportados para usar em notebooks e etapas de treinamento de modelos.

---

## Estrutura do repositório

A estrutura abaixo reflete o conteúdo visto até agora e pode evoluir com novos tópicos:

- `SageMaker Studio/`
  - `domain_config/`  
    - criação do domínio e acesso ao Studio
- `Data Wrangler/`
  - `datasets/`
    - `income_data.csv`
  - `images/`
    - `import_data/`
    - `data_analyses/`
    - `transform/`
    - `data_export/`
  - `import_data.md`
  - `data_analyses.md`
  - `data_transformation.md`
  - `data_export.md`

---

## Pré-requisitos

Para reproduzir os exemplos, normalmente você vai precisar de:

- Uma conta AWS (de preferência com MFA habilitado)
- Permissões adequadas para SageMaker (IAM Role/Policies)
- Acesso ao SageMaker Studio
- (Opcional) Um bucket S3 para armazenar datasets e outputs

---

## Como usar este repositório

1. Comece por `SageMaker Studio/domain_config/` para criar o domínio e liberar o Studio.
2. Depois siga a sequência em `Data Wrangler/`:
   - `import_data.md`
   - `data_analyses.md`
   - `data_transformation.md`
   - `data_export.md`
3. Replique o fluxo na sua conta AWS.
4. Compare seus resultados com os prints e observações.

Se você estiver estudando para certificações, recomendo anotar:
- O que o serviço faz
- Quando usar
- Integrações
- Boas práticas e segurança
- Custos e cuidados (ex.: desligar ou excluir recursos quando terminar)

---

## Segurança e custos

- Evite publicar dados sensíveis (chaves, tokens, IDs internos, dados pessoais).
- Sempre que terminar um laboratório, revise e encerre recursos que geram custo (instâncias, apps do Studio, endpoints, jobs, etc.).
- Se possível, configure AWS Budgets para evitar surpresas.

---

## Contribuições

Sugestões e melhorias são bem-vindas. Se você quiser contribuir:
- abra uma issue com sugestões/erros
- ou envie um pull request com melhorias

---

## Observação

Este repositório é voltado para aprendizado e demonstrações.  
Ele não substitui a documentação oficial da AWS, mas tenta tornar o caminho mais prático e direto.

---

## Contato

Se quiser trocar ideia sobre os labs ou a trilha de estudos:
- LinkedIn: https://www.linkedin.com/in/caio-alves-520469266/

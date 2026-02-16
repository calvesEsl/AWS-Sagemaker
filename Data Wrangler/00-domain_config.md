# Criando um domínio no SageMaker (para usar o SageMaker Studio)

A seguir está um passo a passo para criar um **Domínio do SageMaker** e acessar o **SageMaker Studio** para iniciar o fluxo de Machine Learning. Este guia foi escrito com foco em estudo pessoal, mas também explica as opções voltadas para organizações.

---

## 1) Acessar o SageMaker na AWS

1. Na página inicial da AWS (AWS Management Console), utilize a **barra de busca de serviços**.
2. Pesquise por **SageMaker AI** e selecione o serviço.

![alt text](/Data%20Wrangler/images/domain_creation/passo-1.png)

---

## 2) Entendendo a página do SageMaker AI

Ao abrir o SageMaker AI, você verá no painel esquerdo várias ferramentas e recursos (Studio, Data Wrangler, Training, Pipelines, etc.).

Neste momento, o foco será **criar um Domínio**, pois ele é necessário para acessar o ambiente do **SageMaker Studio** e executar o fluxo de ML.

### Conceito: Domínio do SageMaker (o que é?)
Um **Domínio do SageMaker** é o “ambiente base” do **SageMaker Studio** dentro da sua conta AWS.  
Ele define, entre outras coisas:
- o método de autenticação (ex.: IAM Identity Center / SSO, IAM, etc., conforme a configuração disponível)
- as permissões (roles) para uso do SageMaker
- configurações de rede (por exemplo, acesso via VPC, quando aplicável)
- os **usuários** e seus perfis de execução
- padrões do workspace (armazenamento, apps e recursos associados)

![alt text](/Data%20Wrangler/images/domain_creation/passo-02.png)

Em resumo: o domínio é a estrutura que organiza e habilita o acesso ao Studio e aos recursos de trabalho.

---

## 3) Criar o domínio

1. Clique na opção para **criar um domínio**.
2. Você será direcionado para a página de configuração do domínio.

![alt text](/Data%20Wrangler/images/domain_creation/passo-03.png)

---

## 4) Escolher o tipo de configuração (setup) do domínio

Como este ambiente será usado **para estudo pessoal** e não para uma organização, selecione a opção **default** (configuração padrão) e clique em **Set up**.

### Setup for single user (o que significa?)
Essa opção é indicada para **uso individual**. Em geral, ela:
- cria um domínio com configurações padrão para começar rápido
- já provisiona um **usuário padrão** para você acessar o Studio
- reduz a complexidade de configuração (ideal para aprendizado, testes e labs)

### Setup for organizations (o que significa?)
Essa opção é indicada para **ambientes corporativos** e times. Normalmente ela é usada quando você precisa:
- gerenciar múltiplos usuários de forma centralizada
- aplicar políticas e permissões mais controladas (governança)
- padronizar acessos (SSO/Identity Center), rede (VPC), compliance e regras internas
- separar perfis e permissões por equipe/função (ex.: Data Scientist, MLOps, Analista)

![alt text](/Data%20Wrangler/images/domain_creation/passo-04.png)

---

## 5) Aguardar o provisionamento do Studio

Após escolher a forma de configuração do domínio, você será redirecionado para uma tela informando que o ambiente do **SageMaker Studio** está sendo configurado.

Esse processo pode levar alguns minutos. Basta aguardar até a finalização.

![alt text](/Data%20Wrangler/images/domain_creation/passo-05.png)

---

## Confirmação de criação do domínio

Voltando para a página inicial (ou para a lista de domínios), você verá a listagem dos seus domínios.

- Você pode acessar detalhes e configurações clicando no **hyperlink do domínio** na coluna **Name**.
- Por padrão, o domínio já vem com **1 usuário** configurado para uso.
  - Como o objetivo aqui é estudo, não será necessário criar usuários adicionais.

Quando o status do domínio, na coluna **Status**, estiver como **InService**, significa que o domínio está pronto.

![alt text](/Data%20Wrangler/images/domain_creation/passo-listagem.png)

Com o domínio em **InService**, você já pode **abrir o SageMaker Studio** e começar a trabalhar com os recursos (por exemplo, Data Wrangler, notebooks, pipelines, etc.).

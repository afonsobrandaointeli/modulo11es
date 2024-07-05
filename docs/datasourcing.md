# Módulo 11 de Engenharia de Software: Análise de Dados com RStudio

## Introdução

Nesta aula, vamos explorar a análise de dados avançada utilizando o RStudio e diversas ferramentas de suporte. Nosso parceiro, o Boston Consulting Group (BCG), fornecerá arquivos CSV de grande porte para análise. Vamos abordar desde a padronização e normalização dos dados até a construção de uma aplicação de análise de dados utilizando diversas tecnologias.

Utilizaremos o conceito de processamento de dados "Raw", "Working" e "Trusted".

## Arquitetura e Ferramentas

![image](https://res.cloudinary.com/dyhjjms8y/image/upload/v1720194394/Captura_de_tela_2024-07-05_124607_gfz5dt.png)

## Ferramentas Utilizadas

### RStudio
- **Descrição**: Ambiente de desenvolvimento integrado (IDE) para a linguagem de programação R.
- **Uso**: Análise de dados, geração de relatórios e visualizações.

### RMarkdown
- **Descrição**: Ferramenta para criar documentos dinâmicos com R.
- **Uso**: Geração de relatórios para cada arquivo CSV analisado.

### Appwrite
- **Descrição**: Plataforma de Backend as a Service (BaaS) que oferece serviços como autenticação, banco de dados, armazenamento e muito mais.
- **Uso**: Armazenamento de dados raw e dados processados, utilizando o storage e MariaDB.

### MariaDB
- **Descrição**: Sistema de gerenciamento de banco de dados relacional.
- **Uso**: Armazenamento de dados processados (dados working).

### ElasticSearch
- **Descrição**: Motor de busca e análise distribuído e de código aberto.
- **Uso**: Indexação e busca avançada dos dados processados.

### ClickHouse
- **Descrição**: Sistema de gerenciamento de banco de dados orientado a colunas, de código aberto, para consultas analíticas em tempo real.
- **Uso**: Armazenamento e análise de dados processados (dados trusted).

### Streamlit
- **Descrição**: Framework de código aberto para a criação de aplicações web interativas em Python.
- **Uso**: Construção de uma aplicação de análise de dados (DataApp).

### Apache Spark
- **Descrição**: Motor de análise unificada para processamento de dados em grande escala.
- **Uso**: Processamento e predição de dados em produção.

### Docker
- **Descrição**: Plataforma para desenvolvimento, envio e execução de aplicações em contêineres.
- **Uso**: Dockerização da aplicação Streamlit, ElasticSearch e ClickHouse.

### Poetry
- **Descrição**: Gestor de pacotes e dependências para projetos Python.
- **Uso**: Gerenciamento de dependências da aplicação Streamlit.

## Arquitetura de Processamento de Dados

**Recebimento dos Arquivos CSV**
   - Os arquivos CSV fornecidos pelo BCG serão carregados no RStudio para análise inicial.

**Análise e Padronização dos Dados**
   - Utilizando RStudio, os dados serão ajustados e padronizados.
   - Relatórios serão gerados em RMarkdown para cada arquivo CSV.

**Armazenamento dos Dados Raw**
   - Os arquivos CSV originais serão armazenados no storage do Appwrite.

**Normalização e Processamento dos Dados**
   - Os dados serão normalizados e processados no RStudio.
   - Dados processados (dados working) serão armazenados no MariaDB do Appwrite.

**Indexação e Armazenamento de Dados Trusted**
   - Um contêiner Docker do ElasticSearch será configurado para indexação e busca avançada.
   - Alternativamente, um contêiner Docker do ClickHouse será configurado para armazenamento e análise de dados processados.
   - Dados do MariaDB serão indexados no ElasticSearch ou armazenados no ClickHouse.

**Construção da Aplicação DataApp**
   - Utilizando Streamlit, uma aplicação interativa será desenvolvida para consumir dados do MariaDB, ElasticSearch e ClickHouse.
   - A aplicação será dockerizada e gerenciada com Poetry.

**Processamento com Apache Spark**
   - Apache Spark será utilizado para realizar predições com os dados em produção.

## O que é Backend as a Service (BaaS)?

Backend as a Service (BaaS) é um modelo de serviço que fornece uma infraestrutura de backend pronta para uso, permitindo que desenvolvedores se concentrem no desenvolvimento do frontend e na lógica de negócios. O BaaS oferece serviços como autenticação, banco de dados, armazenamento de arquivos, notificações push, entre outros, eliminando a necessidade de gerenciar servidores e infraestrutura.

## ElasticSearch vs ClickHouse

### ElasticSearch
**Descrição**: Motor de busca e análise distribuído, ideal para indexação e busca avançada.
**Vantagens**: 
  - Excelente para buscas textuais e análises em tempo real.
  - Suporte robusto para consultas complexas e agregações.
**Desvantagens**:
  - Pode ser mais complexo de configurar e gerenciar para grandes volumes de dados.

### ClickHouse
**Descrição**: Sistema de gerenciamento de banco de dados orientado a colunas, otimizado para consultas analíticas em tempo real.
**Vantagens**:
  - Desempenho extremamente rápido para consultas analíticas.
  - Otimizado para grandes volumes de dados e consultas de leitura intensiva.
**Desvantagens**:
  - Menos adequado para buscas textuais complexas comparado ao ElasticSearch.

Toda a arquitetura será criada com Docker e rodará on-premise, mas poderá ser facilmente integrada em uma nuvem ajustando os ambientes de conexão (envs).

## Ferramentas e Tecnologias

| Ferramenta       | Descrição                                                                 | Uso                                                                 |
|------------------|---------------------------------------------------------------------------|---------------------------------------------------------------------|
| **RStudio**      | IDE para R                                                                | Análise de dados, geração de relatórios                             |
| **RMarkdown**    | Ferramenta para documentos dinâmicos                                      | Geração de relatórios                                               |
| **Appwrite**     | Plataforma de BaaS                                                        | Armazenamento de dados raw e processados                            |
| **MariaDB**      | Sistema de gerenciamento de banco de dados relacional                     | Armazenamento de dados processados                                  |
| **ElasticSearch**| Motor de busca e análise distribuído                                      | Indexação e busca avançada dos dados                                |
| **ClickHouse**   | Sistema de gerenciamento de banco de dados orientado a colunas            | Armazenamento e análise de dados processados                        |
| **Streamlit**    | Framework para criação de aplicações web interativas                      | Construção de uma aplicação de análise de dados (DataApp)           |
| **Apache Spark** | Motor de análise unificada para processamento de dados em grande escala   | Processamento e predição de dados                                   |
| **Docker**       | Plataforma para desenvolvimento, envio e execução de aplicações em contêineres | Dockerização da aplicação Streamlit, ElasticSearch e ClickHouse     |
| **Poetry**       | Gestor de pacotes e dependências para projetos Python                     | Gerenciamento de dependências da aplicação Streamlit                |

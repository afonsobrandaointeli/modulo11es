<a href="https://drive.google.com/drive/folders/1pmO9_8W6W5_4a5tq0Oxby7LoZTjt5f6p?usp=drive_link" class="btn btn-primary" style="width: 100%; margin: 10px;">Dados do Módulo</a>

### Agosto
<a href="datasourcing" class="btn btn-primary" style="width: 100%; margin: 10px;">Data Sourcing e Data Analysis com R Studio</a>
<a href="arquitetura1" class="btn btn-primary" style="width: 100%; margin: 10px;">Arquitetura e Governança de Dados na Nuvem 1</a>
<a href="arquitetura2" class="btn btn-primary" style="width: 100%; margin: 10px;">Arquitetura e Governança de Dados na Nuvem 2</a>
<a href="ingestao" class="btn btn-primary" style="width: 100%; margin: 10px;">Ingestão e Processamento de Dados (Framework de testes e qualidade)</a>
<a href="seguranca" class="btn btn-primary" style="width: 100%; margin: 10px;">Segurança e Governança de Dados (LGPD)</a>
<a href="precificacao" class="btn btn-primary" style="width: 100%; margin: 10px;">Precificação em Nuvem</a>

### Setembro

<a href="metricas" class="btn btn-primary" style="width: 100%; margin: 10px;">Métricas, Telemetria e Gestão de Microserviços</a>
<a href="datalakes" class="btn btn-primary" style="width: 100%; margin: 10px;">Data Lakes e Data Warehouses</a>
<a href="etl" class="btn btn-primary" style="width: 100%; margin: 10px;">Serviços e ETLs para Transformação de Dados e Processamento de Dados em Escala</a>
<a href="processamento" class="btn btn-primary" style="width: 100%; margin: 10px;">Processamento de Dados na Nuvem</a>
<a href="mlops" class="btn btn-primary" style="width: 100%; margin: 10px;">Ciclo de Vida e Automatização de Pipeline de Dados (MLOps)</a>
<a href="predicao" class="btn btn-primary" style="width: 100%; margin: 10px;">Processamento e Predição em Produção</a>

### Outubro

<a href="ui_dashboards" class="btn btn-primary" style="width: 100%; margin: 10px;">User Interface e Dashboards</a>
<a href="datastorytelling" class="btn btn-primary" style="width: 100%; margin: 10px;">Data Storytelling</a>


## Boas Práticas para o Módulo

1. Iremos utilizar fortemente o [GitFlow](https://youtu.be/oweffeS8TRc?si=zgdwEXs-EIcftVmx)
2. Sugiro que vocês utilizem o [GitGraph](https://youtu.be/u9ZQpKGTog4?si=Y3TwjemDVhEe7VXH) para VSCode
3. Sugiro que o VSCode seja nosso ambiente principal de codificação
4. Instale o [Pyhton 3.12](https://www.python.org/downloads/) e sete como global
    - Instale o code tools na opção de instalação se for por windows
5. Vamos utilizar muito o Powershell no windows, se acostume!
6. Desinstale o Github Desktop! É sério...
7. Tenha instalado o [Docker e o Docker Compose](https://www.docker.com/products/docker-desktop/)
8. Instale o [R em sua última versão e o RStudio](https://posit.co/download/rstudio-desktop/)
9. Padronize seu nickname do git no seu computador desta forma:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu_email@exemplo.com"
```

- Mantendo o mesmo username e email em todo o módulo! ou instale o gh ou [github cli](https://cli.github.com/)

# Módulo 11 de Engenharia de Software: Análise de Dados com RStudio

## Introdução

Nesta aula, vamos explorar a análise de dados avançada utilizando o RStudio e diversas ferramentas de suporte. Nosso parceiro, o Boston Consulting Group (BCG), fornecerá arquivos CSV de grande porte para análise. Vamos abordar desde a padronização e normalização dos dados até a construção de uma aplicação de análise de dados utilizando diversas tecnologias.

Utilizaremos o conceito de processamento de dados "Raw", "Working" e "Trusted".

## Arquitetura e Ferramentas

![image](https://res.cloudinary.com/dyhjjms8y/image/upload/v1720194394/Captura_de_tela_2024-07-05_124607_gfz5dt.png)

## Ferramentas Utilizadas

### [RStudio](https://rstudio.com/)
- **Descrição**: Ambiente de desenvolvimento integrado (IDE) para a linguagem de programação R.
- **Uso**: Análise de dados, geração de relatórios e visualizações.
- **Mais detalhes**: RStudio é uma IDE poderosa para R que facilita a análise de dados, a criação de gráficos e a geração de relatórios. Ele oferece uma interface amigável e ferramentas integradas para ajudar na codificação, depuração e visualização de dados.

### [RMarkdown](https://rmarkdown.rstudio.com/)
- **Descrição**: Ferramenta para criar documentos dinâmicos com R.
- **Uso**: Geração de relatórios para cada arquivo CSV analisado.
- **Mais detalhes**: RMarkdown permite a criação de documentos dinâmicos que combinam código R, texto e visualizações. É ideal para gerar relatórios que podem ser facilmente atualizados com novos dados.

### [Appwrite](https://appwrite.io/)
- **Descrição**: Plataforma de Backend as a Service (BaaS) que oferece serviços como autenticação, banco de dados, armazenamento e muito mais.
- **Uso**: Armazenamento de dados raw e dados processados, utilizando o storage e MariaDB.
- **Mais detalhes**: Appwrite é uma plataforma BaaS que simplifica o desenvolvimento de aplicativos ao fornecer serviços essenciais como autenticação, banco de dados, armazenamento de arquivos e muito mais, tudo em uma única solução.

### [MariaDB](https://mariadb.org/)
- **Descrição**: Sistema de gerenciamento de banco de dados relacional.
- **Uso**: Armazenamento de dados processados (dados working).
- **Mais detalhes**: MariaDB é um sistema de gerenciamento de banco de dados relacional que é uma bifurcação do MySQL. Ele é conhecido por sua escalabilidade, desempenho e robustez, sendo amplamente utilizado para armazenar dados estruturados.

### [ElasticSearch](https://www.elastic.co/elasticsearch/)
- **Descrição**: Motor de busca e análise distribuído e de código aberto.
- **Uso**: Indexação e busca avançada dos dados processados.
- **Mais detalhes**: ElasticSearch é uma ferramenta poderosa para busca e análise de dados em tempo real. Ele permite a indexação rápida e eficiente de grandes volumes de dados, facilitando a busca e a análise avançada.

### [ClickHouse](https://clickhouse.com/)
- **Descrição**: Sistema de gerenciamento de banco de dados orientado a colunas, de código aberto, para consultas analíticas em tempo real.
- **Uso**: Armazenamento e análise de dados processados (dados trusted).
- **Mais detalhes**: ClickHouse é um sistema de banco de dados orientado a colunas que é otimizado para consultas analíticas em tempo real. Ele é ideal para grandes volumes de dados e oferece desempenho excepcional para análises complexas.

### [Streamlit](https://streamlit.io/)
- **Descrição**: Framework de código aberto para a criação de aplicações web interativas em Python.
- **Uso**: Construção de uma aplicação de análise de dados (DataApp).
- **Mais detalhes**: Streamlit é um framework que facilita a criação de aplicações web interativas para análise de dados. Com ele, é possível transformar scripts Python em aplicativos web de forma rápida e eficiente.

### [Apache Spark](https://spark.apache.org/)
- **Descrição**: Motor de análise unificada para processamento de dados em grande escala.
- **Uso**: Processamento e predição de dados em produção.
- **Mais detalhes**: Apache Spark é uma plataforma de processamento de dados em grande escala que oferece suporte para processamento em lote e em tempo real. Ele é amplamente utilizado para análise de big data e aprendizado de máquina.

### [Docker](https://www.docker.com/)
- **Descrição**: Plataforma para desenvolvimento, envio e execução de aplicações em contêineres.
- **Uso**: Dockerização da aplicação Streamlit, ElasticSearch e ClickHouse.
- **Mais detalhes**: Docker é uma plataforma que permite a criação, envio e execução de aplicações em contêineres. Ele facilita a portabilidade e a escalabilidade das aplicações, garantindo que elas funcionem de maneira consistente em diferentes ambientes.

### [Poetry](https://python-poetry.org/)
- **Descrição**: Gestor de pacotes e dependências para projetos Python.
- **Uso**: Gerenciamento de dependências da aplicação Streamlit.
- **Mais detalhes**: Poetry é uma ferramenta para gerenciamento de dependências e pacotes em projetos Python. Ele simplifica a instalação e atualização de bibliotecas, garantindo que todas as dependências sejam resolvidas corretamente.

### [Portainer](https://www.portainer.io/)
- **Descrição**: Interface de gerenciamento para Docker.
- **Uso**: Gerenciamento de contêineres Docker.
- **Mais detalhes**: Portainer é uma interface de usuário para gerenciamento de contêineres Docker. Ele facilita a administração de ambientes Docker, permitindo a visualização, criação e gerenciamento de contêineres de forma intuitiva.
- **Descrição**: Interface de gerenciamento para Docker.
- **Uso**: Gerenciamento de contêineres Docker.
<details>
  <summary>Mais detalhes</summary>
  Portainer é uma interface de usuário para gerenciamento de contêineres Docker. Ele facilita a administração de ambientes Docker, permitindo a visualização, criação e gerenciamento de contêineres de forma intuitiva.
</details>

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


## Mas isso não é ferro e fogo!

Sinta-se a vontade para trazer novas tecnologias para o nosso módulo! Conte com os professores para analisarmos juntos novas soluções. Aqui vai o refactoring Guru para dar novas ideias à vocês =)

![image](https://refactoring.guru/images/content-public/logos/logo-new-2x.png?id=3bc33294e095bab1d6fe9ae421d07837)

[Refactoring Guru](https://refactoring.guru/)
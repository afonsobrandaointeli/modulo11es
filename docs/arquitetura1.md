# Autoestudos

| 📚 **Nome**                                     | 🔗 **Link**                                                                 |
|-------------------------------------------------------|-----------------------------------------------------------------------------|
| 🎥 O que é governança de dados e como funciona?      | [Assistir](https://www.youtube.com/watch?v=2BNaO_KA-8o)                     |
| 📝 Arquiteto de Dados - Por Onde Começar em 5 Passos | [Ler](https://blog.dsacademy.com.br/arquiteto-de-dados-por-onde-comecar-em-5-passos/) |
| 🏢 Estruturas Organizacionais                        | [Acessar](https://integrada.minhabiblioteca.com.br/reader/books/9786587019536/pageid/99) |

# Agenda da Aula

|Atividade                                        |Min    |
|-------------------------------------------------|-------|
|Kahoot dos Autoestudos                           |20     |
|Aula Expositiva de Exemplo de Modelo de Template |40     |
|Vamos subir o Supabase e Analisar uma Arquitetura|60     |
|**Total**                                        |**120**|

# Kahoot

<a href="https://kahoot.it/" target="blank_" class="btn btn-primary" style="width: 100%; margin: 10px;"><strong>📟Kahoot.it</strong></a>

# Template de Arquitetura de Dados na Nuvem

## Introdução

Este documento delineia as diretrizes e decisões arquiteturais fundamentais para o projeto de Arquitetura e Governança de Dados na Nuvem. Ele fornece uma visão clara da estrutura global, abordando aspectos como padrões de design, escolhas tecnológicas, integração de sistemas, segurança e escalabilidade. Este template visa garantir consistência e coerência na implementação, facilitando a compreensão e promovendo uma abordagem unificada durante o desenvolvimento.

## Conformidade com Padrões Oficiais de Engenharia de Software

Este documento baseia-se nos padrões oficiais de engenharia de software, incluindo TOGAF e IEEE, adaptando sua estrutura às necessidades específicas do projeto.

## Seções Mínimas Requeridas

### Requerimentos/User Stories

#### Requerimentos Funcionais

- **RF001**: O sistema deve permitir a inserção de novos perfis de usuários.
- **RF002**: O sistema deve permitir a atualização de perfis de usuários existentes.
- **RF003**: O sistema deve permitir a exclusão de perfis de usuários.
- **RF004**: O sistema deve fornecer uma interface para visualização dos perfis de usuários.

#### Requerimentos Não Funcionais

- **RNF001**: O sistema deve ser escalável para suportar um grande número de usuários simultâneos.
- **RNF002**: O sistema deve garantir a segurança dos dados armazenados e transmitidos.
- **RNF003**: O sistema deve ter uma alta disponibilidade, com um tempo de inatividade máximo de 1%.
- **RNF004**: O sistema deve ser usável, com uma interface intuitiva e responsiva.

#### User Stories

- **US001**: Como um administrador, eu quero poder adicionar novos perfis de usuários para gerenciar melhor o acesso ao sistema.
- **US002**: Como um usuário, eu quero atualizar meu perfil para manter minhas informações atualizadas.
- **US003**: Como um administrador, eu quero excluir perfis de usuários inativos para manter a base de dados limpa.
- **US004**: Como um usuário, eu quero visualizar meu perfil para verificar minhas informações pessoais.

### Arquitetura (Em UML de Componentes)

#### Visão Geral da Arquitetura

![Visão Geral da Arquitetura](https://res.cloudinary.com/dyhjjms8y/image/upload/v1720194394/Captura_de_tela_2024-07-05_124607_gfz5dt.png)

#### Transformar a sua Arquitetura em UML de Componentes

![UML de componentes](https://d2slcw3kip6qmk.cloudfront.net/marketing/pages/chart/uml/component-diagram/component-diagram-example-497x318.PNG)

A arquitetura do sistema é baseada em uma estrutura modular, composta pelos seguintes componentes principais:

(Exemplo)

- **Frontend**: Interface do usuário desenvolvida em React.
- **Backend**: API RESTful desenvolvida em Node.js.
- **Banco de Dados**: PostgreSQL, gerenciado pelo Supabase.
- **Autenticação**: Gerenciada pelo Supabase Auth.
- **Armazenamento**: Supabase Storage para arquivos estáticos.

#### Padrões de Design

- **MVC (Model-View-Controller)**: Separação de responsabilidades entre a interface do usuário, lógica de negócios e acesso a dados.
- **RESTful API**: Interface de comunicação entre o frontend e o backend.
- **JWT (JSON Web Tokens)**: Para autenticação e autorização segura.

#### Escolhas Tecnológicas

- **Linguagem de Programação**: JavaScript/TypeScript
- **Frameworks**: React (Frontend), Node.js (Backend)
- **Banco de Dados**: PostgreSQL
- **Plataforma de Backend**: Supabase

#### Integração de Sistemas

- **CI/CD**: Integração contínua e entrega contínua usando GitHub Actions.
- **Monitoramento**: Ferramentas como Grafana e Prometheus para monitoramento de desempenho e saúde do sistema.

#### Segurança

- **Autenticação**: Implementação de autenticação baseada em JWT.
- **Autorização**: Políticas de acesso definidas no Supabase.
- **Criptografia**: Dados sensíveis são criptografados em trânsito e em repouso.

#### Escalabilidade

- **Horizontal Scaling**: Capacidade de adicionar mais instâncias de servidores conforme a demanda aumenta.
- **Load Balancing**: Distribuição de tráfego entre várias instâncias de servidores para otimizar a resposta do sistema.

### Auditoria

#### Processo de Auditoria

- **Registro de Logs**: Todos os eventos importantes são registrados para auditoria.
- **Revisão de Segurança**: Auditorias regulares de segurança para identificar e corrigir vulnerabilidades.
- **Compliance**: Garantia de conformidade com regulamentos como LGPD e GDPR.

## Efetividade da Navegação no Documento

Este documento foi estruturado para proporcionar uma navegação eficiente e intuitiva. Utilize o índice no início do documento para acessar rapidamente as seções desejadas.

## Design Visual

O design visual deste documento foi pensado para ser consistente e agradável, melhorando a experiência do usuário. Use cabeçalhos claros, listas e links para facilitar a leitura e a navegação.

# TOGAF: The Open Group Architecture Framework

![togaf](https://www.opengroup.org/sites/default/files/styles/no_style/public/TOGAF10-banner.png?itok=wiZswmdx)

TOGAF, ou The Open Group Architecture Framework, é um framework de arquitetura empresarial que fornece uma abordagem abrangente para o design, planejamento, implementação e governança da arquitetura de uma empresa. Desenvolvido pelo The Open Group, o TOGAF foi lançado pela primeira vez em 1995 e desde então passou por várias revisões, sendo a versão mais recente o TOGAF 9.2, lançado em abril de 2018.

O TOGAF é composto por vários componentes principais:

- **ADM (Architecture Development Method)**: O núcleo do TOGAF, que fornece um processo passo a passo para desenvolver uma arquitetura empresarial. As fases incluem:
  - *Preliminary Phase*: Preparação e iniciação das atividades de arquitetura.
  - *Phase A: Architecture Vision*: Definição da visão e escopo da arquitetura.
  - *Phase B: Business Architecture*: Desenvolvimento da arquitetura de negócios.
  - *Phase C: Information Systems Architectures*: Desenvolvimento das arquiteturas de dados e aplicações.
  - *Phase D: Technology Architecture*: Desenvolvimento da arquitetura tecnológica.
  - *Phase E: Opportunities and Solutions*: Identificação de oportunidades e soluções.
  - *Phase F: Migration Planning*: Planejamento da migração.
  - *Phase G: Implementation Governance*: Governança da implementação.
  - *Phase H: Architecture Change Management*: Gestão de mudanças na arquitetura.
  - *Requirements Management*: Gestão contínua dos requisitos.

- **Content Framework**: Fornece uma estrutura para organizar os artefatos de arquitetura, incluindo modelos, visões e pontos de vista, garantindo que todos os aspectos da arquitetura sejam abordados de forma consistente.

- **Enterprise Continuum**: Um repositório de ativos de arquitetura, incluindo modelos, padrões e melhores práticas, que promove a reutilização e a consistência na arquitetura empresarial.

- **TOGAF Reference Models**: Inclui vários modelos de referência, como o TRM (Technical Reference Model) e o III-RM (Integrated Information Infrastructure Reference Model), que fornecem orientações para o desenvolvimento de arquiteturas específicas.

Os benefícios do TOGAF incluem:

- **Alinhamento de TI com Negócios**: Garante que a arquitetura de TI esteja alinhada com os objetivos e estratégias de negócios, promovendo uma abordagem integrada e coesa.
  
- **Redução de Custos e Aumento da Eficiência**: Ajuda a reduzir custos, evitar redundâncias e aumentar a eficiência operacional ao fornecer uma abordagem estruturada para o desenvolvimento da arquitetura.

- **Flexibilidade e Adaptabilidade**: Pode ser adaptado para atender às necessidades específicas de diferentes organizações e indústrias.

- **Melhoria da Governança**: Promove a governança eficaz da arquitetura, garantindo que as decisões sejam tomadas de forma informada e que as mudanças sejam gerenciadas de maneira controlada.

Exemplos de aplicação do TOGAF incluem:

- **Desenvolvimento de uma Arquitetura de Negócios**: Utilizando a Phase B do ADM para definir processos de negócios, capacidades e objetivos.
  
- **Implementação de uma Arquitetura de Dados**: Utilizando a Phase C do ADM para definir modelos de dados, fluxos de dados e requisitos de armazenamento.

- **Planejamento de Migração**: Utilizando a Phase F do ADM para criar um plano detalhado de migração para uma nova infraestrutura de TI.

O The Open Group oferece certificações TOGAF para profissionais de arquitetura empresarial, divididas em dois níveis:

- **TOGAF 9 Foundation (Level 1)**: Foco nos conceitos básicos e na terminologia do TOGAF.
- **TOGAF 9 Certified (Level 2)**: Foco na aplicação prática do TOGAF no desenvolvimento de arquiteturas empresariais.

O TOGAF é um framework poderoso e amplamente adotado que ajuda as organizações a alinhar a TI com os objetivos de negócios, melhorar a eficiência e gerenciar mudanças complexas de maneira eficaz. Para mais informações, visite o [site oficial do TOGAF](https://www.opengroup.org/togaf).

# IEEE: Institute of Electrical and Electronics Engineers

![IEEE](https://www.ieee.org/content/dam/ieee-org/ieee/web/org/globals/ieee_logo_140yrs.png)


O IEEE, ou Institute of Electrical and Electronics Engineers, é uma organização profissional dedicada ao avanço da tecnologia em benefício da humanidade. Fundada em 1884, o IEEE é a maior organização profissional técnica do mundo, com mais de 400.000 membros em mais de 160 países.

O IEEE é conhecido por desenvolver padrões técnicos que são amplamente adotados em diversas indústrias. Esses padrões ajudam a garantir a interoperabilidade, segurança e qualidade dos produtos e serviços tecnológicos.

## Principais Áreas de Atuação

- **Padrões Técnicos**: O IEEE é responsável por mais de 1.300 padrões ativos, abrangendo uma ampla gama de tecnologias, incluindo:
  - *IEEE 802.3*: Padrão para Ethernet, que define as características físicas e de controle de acesso ao meio para redes locais com fio.
  - *IEEE 802.11*: Padrão para redes sem fio (Wi-Fi), que define os protocolos para comunicação sem fio em redes locais.
  - *IEEE 1547*: Padrão para interconexão de recursos de energia distribuída com sistemas de energia elétrica.

- **Publicações e Conferências**: O IEEE publica cerca de um terço da literatura técnica mundial nas áreas de engenharia elétrica, eletrônica e ciência da computação. Além disso, organiza mais de 1.800 conferências anuais, proporcionando uma plataforma para a troca de conhecimento e inovação.

- **Educação e Certificação**: O IEEE oferece uma variedade de programas educacionais e certificações para ajudar profissionais a se manterem atualizados com as últimas inovações tecnológicas. Exemplos incluem:
  - *Certificação IEEE Wireless Communication*: Foco em tecnologias de comunicação sem fio.
  - *Certificação IEEE Software Development*: Foco em práticas e padrões de desenvolvimento de software.

- **Comunidades Técnicas**: O IEEE possui mais de 39 sociedades técnicas e conselhos que cobrem uma ampla gama de disciplinas tecnológicas, permitindo que membros se conectem e colaborem em áreas específicas de interesse.

## Benefícios do IEEE

- **Inovação Tecnológica**: O IEEE promove a inovação tecnológica através do desenvolvimento de padrões e da disseminação de conhecimento técnico.
  
- **Interoperabilidade**: Os padrões IEEE garantem que produtos e sistemas de diferentes fabricantes possam trabalhar juntos de forma eficaz e segura.

- **Segurança e Qualidade**: Os padrões IEEE ajudam a garantir a segurança e a qualidade dos produtos e serviços tecnológicos.

- **Desenvolvimento Profissional**: O IEEE oferece recursos educacionais e oportunidades de certificação para ajudar profissionais a avançarem em suas carreiras.

Exemplos de aplicação dos padrões IEEE incluem:

- **Redes Locais com Fio**: Implementação de redes Ethernet baseadas no padrão IEEE 802.3, utilizado em escritórios, data centers e ambientes industriais.
  
- **Redes Sem Fio**: Configuração de redes Wi-Fi baseadas no padrão IEEE 802.11, amplamente utilizado em residências, empresas e locais públicos.

- **Energia Renovável**: Interconexão de painéis solares e turbinas eólicas com a rede elétrica utilizando o padrão IEEE 1547.

Para mais informações, visite o [site oficial do IEEE](https://www.ieee.org).

# Prática (Supabase Self-Hosting com Docker🐋)

- Vamos seguir a documentação:

<a href="https://supabase.com/docs/guides/self-hosting/docker" target="blank_" class="btn btn-primary" style="width: 100%; margin: 10px;"><strong>Link para a Documentação Supabase 🕮</strong></a>


#### Vamos explorar o Supabase 🧠

- É neste local que iremos armazenar os dados de processamento

# Prática (ClickHouse como DataWareHouse)

<a href="https://clickhouse.com/docs/en/install" target="blank_" class="btn btn-primary" style="width: 100%; margin: 10px;"><strong>Link para a Documentação ClickHouse 🕮</strong></a>

<a href="https://hub.docker.com/r/clickhouse/clickhouse-server/" target="blank_" class="btn btn-primary" style="width: 100%; margin: 10px;"><strong>Imagem DockerHub 🐋</strong></a>

- Vamos instalar o DBeaver🦛 para visualizar os dados: [Link de Instalação](https://dbeaver.io/download/)

- Iniciar o ClickHouse via Powershell

```bash
docker run -d `
  --name clickhouse-server `
  --ulimit nofile=262144:262144 `
  -p 8123:8123 `
  -p 9000:9000 `
  -v C:\path\to\clickhouse\config:C:\etc\clickhouse-server\config.xml `
  -v C:\path\to\clickhouse\data:C:\var\lib\clickhouse `
  yandex/clickhouse-server
```

- Iniciar via Linux e OSX

```bash
docker run -d `
  --name clickhouse-server `
  --ulimit nofile=262144:262144 `
  -p 8123:8123 `
  -p 9000:9000 `
  yandex/clickhouse-server
```

## Teste de Comparação

### 1. Criação do `docker-compose.yml`

Aqui está o arquivo `docker-compose.yml` atualizado para incluir a configuração de senha para o ClickHouse:

```yaml
version: '3.8'

services:
  postgres:
    image: postgres:latest
    container_name: postgres
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: testdb
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data

  clickhouse:
    image: clickhouse/clickhouse-server:latest
    container_name: clickhouse
    environment:
      CLICKHOUSE_USER: user
      CLICKHOUSE_PASSWORD: password
      CLICKHOUSE_DB: testdb
    ports:
      - "8123:8123"
      - "9000:9000"
    volumes:
      - clickhouse_data:/var/lib/clickhouse

volumes:
  pgdata:
  clickhouse_data:
```

### 2. Inicialização dos Contêineres

Execute o comando abaixo para iniciar os contêineres:

```sh
docker-compose up -d
```

### 3. Criação das Tabelas e Inserção de Dados

#### PostgreSQL

Crie um arquivo chamado `postgres_setup.sql`:

```sql
-- Criação da tabela de teste
CREATE TABLE teste (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100),
    valor NUMERIC
);

-- Inserção de dados
INSERT INTO teste (nome, valor)
SELECT
    'Nome ' || generate_series(1, 1000000),
    random() * 100
FROM generate_series(1, 1000000);
```

Para executar este script dentro do contêiner PostgreSQL, utilize o comando:

```sh
docker exec -i postgres psql -U user -d testdb -f /path/to/postgres_setup.sql
```

#### ClickHouse

Crie um arquivo chamado `clickhouse_setup.sql`:

```sql
-- Criação da tabela de teste
CREATE TABLE teste (
    id UInt32,
    nome String,
    valor Float32
) ENGINE = MergeTree()
ORDER BY id;

-- Inserção de dados
INSERT INTO teste SELECT
    number AS id,
    concat('Nome ', toString(number)) AS nome,
    rand() % 100 AS valor
FROM numbers(1000000);
```

Para executar este script dentro do contêiner ClickHouse, utilize o comando:

```sh
docker exec -i clickhouse clickhouse-client --user user --password password --query="$(cat /path/to/clickhouse_setup.sql)"
```

### 4. Execução das Consultas de Leitura

#### PostgreSQL

```sql
\timing
SELECT * FROM teste WHERE valor > 50;
```

Para executar esta consulta dentro do contêiner PostgreSQL:

```sh
docker exec -it postgres psql -U user -d testdb -c "\timing" -c "SELECT * FROM teste WHERE valor > 50;"
```

#### ClickHouse

```sql
SELECT * FROM teste WHERE valor > 50;
```

Para executar esta consulta dentro do contêiner ClickHouse:

```sh
docker exec -it clickhouse clickhouse-client --user user --password password --query="SELECT * FROM teste WHERE valor > 50;"
```

### 5. Limpeza

Para remover as tabelas de teste após a execução dos testes:

#### PostgreSQL

```sql
DROP TABLE teste;
```

Para executar este comando dentro do contêiner PostgreSQL:

```sh
docker exec -it postgres psql -U user -d testdb -c "DROP TABLE teste;"
```

#### ClickHouse

```sql
DROP TABLE teste;
```

Para executar este comando dentro do contêiner ClickHouse:

```sh
docker exec -it clickhouse clickhouse-client --user user --password password --query="DROP TABLE teste;"
```

#### Arquitetura e Design

1. **Armazenamento em Colunas**:
   - **ClickHouse**: Utiliza uma arquitetura de armazenamento em colunas, o que significa que os dados são armazenados por coluna em vez de por linha. Isso permite uma leitura e compressão de dados muito mais eficiente, especialmente para consultas analíticas que acessam um subconjunto de colunas.
   - **PostgreSQL**: Utiliza uma arquitetura de armazenamento em linhas, o que é mais eficiente para operações transacionais (OLTP) onde a maioria das consultas acessa todas as colunas de uma linha específica.

2. **Compressão de Dados**:
   - **ClickHouse**: A compressão de dados em colunas é mais eficiente porque dados semelhantes são armazenados juntos, permitindo algoritmos de compressão mais eficazes.
   - **PostgreSQL**: Embora suporte compressão, a eficiência é menor devido ao armazenamento em linhas.

3. **Processamento em Modo Vetorial**:
   - **ClickHouse**: Utiliza processamento em modo vetorial, onde as operações são realizadas em blocos de dados ao invés de tuplas individuais, resultando em melhor utilização da CPU e maior throughput.
   - **PostgreSQL**: Processa dados em tuplas individuais, o que é menos eficiente para grandes volumes de dados.

#### Performance em Consultas

1. **Consultas Analíticas**:
   - **ClickHouse**: Projetado especificamente para consultas analíticas (OLAP), oferecendo desempenho superior em agregações, filtragens e cálculos em grandes conjuntos de dados.
   - **PostgreSQL**: Embora possa executar consultas analíticas, não é otimizado para tal e pode ser significativamente mais lento em comparação com ClickHouse.

2. **Indexação**:
   - **ClickHouse**: Utiliza índices primários baseados em ordenação e índices de dados em colunas, otimizados para leitura rápida.
   - **PostgreSQL**: Utiliza índices B-tree e outros tipos de índices que são mais versáteis, mas podem ser menos eficientes para consultas analíticas em grandes volumes de dados.

#### Trade-offs

1. **Transações e Consistência**:
   - **ClickHouse**: Não oferece suporte completo a transações ACID (Atomicidade, Consistência, Isolamento e Durabilidade). É otimizado para leituras rápidas e escritas em massa, mas pode não garantir a consistência em todas as operações.
   - **PostgreSQL**: Oferece suporte completo a transações ACID, sendo ideal para aplicações OLTP onde a consistência e a integridade dos dados são cruciais.

2. **Flexibilidade e Funcionalidades**:
   - **ClickHouse**: Focado em consultas analíticas, pode não oferecer todas as funcionalidades avançadas de um banco de dados relacional completo, como suporte a joins complexos, triggers e stored procedures.
   - **PostgreSQL**: Extremamente versátil, oferece uma ampla gama de funcionalidades, incluindo suporte a joins complexos, triggers, stored procedures, e extensões como PostGIS para dados geoespaciais.

3. **Escritas e Atualizações**:
   - **ClickHouse**: Otimizado para leituras rápidas, mas as operações de escrita e atualização podem ser menos eficientes. Não é ideal para cargas de trabalho que envolvem muitas atualizações frequentes de dados.
   - **PostgreSQL**: Melhor equilibrado para operações de leitura e escrita, sendo adequado tanto para OLTP quanto para OLAP, embora não seja tão rápido quanto ClickHouse para grandes consultas analíticas.

4. **Ecossistema e Suporte**:
   - **ClickHouse**: Comunidade em crescimento, mas ainda mais recente em comparação com PostgreSQL. Pode haver menos ferramentas e bibliotecas disponíveis.
   - **PostgreSQL**: Ecossistema maduro com uma vasta gama de ferramentas, bibliotecas e suporte comunitário e comercial.


### Introdução ao Parquet

![cloudinary](https://res.cloudinary.com/dyhjjms8y/image/upload/v1723124171/Captura_de_tela_2024-08-08_103536_ekp0vn.png)

**Parquet** é um formato de armazenamento de dados em colunas desenvolvido para o ecossistema Hadoop. É projetado para ser altamente eficiente tanto em termos de espaço quanto de desempenho, especialmente para grandes volumes de dados. Ele é amplamente utilizado em ambientes de Big Data devido à sua capacidade de suportar leitura e escrita eficientes.

### Introdução ao CSV

**CSV (Comma-Separated Values)** é um formato de arquivo simples e amplamente utilizado para armazenar dados tabulares em texto plano. Cada linha do arquivo representa um registro e cada campo é separado por uma vírgula (ou outro delimitador, como ponto e vírgula).

### Comparação: Parquet vs. CSV

#### Estrutura de Armazenamento

- **Parquet**:
  - **Armazenamento em Colunas**: Os dados são armazenados por coluna, o que permite uma leitura e compressão mais eficiente, especialmente para consultas que acessam um subconjunto de colunas.
  - **Metadados**: Inclui metadados ricos que descrevem o esquema dos dados, tipos de dados e outras informações úteis.

- **CSV**:
  - **Armazenamento em Linhas**: Os dados são armazenados por linha, o que é simples e direto, mas menos eficiente para grandes volumes de dados e consultas que acessam apenas algumas colunas.
  - **Metadados**: Não possui metadados embutidos. O esquema dos dados deve ser inferido ou fornecido separadamente.

#### Desempenho

- **Parquet**:
  - **Leitura e Escrita**: Muito eficiente para leitura de grandes volumes de dados, especialmente quando apenas algumas colunas são necessárias. A escrita pode ser mais lenta devido à compressão e ao armazenamento em colunas.
  - **Compressão**: Suporta compressão eficiente de dados, reduzindo significativamente o espaço de armazenamento necessário.
  - **Consultas Analíticas**: Excelente desempenho para consultas analíticas devido ao armazenamento em colunas.

- **CSV**:
  - **Leitura e Escrita**: Leitura e escrita simples e rápidas, mas pode ser ineficiente para grandes volumes de dados.
  - **Compressão**: Não suporta compressão nativamente. Pode ser comprimido usando ferramentas externas (por exemplo, gzip), mas isso não é tão eficiente quanto a compressão nativa do Parquet.
  - **Consultas Analíticas**: Desempenho inferior para consultas analíticas em grandes volumes de dados devido ao armazenamento em linhas.

#### Flexibilidade e Usabilidade

- **Parquet**:
  - **Complexidade**: Mais complexo de usar e configurar devido à necessidade de bibliotecas específicas para leitura e escrita.
  - **Compatibilidade**: Amplamente suportado em ferramentas de Big Data, como Apache Spark, Apache Hive, e Apache Drill.

- **CSV**:
  - **Simplicidade**: Muito simples de usar e entender. Pode ser aberto e editado com qualquer editor de texto ou planilha.
  - **Compatibilidade**: Suportado por praticamente todas as ferramentas de software, desde simples editores de texto até sistemas de banco de dados e ferramentas de análise de dados.

#### Casos de Uso

- **Parquet**:
  - Ideal para grandes volumes de dados e cargas de trabalho analíticas.
  - Usado em ambientes de Big Data onde a eficiência de armazenamento e desempenho de leitura são críticos.

- **CSV**:
  - Adequado para pequenos a médios volumes de dados.
  - Ideal para intercâmbio de dados entre sistemas e para uso em ferramentas que não suportam formatos de dados mais complexos.
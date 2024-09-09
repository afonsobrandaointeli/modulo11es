# Data Lakes e Data Warehouses

Bem-vindo(a) à aula de hoje, onde vamos explorar conceitos importantes relacionados a **bancos de dados**, **data warehouses** e **data lakes**. Estes componentes desempenham papéis fundamentais em sistemas modernos de armazenamento e análise de dados. Vamos entender suas diferenças e como cada um pode ser utilizado de forma eficiente.

---

|Autoestudo|Link|
|----------|----|
|Databases Vs Data Warehouses Vs Data Lakes - What Is The Difference And Why Should You Care?|[Link](https://youtu.be/FxpRL0m9BcA?feature=shared)
|Qual é a diferença entre um data warehouse, um data lake e um data mart?|[Link](https://aws.amazon.com/pt/compare/the-difference-between-a-data-warehouse-data-lake-and-data-mart/)

---

<iframe src="https://docs.google.com/presentation/d/1NqZKIvlY6KzL8OWAD_Ggzf-XI5xpwasg/embed?start=false&loop=false&delayms=3000" frameborder="0" width="800" height="486" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

# Bancos de Dados (Databases)

Os **bancos de dados** são frequentemente usados para armazenar e gerenciar dados transacionais, comumente em sistemas **OLTP (Online Transaction Processing)**. Bancos de dados tradicionais incluem MySQL, PostgreSQL, Oracle e Microsoft SQL Server. Eles geralmente seguem o modelo de **armazenamento baseado em linhas (row-based storage)**, ideal para operações CRUD (Create, Read, Update, Delete), como:

- **Criação** de registros
- **Leitura** de dados específicos
- **Atualização** de registros existentes
- **Exclusão** de dados

### Características Principais

- **Eficiência nas operações transacionais**: sistemas transacionais como o backend do Facebook ainda utilizam bancos de dados tradicionais como MySQL para operações em grande escala.
- **Limitações para análises**: embora seja possível realizar análises diretamente em bancos de dados, isso pode ser ineficiente e até arriscado, pois pode afetar a performance de sistemas que lidam com transações.

---

# Data Warehouses

Os **Data Warehouses (Armazéns de Dados)** surgem como solução para análises históricas e complexas de dados. Diferente dos bancos de dados OLTP, os data warehouses são voltados para o processamento analítico **OLAP (Online Analytical Processing)**.

### Definição

De acordo com **Bill Inman**, considerado o "pai" do data warehouse, um data warehouse é uma **coleção orientada a assuntos, integrada, variante no tempo e não volátil de dados,** usada para dar suporte à tomada de decisões gerenciais.

### Principais Vantagens

- **Armazenamento de dados históricos**: permitem manter registros detalhados ao longo do tempo, essenciais para análises temporais.
- **Integração de dados**: combinam dados de diversas fontes (ex.: Salesforce, sistemas internos) em um único repositório.
- **Estrutura em estrela ou floco de neve**: são frequentemente organizados em esquemas estruturados para otimizar consultas analíticas.

---

# Data Lakes

Os **Data Lakes** surgiram como uma solução mais flexível para lidar com grandes volumes de dados não estruturados ou semi-estruturados. Eles são amplamente utilizados em projetos de **ciência de dados** e **machine learning**.

### Características Principais

- **Flexibilidade no armazenamento**: permitem armazenar dados em qualquer formato (ex.: JSON, Parquet, CSV), o que os torna mais flexíveis que os data warehouses.
- **Schema on Read**: o esquema é aplicado durante a leitura dos dados, oferecendo maior flexibilidade em comparação aos data warehouses.
- **Uso em análises exploratórias**: data lakes são ideais para análises exploratórias antes de os dados serem movidos para um data warehouse para produção.

### Casos de Uso

- **Ciência de dados e machine learning**: oferecem o ambiente ideal para análises exploratórias.
- **Processamento de dados em tempo real**: permite relatórios operacionais rápidos, sem a necessidade de aguardar longos processos de ETL.

---

# Diferenças Entre Data Warehouses e Data Lakes

| Aspecto               | Data Warehouse                     | Data Lake                             |
|-----------------------|------------------------------------|---------------------------------------|
| **Estrutura**          | Altamente estruturado (Esquemas)   | Menos estruturado (armazenamento flexível) |
| **Uso**                | Relatórios e decisões gerenciais   | Análise exploratória, machine learning |
| **Armazenamento**      | Armazenamento em colunas ou linhas | Arquivos (JSON, Parquet, etc.)        |
| **Histórico de Dados** | Mantém dados históricos            | Pode ou não armazenar histórico       |

---

# Exemplo no Google Colab

Vamos criar um exemplo simples de DataMart utilizando Python no Colab, onde teremos tanto um **Data Warehouse** quanto um **DataMart**. Para isso, utilizaremos o pandas para simular a criação de tabelas e a manipulação de dados. Segue o passo a passo:

### 1. Criação do Data Warehouse
Um **Data Warehouse** é um repositório de dados integrados de diversas fontes. Vamos simular a criação de um Data Warehouse com tabelas de exemplo para vendas, clientes e produtos.

### 2. Criação do DataMart
Um **DataMart** é uma parte do Data Warehouse focada em um assunto específico. Vamos criar um DataMart de vendas, que conterá apenas os dados relevantes para a análise de vendas.

Aqui está o código completo para criar um Data Warehouse e um DataMart usando pandas no Colab:

```python
# Importando as bibliotecas necessárias
import pandas as pd

# Criando o Data Warehouse (DW)
# Tabela de Clientes
clientes = pd.DataFrame({
    'cliente_id': [1, 2, 3, 4],
    'nome': ['João', 'Maria', 'Pedro', 'Ana'],
    'cidade': ['São Paulo', 'Rio de Janeiro', 'Belo Horizonte', 'Curitiba']
})

# Tabela de Produtos
produtos = pd.DataFrame({
    'produto_id': [101, 102, 103, 104],
    'produto_nome': ['Notebook', 'Smartphone', 'Tablet', 'Smartwatch'],
    'preco': [3500, 1500, 2000, 1200]
})

# Tabela de Vendas
vendas = pd.DataFrame({
    'venda_id': [1001, 1002, 1003, 1004],
    'cliente_id': [1, 2, 3, 4],
    'produto_id': [101, 102, 103, 104],
    'quantidade': [1, 2, 1, 3],
    'data_venda': ['2024-09-01', '2024-09-02', '2024-09-03', '2024-09-04']
})

# Exibindo o Data Warehouse
print("Tabela de Clientes:")
print(clientes)
print("\nTabela de Produtos:")
print(produtos)
print("\nTabela de Vendas:")
print(vendas)

# Criando o DataMart de Vendas
# Juntando as tabelas para criar um DataMart de Vendas
data_mart_vendas = vendas.merge(clientes, on='cliente_id').merge(produtos, on='produto_id')

# Selecionando apenas colunas relevantes para o DataMart de Vendas
data_mart_vendas = data_mart_vendas[['venda_id', 'nome', 'produto_nome', 'quantidade', 'preco', 'data_venda']]

# Exibindo o DataMart de Vendas
print("\nDataMart de Vendas:")
print(data_mart_vendas)

# Criando uma coluna de valor total (quantidade * preço)
data_mart_vendas['valor_total'] = data_mart_vendas['quantidade'] * data_mart_vendas['preco']

# Exibindo o DataMart com o valor total
print("\nDataMart de Vendas com Valor Total:")
print(data_mart_vendas)
```

### Explicação:
1. **Data Warehouse**: Temos três tabelas principais (clientes, produtos e vendas).
2. **DataMart**: Criamos um DataMart focado em vendas, que contém informações de clientes, produtos e vendas, com uma coluna adicional de valor total (quantidade * preço).

Você pode rodar esse código no Google Colab para simular um pequeno exemplo de Data Warehouse e DataMart.

Se precisar de mais detalhes ou uma abordagem mais avançada, posso ajudar a expandir o exemplo!

# Ponderada

## Criação de Dashboard de Telemetria do Data Lake e do Data Warehouse

## Comando:
Criar um **dashboard de telemetria** para monitorar a utilização do **Data Lake** e do **Data Warehouse**. O Data Lake, que pode estar em buckets ou banco de dados, já deve estar implementado, e o dashboard deve medir a utilização desses recursos. O dashboard deve ser discutido em sala de aula.

## Critérios de Avaliação:

1. **Compreensão dos Dados (25%)**: O aluno deve identificar corretamente os principais elementos a serem utilizados, demonstrando uma compreensão abrangente dos dados.
2. **Seleção de Métricas Relevantes (20%)**: O aluno deve escolher as métricas relevantes para as necessidades de monitoramento e os objetivos da telemetria.
3. **Eficiência na Integração de Dados (25%)**: O aluno deve integrar os dados de forma eficiente, criando uma visão unificada e sólida, levando em conta as diferentes fontes.
4. **Design e Usabilidade do Dashboard (20%)**: O aluno deve criar um design atraente, funcional, organizado e com uma experiência de usuário intuitiva e eficaz.
5. **Análise e Interpretação dos Resultados (10%)**: O aluno deve apresentar uma análise sólida dos dados, destacando tendências e padrões, fornecendo insights valiosos para a tomada de decisões.

## Pontuação Total: **100 pontos**

---

# Barema de Qualidade

### 1. Compreensão dos Dados (25%)

- **Avançado (9,1 - 10)**: Compreensão abrangente dos dados, incluindo detalhes relevantes para a telemetria.
- **Intermediário (7,1 - 9)**: Compreensão sólida dos dados, identificando corretamente os principais elementos.
- **Básico (4,1 - 7)**: Compreensão básica, mas com lacunas significativas na interpretação dos dados.
- **Insuficiente (0 - 4)**: Falta de compreensão dos dados presentes no Data Lake e no Data Warehouse.

### 2. Seleção de Métricas Relevantes (20%)

- **Avançado (9,1 - 10)**: Seleção excelente de métricas, alinhadas de maneira precisa aos objetivos de telemetria.
- **Intermediário (7,1 - 9)**: Escolha sólida de métricas relevantes, demonstrando compreensão das necessidades de monitoramento.
- **Básico (4,1 - 7)**: Seleção básica de métricas, mas com falta de abordagem crítica.
- **Insuficiente (0 - 4)**: Escolha inadequada ou ausência de métricas relevantes para a telemetria.

### 3. Eficiência na Integração de Dados (25%)

- **Avançado (9,1 - 10)**: Integração eficiente dos dados, proporcionando uma visão unificada e consistente.
- **Intermediário (7,1 - 9)**: Integração sólida dos dados, considerando fontes do Data Lake e do Data Warehouse.
- **Básico (4,1 - 7)**: Integração básica, mas com erros substanciais ou falta de coerência.
- **Insuficiente (0 - 4)**: Implementação inexistente ou com sérios problemas na integração dos dados.

### 4. Design e Usabilidade do Dashboard (20%)

- **Avançado (9,1 - 10)**: Excelente design, proporcionando uma experiência de usuário intuitiva e eficaz.
- **Intermediário (7,1 - 9)**: Design atraente e funcional, facilitando a compreensão das métricas apresentadas.
- **Básico (4,1 - 7)**: Design básico, com alguns elementos confusos ou desorganizados.
- **Insuficiente (0 - 4)**: Design inadequado, dificultando a interpretação das informações.

### 5. Análise e Interpretação dos Resultados (10%)

- **Avançado (9,1 - 10)**: Análise excepcional, oferecendo insights valiosos para a tomada de decisões.
- **Intermediário (7,1 - 9)**: Análise sólida, destacando tendências e padrões relevantes.
- **Básico (4,1 - 7)**: Análise básica, com falta de profundidade ou insights significativos.
- **Insuficiente (0 - 4)**: Falha na análise ou interpretação dos resultados apresentados.

## Pontuação Total: **100%**



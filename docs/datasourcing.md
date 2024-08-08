#  Data Sourcing e Data Analysis com R Studio

## Autoestudos

| Nome                                                                               | Tipo                 |
|------------------------------------------------------------------------------------|----------------------|
| [Notebook de Datasourcing](https://r4ds.had.co.nz/exploratory-data-analysis.html)  | Documentação         |
| [Exploratory Data Analysis in R Programming](https://www.geeksforgeeks.org/exploratory-data-analysis-in-r-programming/) | Documentação  |

---

# Slides

<iframe src="https://docs.google.com/presentation/d/1y0cVhWmuc8Y5KpPol9FG3mHzZ3GWiHB7/embed?start=false&loop=false&delayms=3000" frameborder="0" width="700" height="500" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>


# Introdução à Linguagem R

## O que é R?

R é uma linguagem de programação e um ambiente de software livre para computação estatística e gráficos. Foi desenvolvido por Ross Ihaka e Robert Gentleman na Universidade de Auckland, Nova Zelândia, e é amplamente utilizado por estatísticos e analistas de dados para desenvolver software estatístico e realizar análise de dados.

## Características Principais

- **Interativa**: R é uma linguagem interpretada, o que significa que você pode executar comandos um de cada vez e ver os resultados imediatamente.
- **Extensível**: Há uma vasta quantidade de pacotes adicionais disponíveis que podem ser instalados para estender a funcionalidade do R.
- **Gráficos de Alta Qualidade**: R possui ferramentas poderosas para a criação de gráficos de alta qualidade e visualizações de dados.
- **Comunidade Ativa**: A comunidade R é grande e ativa, oferecendo suporte e recursos através de fóruns, blogs, e documentação.

## Estrutura Básica da Linguagem

### Objetos e Variáveis

R é uma linguagem orientada a objetos, e quase tudo em R é um objeto. Você pode criar variáveis para armazenar dados e manipular esses dados usando várias funções.

```r
# Atribuição de valores a variáveis
x <- 10
y <- 5

# Operações aritméticas
z <- x + y
print(z)  # Saída: 15
```

### Tipos de Dados

R suporta vários tipos de dados básicos, incluindo:

- **Números**: inteiros e números de ponto flutuante.
- **Caracteres**: strings.
- **Vetores**: uma sequência de dados do mesmo tipo.
- **Matrizes**: uma coleção bidimensional de dados.
- **Data Frames**: uma tabela de dados, onde cada coluna pode conter diferentes tipos de dados.
- **Listas**: uma coleção de objetos que podem ser de tipos diferentes.

```r
# Exemplos de tipos de dados
num <- 42
char <- "Olá, mundo!"
vetor <- c(1, 2, 3, 4, 5)
matriz <- matrix(1:9, nrow = 3)
df <- data.frame(Nomes = c("Ana", "Pedro"), Idades = c(28, 34))
lista <- list(num, char, vetor, matriz, df)
```

### Funções

Funções são uma parte essencial de R e permitem encapsular código que pode ser reutilizado. Você pode usar funções integradas ou criar suas próprias funções.

```r
# Função simples para somar dois números
soma <- function(a, b) {
  return(a + b)
}

resultado <- soma(3, 4)
print(resultado)  # Saída: 7
```

### Controle de Fluxo

R suporta estruturas de controle de fluxo, como condicionais (`if`, `else`) e loops (`for`, `while`).

```r
# Condicional if-else
if (x > y) {
  print("x é maior que y")
} else {
  print("x não é maior que y")
}

# Loop for
for (i in 1:5) {
  print(i)
}
```

## Importação e Manipulação de Dados

### Importação de Dados

R facilita a importação de dados de várias fontes, como arquivos CSV, Excel, bancos de dados e APIs.

```r
# Importar dados de um arquivo CSV
dados <- read.csv("dados.csv")

# Visualizar as primeiras linhas do data frame
head(dados)
```

### Manipulação de Dados

A manipulação de dados em R pode ser realizada usando pacotes como `dplyr` e `tidyr`.

```r
# Carregar o pacote dplyr
library(dplyr)

# Selecionar colunas e filtrar linhas
dados_filtrados <- dados %>%
  select(Nome, Idade) %>%
  filter(Idade > 30)
```

## Visualização de Dados

R possui pacotes poderosos para visualização de dados, como `ggplot2`.

```r
# Carregar o pacote ggplot2
library(ggplot2)

# Criar um gráfico de dispersão
ggplot(dados, aes(x = Idade, y = Salario)) +
  geom_point() +
  theme_minimal() +
  labs(title = "Idade vs. Salário", x = "Idade", y = "Salário")
```

## Pacotes e Extensões

Uma das grandes vantagens de R é a sua extensibilidade através de pacotes. Você pode instalar pacotes do CRAN (Comprehensive R Archive Network) para adicionar novas funcionalidades ao R.

```r
# Instalar e carregar um pacote
install.packages("tidyverse")
library(tidyverse)
```

# Análise Exploratória Avançada com R

## Pré-requisitos

- Conhecimento básico de R e RStudio
- Conhecimento básico de EDA

## Conteúdo da Aula

1. [Preparação do Ambiente](#preparação-do-ambiente)
2. [Importação e Limpeza de Dados](#importação-e-limpeza-de-dados)
3. [Análise Univariada](#análise-univariada)
4. [Análise Bivariada](#análise-bivariada)
5. [Análise Multivariada](#análise-multivariada)
6. [Visualização Avançada](#visualização-avançada)
7. [Estatísticas Avançadas](#estatísticas-avançadas)

## Preparação do Ambiente

Para começar, precisamos preparar nosso ambiente de trabalho instalando e carregando os pacotes necessários.

```r
# Instalar pacotes necessários
install.packages(c("tidyverse", "data.table", "GGally", "corrplot", "gridExtra"))

# Carregar pacotes
library(tidyverse)
library(data.table)
library(GGally)
library(corrplot)
library(gridExtra)
```

## Importação e Limpeza de Dados

Nesta seção, vamos importar nossos dados e realizar a limpeza necessária.

```r
# Importar dados
data <- fread("path/to/your/data.csv")

# Exibir as primeiras linhas dos dados
head(data)

# Verificar dados faltantes
sum(is.na(data))

# Limpeza de dados (exemplo: remover linhas com dados faltantes)
data <- na.omit(data)
```

## Análise Univariada

A análise univariada envolve a descrição de cada variável individualmente.

```r
# Distribuição de uma variável numérica
ggplot(data, aes(x = variable)) +
  geom_histogram(binwidth = 10, fill = "blue", color = "black") +
  theme_minimal() +
  labs(title = "Distribuição de Variable", x = "Variable", y = "Frequência")

# Medidas de tendência central e dispersão
summary(data$variable)
```

## Análise Bivariada

A análise bivariada examina a relação entre duas variáveis.

```r
# Scatter plot para duas variáveis numéricas
ggplot(data, aes(x = variable1, y = variable2)) +
  geom_point() +
  theme_minimal() +
  labs(title = "Relação entre Variable1 e Variable2", x = "Variable1", y = "Variable2")

# Boxplot para uma variável categórica e uma numérica
ggplot(data, aes(x = categorical_variable, y = numeric_variable)) +
  geom_boxplot() +
  theme_minimal() +
  labs(title = "Boxplot de Categorical Variable e Numeric Variable", x = "Categorical Variable", y = "Numeric Variable")
```

## Análise Multivariada

A análise multivariada considera múltiplas variáveis simultaneamente.

```r
# Matriz de correlação
cor_matrix <- cor(data %>% select_if(is.numeric))
corrplot(cor_matrix, method = "circle")

# Scatterplot matrix
ggpairs(data %>% select_if(is.numeric))
```

## Visualização Avançada

Vamos explorar técnicas avançadas de visualização para EDA.

```r
# Densidade 2D para grandes conjuntos de dados
ggplot(data, aes(x = variable1, y = variable2)) +
  geom_bin2d() +
  scale_fill_gradient(low = "white", high = "blue") +
  theme_minimal() +
  labs(title = "Densidade 2D de Variable1 e Variable2", x = "Variable1", y = "Variable2")

# Facet wrap para visualização de subgrupos
ggplot(data, aes(x = variable)) +
  geom_histogram(binwidth = 10, fill = "blue", color = "black") +
  facet_wrap(~ categorical_variable) +
  theme_minimal() +
  labs(title = "Distribuição de Variable por Categoria", x = "Variable", y = "Frequência")
```

## Estatísticas Avançadas

Utilizaremos técnicas estatísticas avançadas para aprofundar nossa análise.

```r
# Regressão linear simples
model <- lm(variable2 ~ variable1, data = data)
summary(model)

# Análise de componentes principais (PCA)
pca <- prcomp(data %>% select_if(is.numeric), scale = TRUE)
summary(pca)

# Visualização dos componentes principais
autoplot(pca, data = data, colour = 'categorical_variable')
```

# Por que Fazer Análise Exploratória Avançada com R em Dados Grandes?

## Introdução

A análise exploratória de dados (EDA) é um passo fundamental no processo de análise de dados. Quando se trata de grandes volumes de dados, a importância de uma EDA avançada se torna ainda mais crucial. A linguagem R é uma das ferramentas mais poderosas e versáteis disponíveis para realizar EDA em grandes conjuntos de dados. Aqui estão alguns motivos pelos quais você deve considerar fazer análise exploratória avançada com R em dados grandes.

## 1. Ferramentas Poderosas de Manipulação de Dados

### **`dplyr` e `data.table`**

R oferece pacotes como `dplyr` e `data.table` que são otimizados para manipulação de dados rápida e eficiente, mesmo com conjuntos de dados grandes. Eles permitem realizar operações complexas de transformação de dados com uma sintaxe simples e intuitiva.

```r
# Exemplo de manipulação de dados com dplyr
library(dplyr)
dados_grandes %>%
  filter(salario > 50000) %>%
  group_by(departamento) %>%
  summarise(media_salario = mean(salario, na.rm = TRUE))
```

## 2. Visualização de Dados Escalável

### **`ggplot2` e `plotly`**

A visualização é uma parte essencial da EDA. R, com pacotes como `ggplot2` e `plotly`, permite criar visualizações detalhadas e interativas que podem lidar com grandes volumes de dados. Estas visualizações ajudam a identificar padrões, tendências e anomalias que não são facilmente visíveis em tabelas de dados.

```r
# Exemplo de visualização com ggplot2
library(ggplot2)
ggplot(dados_grandes, aes(x = idade, y = salario)) +
  geom_point(alpha = 0.5) +
  theme_minimal() +
  labs(title = "Relação entre Idade e Salário")
```

## 3. Suporte para Computação Paralela

### **`parallel` e `future`**

Para conjuntos de dados muito grandes, a computação paralela pode acelerar significativamente o processamento. R possui suporte nativo para computação paralela através de pacotes como `parallel` e `future`, permitindo distribuir tarefas em múltiplos núcleos de CPU.

```r
# Exemplo de computação paralela com future
library(future)
plan(multisession, workers = 4)
resultados <- future_lapply(1:10, function(x) sum(rnorm(1e6)))
```

## 4. Integração com Big Data

### **`sparklyr` e `DBI`**

R pode se integrar facilmente com tecnologias de Big Data como Apache Spark através do pacote `sparklyr`, e também com bancos de dados SQL através do pacote `DBI`. Isso permite que você realize EDA em dados armazenados em sistemas distribuídos ou em bancos de dados de grande escala.

### Exemplo de Integração com Spark usando Docker

#### Passo 1: Configurar o Ambiente Docker

Crie um arquivo `docker-compose.yml` para configurar um cluster Spark com Hadoop.

```yaml
version: '3.7'

services:
  spark-master:
    image: bde2020/spark-master:latest
    container_name: spark-master
    ports:
      - "8080:8080"
      - "7077:7077"
    environment:
      - INIT_DAEMON_STEP=setup_spark
    networks:
      - spark

  spark-worker-1:
    image: bde2020/spark-worker:latest
    container_name: spark-worker-1
    depends_on:
      - spark-master
    environment:
      - "SPARK_MASTER=spark://spark-master:7077"
      - INIT_DAEMON_STEP=setup_worker
    networks:
      - spark

networks:
  spark:
    driver: bridge
```

#### Passo 2: Iniciar o Cluster Spark

Inicie o cluster Spark usando Docker Compose.

```sh
docker-compose up -d
```

#### Passo 3: Conectar ao Spark no R

Utilize o pacote `sparklyr` para conectar ao cluster Spark.

```r
# Instalar e carregar pacotes necessários
install.packages("sparklyr")
library(sparklyr)

# Conectar ao cluster Spark
sc <- spark_connect(master = "spark://localhost:7077")

# Copiar dados para o Spark
dados_spark <- copy_to(sc, dados_grandes, "dados_grandes_tbl")

# Realizar operações no Spark
dados_spark %>%
  filter(salario > 50000) %>%
  group_by(departamento) %>%
  summarise(media_salario = mean(salario, na.rm = TRUE)) %>%
  collect()
```

#### Passo 4: Desconectar do Spark

Após a análise, desconecte do cluster Spark.

```r
spark_disconnect(sc)
```

## 5. Capacidades Estatísticas Avançadas

### **`caret` e `mlr`**

R é amplamente reconhecido por suas capacidades estatísticas e de machine learning. Pacotes como `caret` e `mlr` permitem realizar análises estatísticas avançadas e aplicar algoritmos de machine learning para descobrir insights profundos em grandes volumes de dados.

```r
# Exemplo de análise com caret
library(caret)
modelo <- train(salario ~ ., data = dados_grandes, method = "lm")
print(modelo)
```

## Conclusão

Nesta aula, exploramos técnicas avançadas de Análise Exploratória de Dados (EDA) usando R. Aprendemos a preparar o ambiente, importar e limpar dados, realizar análises univariadas, bivariadas e multivariadas, criar visualizações avançadas e aplicar estatísticas avançadas. Com essas habilidades, você estará bem equipado para realizar EDA de maneira eficaz e profunda.

## Referências

- [Notebook de Datasourcing](https://r4ds.had.co.nz/exploratory-data-analysis.html)
- [Exploratory Data Analysis in R Programming](https://www.geeksforgeeks.org/exploratory-data-analysis-in-r-programming/)
- [R for Data Science](https://r4ds.had.co.nz/)
- [The Comprehensive R Archive Network (CRAN)](https://cran.r-project.org/)
- [R Documentation](https://www.rdocumentation.org/)
- [R for Data Science](https://r4ds.had.co.nz/)
- [Data Manipulation with dplyr](https://cran.r-project.org/web/packages/dplyr/dplyr.pdf)
- [Efficient R programming with data.table](https://cran.r-project.org/web/packages/data.table/data.table.pdf)
- [ggplot2: Elegant Graphics for Data Analysis](https://ggplot2.tidyverse.org/)
- [Apache Spark Integration with R](https://spark.rstudio.com/)

# Mão na Massa! - Análise Exploratória de Dados com o Conjunto de Dados Wine

## Introdução

O conjunto de dados de vinhos [wine](https://archive.ics.uci.edu/dataset/186/wine+quality) é amplamente utilizado para demonstrações de técnicas de análise de dados e machine learning. Ele contém informações químicas sobre diferentes tipos de vinhos e a qualidade atribuída a cada um. Neste tutorial, vamos realizar uma Análise Exploratória de Dados (EDA) completa utilizando a linguagem R.

## Passo 1: Preparação do Ambiente

Primeiro, vamos preparar nosso ambiente de trabalho, instalando e carregando os pacotes necessários.

```r
# Instalar pacotes necessários
install.packages(c("tidyverse", "GGally", "corrplot", "gridExtra"))

# Carregar pacotes
library(tidyverse)
library(GGally)
library(corrplot)
library(gridExtra)
```

## Passo 2: Carregar os Dados

Vamos carregar o conjunto de dados `wine`. Supondo que o arquivo esteja em formato CSV, usaremos a função `read.csv`.

```r
# Carregar os dados
wine_data <- read.csv("path/to/wine.csv")

# Exibir as primeiras linhas do data frame
head(wine_data)
```

## Passo 3: Entender a Estrutura dos Dados

Examinaremos a estrutura dos dados para entender suas características básicas.

```r
# Estrutura dos dados
str(wine_data)

# Resumo estatístico das variáveis
summary(wine_data)
```

## Passo 4: Verificar Dados Faltantes

Verificaremos se há dados faltantes no conjunto de dados.

```r
# Verificar dados faltantes
sum(is.na(wine_data))
```

## Passo 5: Análise Univariada

Realizaremos a análise de cada variável individualmente.

### Distribuição da Qualidade do Vinho

```r
# Histograma da variável 'quality'
ggplot(wine_data, aes(x = quality)) +
  geom_histogram(binwidth = 1, fill = "blue", color = "black") +
  theme_minimal() +
  labs(title = "Distribuição da Qualidade do Vinho", x = "Qualidade", y = "Frequência")
```

### Distribuição de Variáveis Numéricas

```r
# Histograma para cada variável numérica
numeric_vars <- wine_data %>% select(-quality)
p <- lapply(names(numeric_vars), function(var) {
  ggplot(wine_data, aes_string(x = var)) +
    geom_histogram(fill = "blue", color = "black", bins = 30) +
    theme_minimal() +
    labs(title = paste("Distribuição de", var), x = var, y = "Frequência")
})
grid.arrange(grobs = p, ncol = 3)
```

## Passo 6: Análise Bivariada

Examinaremos as relações entre pares de variáveis.

### Relação entre Álcool e Qualidade

```r
# Scatter plot entre 'alcohol' e 'quality'
ggplot(wine_data, aes(x = alcohol, y = quality)) +
  geom_point(alpha = 0.5) +
  theme_minimal() +
  labs(title = "Relação entre Álcool e Qualidade", x = "Álcool", y = "Qualidade")
```

### Boxplot da Qualidade por Tipo de Vinho

```r
# Supondo que há uma coluna 'type' indicando o tipo de vinho
ggplot(wine_data, aes(x = factor(quality), y = alcohol, fill = factor(quality))) +
  geom_boxplot() +
  theme_minimal() +
  labs(title = "Boxplot da Qualidade por Tipo de Vinho", x = "Qualidade", y = "Álcool")
```

## Passo 7: Análise Multivariada

Analisaremos múltiplas variáveis simultaneamente.

### Matriz de Correlação

```r
# Matriz de correlação
cor_matrix <- cor(wine_data %>% select_if(is.numeric))
corrplot(cor_matrix, method = "circle")
```

### Scatterplot Matrix

```r
# Scatterplot matrix
ggpairs(wine_data %>% select_if(is.numeric))
```

## Passo 8: Conclusões e Insights

Após a análise, resumimos nossos principais achados:

- A distribuição da qualidade dos vinhos é...
- A relação entre o teor de álcool e a qualidade é...
- Variáveis como ácido cítrico e pH apresentam correlação...

## Referências

- [Documentação do ggplot2](https://ggplot2.tidyverse.org/)
- [Guia de Introdução ao dplyr](https://dplyr.tidyverse.org/)


## Qual a Missão para o Artefato?

Os grupos deverão realizar uma Análise Exploratória Avançada nos dados que foram fornecidos. Esta análise deve incluir, mas não se limitar a:

- Entender a estrutura dos dados e suas características básicas.
- Realizar uma análise univariada de todas as variáveis.
- Explorar relações bivariadas entre variáveis para identificar possíveis correlações.
- Conduzir uma análise multivariada para entender interações complexas entre variáveis.
- Utilizar visualizações para ilustrar as descobertas e insights obtidos.

### Uso de Computação Distribuída com Spark

Caso o conjunto de dados seja muito extenso e torne o processamento em um único computador inviável, os grupos deverão utilizar o Apache Spark como solução de computação distribuída. O Spark permite manipular e processar grandes volumes de dados de maneira eficiente, distribuindo as tarefas em múltiplos nós de computação.

Utilizem essas ferramentas e técnicas para garantir que a análise seja completa e eficiente, mesmo com conjuntos de dados volumosos. O objetivo final é extrair insights valiosos dos dados fornecidos e apresentar esses insights de forma clara e compreensível.

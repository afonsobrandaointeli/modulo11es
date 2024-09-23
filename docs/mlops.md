# Ciclo de Vida e Automatização de Pipeline de Dados (MLOps)

## Autoestudos

|Autoestudo|Link|
|----------|----|
|O ciclo de vida de um projeto de dados|[Link](https://www.programaria.org/o-ciclo-de-vida-de-um-projeto-de-dados/)|
|Notebook de Como gerenciar o ciclo de vida com MLFlow e Prefect|[Link](https://colab.research.google.com/drive/1F8-QykLhfrpXG2sWirQ0I2kjzt2pHN_Y?usp=sharing)|


---
<iframe src="https://docs.google.com/presentation/d/1oasmXTFCoRoSq-Rt97y-8nSJt7IdNwow/embed?start=false&loop=false&delayms=3000" frameborder="0" width="768" height="461" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>
---

## Data Lifecycle

![imagem](https://youngdestinya.ng/wp-content/uploads/2024/07/data-lifecycle-management.jpg)

![imagem](https://datamanagement.hms.harvard.edu/sites/default/files/assets/Images/RDM-lifecycle-2tier-v5.png)

## Pydantic e sua importância no Data Lifecycle

### Explicação do Pydantic e sua Importância no Ciclo de Vida dos Dados

**Pydantic** é uma biblioteca Python utilizada para modelagem e validação de dados com base em tipos de dados nativos. Ele permite a criação de classes baseadas em modelos que podem validar automaticamente a entrada de dados, assegurando que estejam em conformidade com os tipos esperados. O Pydantic também facilita a conversão de dados entre diferentes formatos, como objetos Python e JSON, com validação rigorosa.

#### **Por que o Pydantic é Importante no Ciclo de Vida dos Dados?**

No **Ciclo de Vida dos Dados**, os dados passam por diversas etapas — coleta, armazenamento, processamento, análise, e visualização. Garantir que esses dados sejam corretos e estejam no formato adequado é crucial para a eficácia de todo o processo. O Pydantic desempenha um papel central em duas dessas etapas: **processamento/validação** e **análise**. Aqui estão os motivos pelos quais o Pydantic é fundamental:

**Validação Automática e Eficiente:**

   - Durante o ciclo de vida dos dados, eles podem ser provenientes de várias fontes (APIs, bancos de dados, arquivos). Cada fonte pode ter diferentes formatos e tipos de dados. O Pydantic permite validar esses dados automaticamente, garantindo que eles estejam corretos antes de serem processados ou armazenados.
   - Exemplo: Se um campo `preco` deve ser um número positivo, o Pydantic valida automaticamente se os dados atendem a essa regra, impedindo que valores incorretos passem adiante.

**Conversão entre Formatos de Dados:**

   - O Pydantic facilita a conversão de dados entre diferentes representações, como converter dados de JSON para objetos Python ou de uma consulta de banco de dados para um formato utilizável em APIs. Isso é particularmente importante para o intercâmbio de dados entre diferentes sistemas.
   - Exemplo: Se uma API retorna dados em formato JSON, o Pydantic pode transformar automaticamente esses dados em um objeto Python validado, pronto para ser manipulado.

**Garantia de Qualidade de Dados:**

   - Um dos grandes desafios no ciclo de vida dos dados é garantir a qualidade dos dados. Isso envolve assegurar que os dados estão completos, no formato correto e sem inconsistências. Com o Pydantic, você pode definir regras de validação robustas, que garantem que apenas dados limpos e corretos avancem nas etapas subsequentes do ciclo.
   - Exemplo: Um campo como `email` pode ser validado para verificar se tem um formato correto de e-mail. Se o dado estiver incorreto, o Pydantic levantará um erro antes que o dado seja processado.

**Facilidade de Integração com Bancos de Dados e APIs:**

   - O Pydantic possui um modo especial para trabalhar com ORMs (Object-Relational Mappers), como SQLAlchemy, permitindo validar os dados diretamente extraídos de um banco de dados. Isso ajuda a integrar a validação de dados com sistemas de armazenamento e APIs, mantendo a consistência.
   - Exemplo: Dados extraídos de um banco de dados podem ser validados em tempo real antes de serem usados em análises ou exibidos em visualizações.

**Documentação e Manutenção de Código Simples:**

   - O Pydantic utiliza anotações de tipo, o que facilita a leitura e manutenção do código. Quando as regras de validação estão claramente definidas em um modelo Pydantic, outros desenvolvedores ou analistas podem entender rapidamente quais dados são esperados e quais são as regras de validação.
   - Exemplo: O modelo Pydantic de um "Produto" define os tipos de dados e suas restrições, tornando explícito que `preco` deve ser positivo e que `estoque` deve ser um número inteiro.

#### **Ciclo de Vida dos Dados e a Validação com Pydantic**

No contexto do ciclo de vida dos dados, o Pydantic pode ser utilizado em diferentes momentos:

- **Coleta/Extração:** Os dados brutos são extraídos de fontes diversas. O Pydantic valida esses dados imediatamente, corrigindo erros antes que avancem no ciclo.
- **Processamento/Validação:** Os dados validados com Pydantic podem ser transformados e preparados para uso posterior. Isso garante que os dados armazenados ou analisados são de alta qualidade.
- **Análise/Visualização:** Quando os dados chegam a essa fase, eles já foram validados e estão prontos para análises complexas, o que minimiza erros nas visualizações e decisões de negócios baseadas nesses dados.

---

## Mão na Massa com Colab

Neste notebook, vamos explorar o **Ciclo de Vida dos Dados** usando **SQLite**, **Pydantic** para validação, **Pytest** para TDD, e **Plotly** para visualização de dados. Todo o processo será simulado em um ambiente SQLite, que será criado e preenchido automaticamente.

### **Passo 1: Configuração Inicial**

No Colab, você pode instalar as dependências diretamente usando o seguinte código:

```python
!pip install sqlalchemy pydantic pytest plotly
```

### **Passo 2: Configurando o Banco de Dados SQLite**

Aqui, vamos criar um banco de dados SQLite em memória e preenchê-lo com dados de exemplo.

```python
import sqlite3
from sqlalchemy import create_engine, Column, Integer, String, Float
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

# Criação do banco de dados SQLite
DATABASE_URL = "sqlite:///produtos.db"
engine = create_engine(DATABASE_URL)

# Criando a base do SQLAlchemy
Base = declarative_base()

# Definindo a tabela "produtos"
class Produto(Base):
    __tablename__ = 'produtos'

    id = Column(Integer, primary_key=True, index=True)
    nome = Column(String, nullable=False)
    preco = Column(Float, nullable=False)
    estoque = Column(Integer, nullable=False)

# Criando a tabela no banco de dados
Base.metadata.create_all(engine)

# Criando a sessão
Session = sessionmaker(bind=engine)
session = Session()

# Preenchendo o banco de dados com dados automáticos
def preencher_dados():
    produtos = [
        Produto(nome="Caneta", preco=1.50, estoque=100),
        Produto(nome="Lápis", preco=0.99, estoque=200),
        Produto(nome="Borracha", preco=0.75, estoque=150),
        Produto(nome="Caderno", preco=15.00, estoque=75),
        Produto(nome="Mochila", preco=50.00, estoque=20)
    ]
    session.bulk_save_objects(produtos)
    session.commit()

# Preenchendo os dados
preencher_dados()

# Verificando se os dados foram inseridos
produtos = session.query(Produto).all()
for produto in produtos:
    print(f"ID: {produto.id}, Nome: {produto.nome}, Preço: {produto.preco}, Estoque: {produto.estoque}")
```

### **Passo 3: Validação dos Dados com Pydantic**

Agora, vamos definir um modelo Pydantic para validar os dados que extraímos do banco de dados.

```python
from pydantic import BaseModel, constr, conint, confloat

# Definindo o modelo Pydantic para validação
class ProdutoModel(BaseModel):
    id: int
    nome: constr(min_length=1)
    preco: confloat(gt=0)
    estoque: conint(ge=0)

    class Config:
        orm_mode = True

# Função para validar os produtos
def validar_produtos(produtos):
    return [ProdutoModel.from_orm(produto) for produto in produtos]

# Validação dos produtos extraídos
produtos_validados = validar_produtos(produtos)
for produto in produtos_validados:
    print(produto.json())
```

### **Passo 4: TDD com Pytest**

Embora o Pytest seja mais utilizado fora do ambiente Colab, podemos simular os testes de validação diretamente no notebook.

```python
import pytest
from pydantic import ValidationError

# Função de teste para produto válido
def test_produto_valido():
    dados = {"id": 1, "nome": "Caneta", "preco": 1.50, "estoque": 100}
    produto = ProdutoModel(**dados)
    assert produto.nome == "Caneta"
    assert produto.preco == 1.50

# Função de teste para nome inválido
def test_nome_invalido():
    dados = {"id": 2, "nome": "", "preco": 2.99, "estoque": 50}
    try:
        ProdutoModel(**dados)
    except ValidationError as e:
        print(e)

# Função de teste para preço negativo
def test_preco_negativo():
    dados = {"id": 3, "nome": "Borracha", "preco": -1.0, "estoque": 20}
    try:
        ProdutoModel(**dados)
    except ValidationError as e:
        print(e)

# Executando os testes
test_produto_valido()
test_nome_invalido()
test_preco_negativo()
```

### **Passo 5: Visualizando os Dados com Plotly**

Agora, vamos usar o **Plotly** para visualizar os dados. Primeiro, criaremos um gráfico de barras que mostra o estoque de cada produto.

```python
import plotly.graph_objects as go

# Criando gráfico de barras para o estoque
def grafico_estoque(produtos):
    nomes = [produto.nome for produto in produtos]
    estoques = [produto.estoque for produto in produtos]
    
    fig = go.Figure([go.Bar(x=nomes, y=estoques)])
    fig.update_layout(title="Estoque de Produtos", xaxis_title="Produto", yaxis_title="Quantidade em Estoque")
    fig.show()

# Exibindo o gráfico de estoque
grafico_estoque(produtos_validados)
```

Também podemos criar um gráfico de pizza para visualizar a distribuição de preços dos produtos.

```python
# Criando gráfico de pizza para distribuição de preços
def grafico_precos(produtos):
    nomes = [produto.nome for produto in produtos]
    precos = [produto.preco for produto in produtos]
    
    fig = go.Figure(data=[go.Pie(labels=nomes, values=precos, hole=0.3)])
    fig.update_layout(title="Distribuição de Preços")
    fig.show()

# Exibindo o gráfico de preços
grafico_precos(produtos_validados)
```

### **Passo 6: Integração Completa**

Agora, vamos combinar todas as etapas em um único fluxo: extrair, validar e visualizar os dados.

```python
def ciclo_de_vida_completo():
    # Extração dos produtos do banco
    produtos_brutos = session.query(Produto).all()
    
    # Validação dos produtos
    produtos_validados = validar_produtos(produtos_brutos)
    
    # Visualizações
    grafico_estoque(produtos_validados)
    grafico_precos(produtos_validados)

# Executando o ciclo de vida completo
ciclo_de_vida_completo()
```
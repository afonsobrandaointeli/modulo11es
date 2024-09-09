# Serviços e ETLs para Transformação de Dados e Processamento de Dados em Escala (train at scale)

|Autoestudo|Link|
|----------|----|
|Como você pode dimensionar processos de ETL para grandes volumes de dados em engenharia de banco de dados?|[Link](https://www.linkedin.com/advice/0/how-can-you-scale-etl-processes-large-data)|
|Refatoração para Padrões|[Link](https://integrada.minhabiblioteca.com.br/reader/books/9788577803033/pageid/47)|


# Aula 100% Prática!

Faça a instalação dos pacotes:

```bash
pip install prefect mlflow pandas scikit-learn xgboost
```

Depois estruturamos o projeto da seguinte forma:

```text
pipeline_voos/
│
├── data/
│   └── voos.csv
│
├── src/
│   ├── __init__.py
│   ├── preprocess.py
│   ├── train.py
│   └── evaluate.py
│
└── main.py
```

Agora implementamos o src/preprocess.py

```python
import pandas as pd
from prefect import task

@task
def carregar_dados(caminho: str):
    return pd.read_csv(caminho)

@task
def preprocessar_dados(df: pd.DataFrame):
    # Simplificado para o exemplo
    df['atraso'] = (df['atraso_chegada'] > 15).astype(int)
    features = ['dia_semana', 'mes', 'distancia']
    X = df[features]
    y = df['atraso']
    return X, y
```

Depois o src/evaluate.py

```python
from sklearn.metrics import accuracy_score, precision_score, recall_score
from prefect import task
import mlflow

@task
def avaliar_modelo(modelo, X_test, y_test):
    y_pred = modelo.predict(X_test)
    
    accuracy = accuracy_score(y_test, y_pred)
    precision = precision_score(y_test, y_pred)
    recall = recall_score(y_test, y_pred)
    
    mlflow.log_metric("accuracy", accuracy)
    mlflow.log_metric("precision", precision)
    mlflow.log_metric("recall", recall)
    
    return accuracy, precision, recall
```

Por final, dentro do módulo, o train.py

```python
from sklearn.model_selection import train_test_split
from xgboost import XGBClassifier
from prefect import task
import mlflow

@task
def treinar_modelo(X, y):
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)
    
    with mlflow.start_run():
        modelo = XGBClassifier()
        modelo.fit(X_train, y_train)
        
        mlflow.log_param("model", "XGBClassifier")
        mlflow.sklearn.log_model(modelo, "modelo")
        
        return modelo, X_test, y_test
```

Crie um voos.csv com este conteúdo:

```csv
id,data,dia_semana,mes,origem,destino,companhia,horario_partida,horario_chegada,distancia,atraso_chegada
1,2024-09-10,2,9,GRU,CGH,LATAM,08:00,09:00,30,0
2,2024-09-10,2,9,CGH,BSB,GOL,10:30,12:30,870,20
3,2024-09-10,2,9,GIG,SSA,AZUL,14:00,16:15,1200,5
4,2024-09-11,3,9,FOR,REC,LATAM,07:45,09:00,630,0
5,2024-09-11,3,9,BSB,GRU,GOL,11:15,13:00,870,30
6,2024-09-12,4,9,CGH,GIG,AZUL,16:30,17:45,360,10
7,2024-09-12,4,9,SSA,FOR,LATAM,09:00,11:00,1000,0
8,2024-09-13,5,9,REC,BSB,GOL,13:45,16:15,1650,45
9,2024-09-13,5,9,GRU,FOR,AZUL,22:00,01:30,2350,15
10,2024-09-14,6,9,GIG,SSA,LATAM,06:30,08:45,1200,0
```

e o main.py na pasta raiz:

```python
from prefect import flow
from prefect.server.schemas.schedules import CronSchedule
from src.preprocess import carregar_dados, preprocessar_dados
from src.train import treinar_modelo
from src.evaluate import avaliar_modelo
import mlflow

@flow
def pipeline_voos():
    mlflow.set_tracking_uri("http://localhost:5000")
    mlflow.set_experiment("previsao_atrasos_voos")
    
    dados = carregar_dados("data/voos.csv")
    X, y = preprocessar_dados(dados)
    modelo, X_test, y_test = treinar_modelo(X, y)
    accuracy, precision, recall = avaliar_modelo(modelo, X_test, y_test)
    
    print(f"Accuracy: {accuracy}")
    print(f"Precision: {precision}")
    print(f"Recall: {recall}")

if __name__ == "__main__":
    pipeline_voos()
    
    # Criar e aplicar o deployment
    pipeline_voos.serve(
        name="pipeline_voos_local",
        schedule=CronSchedule(cron="0 0 * * *", timezone="America/Sao_Paulo"),
        work_queue_name="local"
    )

    print("Deployment criado com sucesso. Inicie o servidor Prefect e um agente para executar o fluxo.")
```

Agora vamos rodar o mlflow:

```bash
mlflow server --backend-store-uri sqlite:///mlflow.db --default-artifact-root ./mlflow-artifacts --host 0.0.0.0
```

E depois o prefect com:

```bash
prefect server start
```

Finalmente o python main com:

```bash
python main.py
```

Agora analisaremos o que aconteceu!

# Mais uma Ponderada!

## Desafio: Criação de uma ETL

O aluno deverá criar, com seu grupo, uma **ETL** para transformar os dados **RAW** no **Data Lake** em dados **WORK**, para serem absorvidos no sistema de banco de dados relacional.

## Critérios de Avaliação

1. **Eficiência na Extração, Transformação e Carga (ETL) (30%)**: 
   - O aluno deve fazer uma implementação sólida e eficiente da ETL, levando em conta os requisitos de transformação dos dados **RAW** para os dados de trabalho (**WORK**).

2. **Integração com o Sistema de Banco de Dados Relacional (25%)**: 
   - O aluno deve integrar a implementação de forma adequada com o modelo de dados, garantindo a absorção correta dos dados.

3. **Organização e Clareza do Código (20%)**: 
   - O código deve ser claro, organizado de forma lógica e seguir boas práticas de programação.

4. **Documentação e Comentários (15%)**: 
   - O código deve conter comentários que permitam sua completa compreensão.

**Pontuação Total**: 100%


|DICA|
|----|
|Cada aluno deve escolher um csv ou parquete criar a etl com extract jsons para mandar para a camada working ;)|
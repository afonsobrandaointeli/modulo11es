# Ingestão e Processamento de Dados

<p style="text-align: justify;">Esta instrução foca em estratégias e metodologias essenciais para a ingestão de dados em plataformas analíticas. Discutiremos as melhores práticas para a coleta eficiente de dados de diversas fontes, a importância de pipelines de dados confiáveis e como otimizar a ingestão para análises em tempo real. Os alunos aprenderão sobre as tecnologias e ferramentas atuais que facilitam o processo de ingestão, garantindo a qualidade e a disponibilidade dos dados para processamento subsequente e análise. Serão feitos scripts com testes integrados.</p>

|Autoestudo|Link|Pontuação
|---------------------------|----|----|
|Pacote de Ingestão de Dados|[Acesse](https://colab.research.google.com/drive/1LJDhsksOxlcf6srx7QIsHAGxu1hGJe5m?usp=sharing)| 3 pontos|
|Consultas complexas em SQL|[Acesse](https://integrada.minhabiblioteca.com.br/reader/books/9786556900186/pageid/118)| 0 pontos |

# Agenda

|Atividade|Tempo|
|------|---|
|Demonstração Prática do Pacote de Ingestão|60m|
|Ponderada em Sala de Aula|60m|

# Demonstração Prática de Um Pacote Python

## Pré-requisitos

- Conhecimento básico em Python e Docker.
- Instalação do Docker e Docker Compose.
- Instalação do Poetry.

## Estrutura da Aula

1. Criar o Pacote Poetry
2. Configurar o Docker Compose com MinIO e ClickHouse
3. Coletar Dados de uma API Aberta
4. Armazenar Dados Brutos no MinIO
5. Criar um Módulo de ETL Simples
6. Visualizar Dados no ClickHouse com DBeaver

### Criando o Pacote

```bash
poetry new data_pipeline
cd data_pipeline
```

### Pyproject.toml

```bash
cd data_pipeline
poetry add flask requests pandas pyarrow minio clickhouse-connect
```

### Configurar o Docker Compose com MinIO e ClickHouse

```yml
version: '3.8'

services:
  minio:
    image: minio/minio
    container_name: minio
    ports:
      - "9000:9000"
    environment:
      MINIO_ROOT_USER: minioadmin
      MINIO_ROOT_PASSWORD: minioadmin
    command: server /data

  clickhouse:
    image: yandex/clickhouse-server
    container_name: clickhouse
    ports:
      - "8123:8123"
```

```bash
docker-compose up -d
```

## Vamos testar o Mini.IO

```python
from minio_test import Minio
from minio.error import S3Error

def test_minio():
    # Configuração do cliente MinIO
    client = Minio(
        "localhost:9000",  # Endereço do MinIO
        access_key="minioadmin",  # Chave de acesso
        secret_key="minioadmin",  # Chave secreta
        secure=False  # Use True se estiver usando HTTPS
    )

    bucket_name = "test-bucket"
    object_name = "test.txt"
    file_content = "Este é um arquivo de teste."

    try:
        # Criar bucket se não existir
        if not client.bucket_exists(bucket_name):
            client.make_bucket(bucket_name)
            print(f"Bucket '{bucket_name}' criado com sucesso.")
        else:
            print(f"Bucket '{bucket_name}' já existe.")

        # Criar um arquivo de teste
        with open(object_name, "w") as file:
            file.write(file_content)

        # Fazer upload do arquivo para o MinIO
        client.fput_object(bucket_name, object_name, object_name)
        print(f"Arquivo '{object_name}' enviado com sucesso para o bucket '{bucket_name}'.")

        # Fazer download do arquivo do MinIO
        client.fget_object(bucket_name, object_name, f"downloaded_{object_name}")
        print(f"Arquivo '{object_name}' baixado com sucesso do bucket '{bucket_name}'.")

        # Ler o conteúdo do arquivo baixado
        with open(f"downloaded_{object_name}", "r") as file:
            downloaded_content = file.read()
            print(f"Conteúdo do arquivo baixado: {downloaded_content}")

    except S3Error as e:
        print(f"Erro ao interagir com o MinIO: {e}")

if __name__ == "__main__":
    test_minio()
```

## SQL para cração da tabela!

```sql
CREATE TABLE IF NOT EXISTS working_data (
    data_ingestao DateTime,
    dado_linha String,
    tag String
) ENGINE = MergeTree()
ORDER BY data_ingestao;
```

## Flask para Armazenamento de Dados

```python
from flask import Flask, request, jsonify
from minio import Minio
import pandas as pd
import pyarrow as pa
import pyarrow.parquet as pq
from datetime import datetime
import clickhouse_connect

app = Flask(__name__)

# Configuração do cliente MinIO
minio_client = Minio(
    "localhost:9000",
    access_key="minioadmin",
    secret_key="minioadmin",
    secure=False
)

# Criar bucket se não existir
if not minio_client.bucket_exists("raw-data"):
    minio_client.make_bucket("raw-data")

# Função para executar o script SQL
def execute_sql_script():
    client = clickhouse_connect.get_client(host='localhost', port=8123)
    with open('sql/init_db.sql', 'r') as file:
        sql_script = file.read()
    client.command(sql_script)

@app.route('/data', methods=['POST'])
def receive_data():
    data = request.get_json()
    if not data or 'date' not in data or 'dados' not in data:
        return jsonify({"error": "Formato de dados inválido"}), 400

    try:
        datetime.fromtimestamp(data['date'])
        int(data['dados'])
    except (ValueError, TypeError):
        return jsonify({"error": "Tipo de dados inválido"}), 400

    # Criar DataFrame e salvar como Parquet
    df = pd.DataFrame([data])
    filename = f"raw_data_{datetime.now().strftime('%Y%m%d%H%M%S')}.parquet"
    table = pa.Table.from_pandas(df)
    pq.write_table(table, filename)

    # Fazer upload para o MinIO
    minio_client.fput_object("raw-data", filename, filename)

    # Ler arquivo Parquet do MinIO
    minio_client.fget_object("raw-data", filename, f"downloaded_{filename}")
    df_parquet = pd.read_parquet(f"downloaded_{filename}")

    # Inserir dados no ClickHouse
    client = clickhouse_connect.get_client(host='localhost', port=8123)
    df_parquet['data_ingestao'] = datetime.now()
    df_parquet['dado_linha'] = df_parquet.apply(lambda row: row.to_json(), axis=1)
    df_parquet['tag'] = 'example_tag'

    client.insert_df('working_data', df_parquet[['data_ingestao', 'dado_linha', 'tag']])

    return jsonify({"message": "Dados recebidos, armazenados e processados com sucesso"}), 200

if __name__ == '__main__':
    execute_sql_script()
    app.run(host='0.0.0.0', port=5000)
```

## Vamos testar com requests.http

```http
POST http://localhost:5000/data
Content-Type: application/json

{
    "date": 1691836800,
    "dados": 42
}
```

## Este é um pacote de demonstração: seu grupo pode e deve criar uma arquitetura própria com Testes!

# Tarefa

<p>Fazer em sala de aula a Ponderada!</p>
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


### Criando o Pacote

```bash
poetry new data_pipeline
```

### Pyproject.toml

```bash
cd data_pipeline
poetry add flask requests pandas pyarrow minio clickhouse-connect python-dotenv
```

### Configurar o Docker Compose com MinIO e ClickHouse

```yml
version: '3.8'

services:
  minio:
    image: minio/minio:latest
    container_name: minio
    ports:
      - "9000:9000"   # Porta para a API
      - "9001:9001"   # Porta para a Web UI
    environment:
      MINIO_ROOT_USER: minioadmin
      MINIO_ROOT_PASSWORD: minioadmin
    volumes:
      - minio_data:/data  # Persistência de dados
    command: server /data --console-address ":9001"
    restart: always

  clickhouse:
    image: yandex/clickhouse-server:latest
    container_name: clickhouse
    ports:
      - "8123:8123"  # Porta para a HTTP interface
    volumes:
      - clickhouse_data:/var/lib/clickhouse  # Persistência de dados
    restart: always

volumes:
  minio_data:
    driver: local
  clickhouse_data:
    driver: local

```

```bash
docker-compose up --build
```

## Vamos testar o Mini.IO

```python
from minio import Minio
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

Crie uma pasta `sql/` e o arquivo `create_table.sql` com o código:

```sql
CREATE TABLE IF NOT EXISTS working_data (
    data_ingestao DateTime,
    dado_linha String,
    tag String
) ENGINE = MergeTree()
ORDER BY data_ingestao;
```

## Aplicativo Pipe de Dados

Dentro da pasta `data_pipeline` crie os arquivos:

`clickhouse_client.py`

```python
import clickhouse_connect
import os
from dotenv import load_dotenv

load_dotenv()

# Configuração do cliente ClickHouse
CLICKHOUSE_HOST = os.getenv('CLICKHOUSE_HOST')
CLICKHOUSE_PORT = os.getenv('CLICKHOUSE_PORT')

def get_client():
    return clickhouse_connect.get_client(host=CLICKHOUSE_HOST, port=CLICKHOUSE_PORT)

def execute_sql_script(script_path):
    client = get_client()
    with open(script_path, 'r') as file:
        sql_script = file.read()
    client.command(sql_script)
    return client

def insert_dataframe(client, table_name, df):
    client.insert_df(table_name, df)
```

`data_processing.py`

```python
import pandas as pd
import pyarrow as pa
import pyarrow.parquet as pq
from datetime import datetime

def process_data(data):
    # Criar DataFrame e salvar como Parquet
    df = pd.DataFrame([data])
    filename = f"raw_data_{datetime.now().strftime('%Y%m%d%H%M%S')}.parquet"
    table = pa.Table.from_pandas(df)
    pq.write_table(table, filename)
    return filename

def prepare_dataframe_for_insert(df):
    df['data_ingestao'] = datetime.now()
    df['dado_linha'] = df.apply(lambda row: row.to_json(), axis=1)
    df['tag'] = 'example_tag'
    return df[['data_ingestao', 'dado_linha', 'tag']]
```

`minio_client.py`

```python

```


e na pasta raiz o `app.py`

```python
from minio import Minio
import os
from dotenv import load_dotenv

load_dotenv()

# Carregar variáveis de ambiente
MINIO_ENDPOINT = os.getenv('MINIO_ENDPOINT')
MINIO_ACCESS_KEY = os.getenv('MINIO_ACCESS_KEY')
MINIO_SECRET_KEY = os.getenv('MINIO_SECRET_KEY')

# Configuração do cliente MinIO
minio_client = Minio(
    MINIO_ENDPOINT,
    access_key=MINIO_ACCESS_KEY,
    secret_key=MINIO_SECRET_KEY,
    secure=False
)

def create_bucket_if_not_exists(bucket_name):
    if not minio_client.bucket_exists(bucket_name):
        minio_client.make_bucket(bucket_name)

def upload_file(bucket_name, file_path):
    file_name = os.path.basename(file_path)
    minio_client.fput_object(bucket_name, file_name, file_path)

def download_file(bucket_name, file_name, local_file_path):
    minio_client.fget_object(bucket_name, file_name, local_file_path)
```

e o `.env`

```text
MINIO_ENDPOINT=localhost:9000
MINIO_ACCESS_KEY=minioadmin
MINIO_SECRET_KEY=minioadmin

CLICKHOUSE_HOST=localhost
CLICKHOUSE_PORT=8123
```

## Vamos testar com requests.http

```http
POST http://localhost:5000/data
Content-Type: application/json

{
    "date": 1692345600,
    "dados": 12345
}
```

## Agora criamos a VIEW:

```sql
CREATE VIEW IF NOT EXISTS working_data_view AS
SELECT
    data_ingestao,
    JSONExtractInt(dado_linha, 'date') AS date_unix,
    JSONExtractInt(dado_linha, 'dados') AS dados,
    toDateTime(JSONExtractInt(dado_linha, 'data_ingestao') / 1000) AS data_ingestao_datetime
FROM working_data;
```

## Este é um pacote de demonstração: seu grupo pode e deve criar uma arquitetura própria com Testes!

# Tarefa

<p><strong>Fazer em sala de aula a Ponderada!</strong></p>
# lab1
exercicio 1 lab 1

Instruções para Executar o Projeto
Passo 1: Preparar o Ambiente
Coloque o arquivo amazon-meta.txt dentro da pasta scripts.
Passo 2: Iniciar o Container
Na pasta principal do projeto, inicie os containers com o comando:

sh
Copiar código
docker-compose up -d
O arquivo entrypoint.sh dará a sequência de compilação dos scripts Python.

Se tudo correr bem, as pastas mongodb, postgre e pokemon serão criadas. (A pasta pokemon pode demorar alguns minutos para ser baixada).

Passo 3: Fechar os Containers
Para parar os containers que não estão sendo usados, execute:
sh
Copiar código
docker-compose down
Passo 4: Compilar o Docker Dentro da Pasta scripts
Entre no terminal na pasta scripts e compile o Docker com o comando:
sh
Copiar código
docker-compose up --build
Passo 5: Executar o Spark
Abra outro terminal e entre no terminal do container Spark com o comando:

sh
Copiar código
docker exec -it trabalho2bd-python-1 /bin/bash
Dentro do container, compile o script AvroScript.py com o comando:

sh
Copiar código
spark-submit --packages org.apache.spark:spark-avro_2.12:3.4.1 /app/scripts/AvroScript.py
Para criar as respostas, compile o comando:

sh
Copiar código
spark-submit --packages org.apache.spark:spark-avro_2.12:3.4.1 /app/scripts/AvroResult.py
As respostas serão guardadas na rota /app/scripts/ingestao/resultado.

Descrição de Cada Script
Script.py: Responsável pela inserção e geração dos arquivos JSON para o MongoDB.
SavePostJson.py: Responsável por pegar os arquivos Post e transformá-los em JSON.
PostScript.py: Responsável pela leitura e inserção dos elementos Amazon no PostgreSQL.
PokeScript.py: Responsável por salvar os dados Pokémon em JSON.
entrypoint.sh: Arquivo Bash que compila os arquivos Python na ordem correta.
AvroScript.py: Transforma JSON em Avro.
AvroResult.py: Gera o resultado dentro da pasta ingestao dos arquivos Avro.
Comandos Adicionais
Para entrar novamente no container Python, use:

sh
Copiar código
docker exec -it trabalho2bd-python-1 /bin/bash
Para entrar no container Spark e executar os scripts, use:

sh
Copiar código
docker exec -it scripts-spark-1 /bin/bash
spark-submit --packages org.apache.spark:spark-avro_2.12:3.4.0 /app/scripts/AvroScript.py
spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.3.0 /app/scripts/AvroScript.py
spark-submit --packages org.apache.spark:spark-avro_2.12:3.4.1 /app/scripts/AvroScript.py

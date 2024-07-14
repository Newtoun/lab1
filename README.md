# lab1
exercicio 1 lab 1

<h1>Instruções para Executar o Projeto</h1>

<h2>Passo 1: Preparar o Ambiente</h2>
<ol>
    <li>Coloque o arquivo <code>amazon-meta.txt</code> dentro da pasta <code>scripts</code>.</li>
</ol>

<h2>Passo 2: Iniciar o Container</h2>
<ol>
    <li>Na pasta principal do projeto, inicie os containers com o comando:
        <pre><code>docker-compose up -d</code></pre>
    </li>
    <li>O arquivo <code>entrypoint.sh</code> dará a sequência de compilação dos scripts Python.</li>
    <li>Se tudo correr bem, as pastas <code>mongodb</code>, <code>postgre</code> e <code>pokemon</code> serão criadas. (A pasta <code>pokemon</code> pode demorar alguns minutos para ser baixada).</li>
</ol>

<h2>Passo 3: Fechar os Containers</h2>
<ol>
    <li>Para parar os containers que não estão sendo usados, execute:
        <pre><code>docker-compose down</code></pre>
    </li>
</ol>

<h2>Passo 4: Compilar o Docker Dentro da Pasta <code>scripts</code></h2>
<ol>
    <li>Entre no terminal na pasta <code>scripts</code> e compile o Docker com o comando:
        <pre><code>docker-compose up --build</code></pre>
    </li>
</ol>

<h2>Passo 5: Executar o Spark</h2>
<ol>
    <li>Abra outro terminal e entre no terminal do container Spark com o comando:
        <pre><code>docker exec -it trabalho2bd-python-1 /bin/bash</code></pre>
    </li>
    <li>Dentro do container, compile o script <code>AvroScript.py</code> com o comando:
        <pre><code>spark-submit --packages org.apache.spark:spark-avro_2.12:3.4.1 /app/scripts/AvroScript.py</code></pre>
    </li>
    <li>Para criar as respostas, compile o comando:
        <pre><code>spark-submit --packages org.apache.spark:spark-avro_2.12:3.4.1 /app/scripts/AvroResult.py</code></pre>
        As respostas serão guardadas na rota <code>/app/scripts/ingestao/resultado</code>.
    </li>
</ol>

<h2>Descrição de Cada Script</h2>
<ul>
    <li><code>Script.py</code>: Responsável pela inserção e geração dos arquivos JSON para o MongoDB.</li>
    <li><code>SavePostJson.py</code>: Responsável por pegar os arquivos Post e transformá-los em JSON.</li>
    <li><code>PostScript.py</code>: Responsável pela leitura e inserção dos elementos Amazon no PostgreSQL.</li>
    <li><code>PokeScript.py</code>: Responsável por salvar os dados Pokémon em JSON.</li>
    <li><code>entrypoint.sh</code>: Arquivo Bash que compila os arquivos Python na ordem correta.</li>
    <li><code>AvroScript.py</code>: Transforma JSON em Avro.</li>
    <li><code>AvroResult.py</code>: Gera o resultado dentro da pasta <code>ingestao</code> dos arquivos Avro.</li>
</ul>

<h2>Comandos Adicionais</h2>
<ol>
    <li>Para entrar novamente no container Python, use:
        <pre><code>docker exec -it trabalho2bd-python-1 /bin/bash</code></pre>
    </li>
    <li>Para entrar no container Spark e executar os scripts, use:
        <pre><code>docker exec -it scripts-spark-1 /bin/bash
spark-submit --packages org.apache.spark:spark-avro_2.12:3.4.0 /app/scripts/AvroScript.py
spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.3.0 /app/scripts/AvroScript.py
spark-submit --packages org.apache.spark:spark-avro_2.12:3.4.1 /app/scripts/AvroScript.py</code></pre>
    </li>
</ol>

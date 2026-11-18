# RASI_GabrielRizzo_CJ3034216
Trabalho de Redes e Administração de Sistemas (RASI) - Docker e Docker Compose. Aluno: Gabriel Rizzo dos Santos. Turma: 2º Informática. Nota: 10. 


---


A partir de agora, começa o tutorial para realizar todos os passos do trabalho, fiz um bem explicativo para que todos (ou nem todos) pudessem entender.

### 1. INTRODUÇÃO

Neste trabalho, desenvolvemos uma aplicação web utilizando Python, Flask, Docker e MySQL. O objetivo foi compreender como configurar um ambiente Linux, acessar uma máquina virtual remotamente, criar uma aplicação web, construir imagens e contêineres Docker e, por fim, integrar diferentes serviços utilizando Docker Compose.

O desenvolvimento foi dividido em cinco etapas principais:

1. Configuração da conexão SSH com a máquina virtual.
2. Instalação e verificação do Docker.
3. Criação da aplicação utilizando Flask.
4. Construção da imagem e execução do contêiner.
5. Integração do Flask com MySQL e Apache utilizando Docker Compose.

---

## 2. CONFIGURAÇÃO DA MÁQUINA VIRTUAL E CONEXÃO SSH

### 2.1. Preparação da máquina virtual

Inicialmente, foi necessário possuir uma máquina virtual configurada. Neste trabalho, utilizamos o Ubuntu de 64 bits.

A máquina virtual permite executar um sistema operacional dentro do computador, sem precisar substituir o sistema principal.

Para facilitar a comunicação entre o computador e a máquina virtual, configuramos a rede no modo Bridge.

**O que é Bridge?**

O modo Bridge faz com que a máquina virtual utilize a rede como se fosse outro dispositivo conectado a ela. Dessa maneira, ela recebe um endereço IP próprio e pode ser acessada por outros dispositivos da mesma rede.

Essa configuração foi realizada nas configurações de rede do programa responsável pela virtualização.

### 2.2. Identificando o endereço IP

Com a máquina virtual iniciada, utilizamos o seguinte comando:

`hostname -I`

**Função do comando:**

- `hostname`: identifica informações relacionadas ao nome e à rede da máquina.
- `-I`: exibe os endereços IP associados às interfaces de rede.

O comando permite descobrir o endereço IP necessário para estabelecer a conexão remota.

No nosso caso, o endereço utilizado foi:

`192.168.15.18`

É importante lembrar que o endereço IP pode ser diferente em cada computador e rede.

### 2.3. Estabelecendo a conexão SSH

Depois de identificar o IP, abrimos o terminal do computador principal. No Windows, utilizamos o CMD.

O comando utilizado foi:

`ssh aluno@192.168.15.18`

**Explicação dos elementos:**

- `ssh`: inicia uma conexão utilizando o protocolo Secure Shell.
- `aluno`: representa o nome do usuário cadastrado no Ubuntu.
- `@`: separa o nome do usuário do endereço da máquina.
- `192.168.15.18`: representa o endereço IP da máquina virtual.

Após executar o comando, foi necessário informar a senha do usuário.

Com isso, conseguimos acessar o terminal do Ubuntu diretamente pelo computador principal.

**Por que utilizamos SSH?**

O SSH permite administrar uma máquina remotamente por meio de um terminal. Isso facilita a execução de comandos, a instalação de programas e a edição de arquivos sem precisar utilizar diretamente a interface da máquina virtual.

---

## 3. INSTALAÇÃO E CONFIGURAÇÃO DO DOCKER

### 3.1. Verificando a instalação

Depois de estabelecer a conexão SSH, começamos a preparar o ambiente de desenvolvimento.

O primeiro passo foi verificar se o Docker estava instalado e qual era sua versão.

Comando:

`docker --version`

**Função:**

- `docker`: executa o programa Docker.
- `--version`: solicita a exibição da versão instalada.

No trabalho, foi apresentada a versão 29.8.1.

Esse procedimento permite verificar se o Docker está instalado e identificar sua versão.

### 3.2. Testando o funcionamento do Docker

Depois de verificar a instalação, executamos um teste utilizando:

`docker run hello-world`

**Explicação:**

- `docker`: chama o programa Docker.
- `run`: solicita a execução de um contêiner.
- `hello-world`: identifica a imagem utilizada para realizar o teste.

O Docker verifica se a imagem está disponível localmente. Caso não esteja, realiza seu download de um repositório de imagens, chamado Docker Hub.

Depois, cria e executa um contêiner baseado nessa imagem.

Se tudo estiver funcionando corretamente, será exibida uma mensagem de boas-vindas informando que a instalação está funcionando.

### 3.3. Instalação do pacote Tree

Para facilitar a visualização dos arquivos e diretórios do projeto, instalamos o pacote Tree.

Comando:

`sudo apt install tree`

**Explicação:**

- `sudo`: executa o comando com privilégios administrativos.
- `apt`: gerenciador de pacotes utilizado no Ubuntu.
- `install`: indica que desejamos instalar um pacote.
- `tree`: nome do pacote que será instalado.

O Tree permite visualizar a estrutura de diretórios em formato de árvore, facilitando a identificação dos arquivos de um projeto.

---

## 4. CRIAÇÃO DO PROJETO FLASK

### 4.1. Criando o diretório do projeto

Com o ambiente preparado, iniciamos a construção da aplicação web.

Primeiramente, criamos uma pasta para organizar todos os arquivos do projeto.

Comando:

`mkdir ~/projeto-flask`

**Explicação:**

- `mkdir`: cria um novo diretório.
- `~`: representa o diretório pessoal do usuário.
- `projeto-flask`: nome escolhido para a pasta.

Depois, entramos no diretório criado:

`cd ~/projeto-flask`

**Função:**

- `cd`: significa Change Directory e permite navegar entre diretórios.
- `~/projeto-flask`: indica o caminho da pasta que desejamos acessar.

A partir desse momento, os arquivos criados pelos próximos comandos serão armazenados dentro dessa pasta, desde que permaneçamos nela.

### 4.2. Criando o arquivo principal app.py

O próximo passo foi criar o arquivo responsável pela aplicação Flask.

Comando:

`touch app.py`

**Função:**

- `touch`: cria um arquivo vazio caso ele ainda não exista.
- `app.py`: nome do arquivo Python que conterá o código da aplicação.

Depois, utilizamos:

`nano app.py`

**Função:**

- `nano`: abre um editor de texto diretamente no terminal.
- `app.py`: indica qual arquivo será aberto para edição.

Dentro desse arquivo, desenvolvemos a aplicação utilizando Flask.

### 4.3. Estrutura do código Flask

A primeira instrução utilizada foi:

`from flask import Flask`

Essa instrução importa a classe Flask da biblioteca Flask.

Ela é necessária para criar e configurar nossa aplicação web.

Em seguida:

`app = Flask(__name__)`

**Explicação:**

- `app`: variável que armazena a aplicação.
- `Flask`: classe utilizada para criar a aplicação.
- `__name__`: variável especial do Python que identifica o módulo atual.

Essa linha inicializa a aplicação Flask.

### 4.4. Criando rotas

Para disponibilizar páginas e conteúdos na aplicação, utilizamos rotas.

Exemplo:

`@app.route('/')`

**Função:**

- `@app.route`: é um decorador do Flask utilizado para associar um endereço a uma função.
- `'/'`: representa a página inicial da aplicação.

Logo depois, criamos uma função:

`def inicio():`

A palavra `def` é utilizada no Python para declarar uma função.

Nesse caso, a função `inicio()` será executada quando alguém acessar a rota `/`.

Para apresentar conteúdo ao usuário, utilizamos o comando `return`, que devolve uma resposta ao navegador.

Também foram utilizadas estruturas HTML dentro das respostas, permitindo apresentar textos, títulos e links.

### 4.5. Executando a aplicação

Ao final do arquivo, utilizamos a estrutura:

`if __name__ == "__main__":`

Essa condição verifica se o arquivo está sendo executado diretamente, e não importado por outro arquivo Python.

Dentro dela, colocamos:

`app.run(host="0.0.0.0", port=5000, debug=True)`

**Explicação de cada parâmetro:**

- `app.run()`: inicia o servidor de desenvolvimento do Flask.
- `host="0.0.0.0"`: permite que o servidor aceite conexões por meio das interfaces de rede da máquina, não ficando restrito ao acesso local.
- `port=5000`: define a porta utilizada pelo servidor.
- `debug=True`: ativa o modo de depuração, facilitando a identificação de erros durante o desenvolvimento.

A porta 5000 será utilizada posteriormente para acessar a aplicação pelo navegador.

---

## 5. CRIANDO O ARQUIVO REQUIREMENTS.TXT

Depois de criar a aplicação, precisamos definir quais bibliotecas serão necessárias para executá-la.

Para isso, criamos o arquivo:

`touch requirements.txt`

Depois, abrimos:

`nano requirements.txt`

Dentro dele, adicionamos:

`Flask`

**Qual é a função desse arquivo?**

O arquivo requirements.txt registra as dependências Python necessárias para executar o projeto.

Nesse caso, informamos que a aplicação precisa da biblioteca Flask.

Posteriormente, o Docker utilizará esse arquivo para instalar automaticamente as dependências durante a construção da imagem.

Isso facilita a reprodução do ambiente em outros computadores.

---

## 6. CRIANDO O DOCKERFILE

### 6.1. O que é um Dockerfile?

O Dockerfile é um arquivo de configuração que contém as instruções utilizadas pelo Docker para construir uma imagem.

Ele determina qual ambiente será utilizado, onde os arquivos serão armazenados, quais bibliotecas serão instaladas e qual comando será executado quando o contêiner iniciar.

Criamos o arquivo com:

`touch Dockerfile`

Depois, abrimos:

`nano Dockerfile`

Dentro dele, adicionamos as seguintes instruções:

### 6.2. Explicação de cada instrução

**1. FROM python:3.14-slim**

Define a imagem-base utilizada para construir o ambiente.

- `FROM`: determina a imagem inicial.
- `python:3.14-slim`: utiliza uma imagem do Python 3.14 em uma versão reduzida.

A versão Slim possui uma estrutura mais enxuta, evitando componentes desnecessários.

**2. WORKDIR /app**

Define o diretório de trabalho dentro do contêiner.

- `WORKDIR`: estabelece o diretório em que as próximas instruções serão executadas.
- `/app`: nome e caminho do diretório criado ou utilizado.

Assim, os arquivos da aplicação ficarão organizados dentro de `/app`.

**3. COPY requirements.txt .**

Copia o arquivo de dependências para dentro do contêiner.

- `COPY`: copia arquivos do computador para a imagem.
- `requirements.txt`: arquivo de origem.
- `.`: representa o diretório de trabalho atual dentro do contêiner.

**4. RUN pip install --no-cache-dir -r requirements.txt**

Executa a instalação das bibliotecas necessárias.

- `RUN`: executa um comando durante a construção da imagem.
- `pip`: gerenciador de pacotes Python.
- `install`: indica a instalação de bibliotecas.
- `--no-cache-dir`: evita armazenar o cache de downloads do pip, ajudando a reduzir o tamanho da imagem.
- `-r`: indica que as dependências serão lidas de um arquivo.
- `requirements.txt`: arquivo que contém as bibliotecas necessárias.

**5. COPY app.py .**

Copia o arquivo principal da aplicação para o diretório de trabalho dentro do contêiner.

- `COPY`: realiza a cópia.
- `app.py`: arquivo que contém o código Flask.
- `.`: diretório de destino.

**6. EXPOSE 5000**

Informa que a aplicação utiliza a porta 5000 dentro do contêiner.

Essa instrução documenta a porta utilizada pelo serviço, mas não publica a porta automaticamente no computador principal.

**7. CMD ["python", "app.py"]**

Define o comando padrão executado quando o contêiner é iniciado.

- `CMD`: determina o comando padrão do contêiner.
- `python`: chama o interpretador Python.
- `app.py`: indica o arquivo que será executado.

Dessa forma, quando o contêiner iniciar, o Python executará nossa aplicação Flask.

---

## 7. CONFERINDO A ESTRUTURA DO PROJETO

Depois de criar os arquivos, utilizamos o comando:

`tree -a`

**Explicação:**

- `tree`: apresenta os diretórios e arquivos em formato de árvore.
- `-a`: inclui também os arquivos ocultos.

A estrutura apresentada nessa etapa foi:

projeto-flask/
- app.py
- Dockerfile
- requirements.txt

Essa organização é importante porque todos os arquivos necessários para construir a imagem estão reunidos no mesmo diretório.

---

## 8. CONSTRUINDO A IMAGEM DOCKER

### 8.1. O que é uma imagem Docker?

Uma imagem Docker é um modelo utilizado para criar contêineres.

Ela reúne o ambiente necessário para executar uma aplicação, incluindo arquivos, bibliotecas e configurações.

No nosso projeto, a imagem será construída a partir do Dockerfile.

Para isso, executamos:

`docker build -t flask-app .`

**Explicação de cada parte:**

- `docker`: chama o Docker.
- `build`: solicita a construção de uma imagem.
- `-t`: permite definir um nome ou uma identificação para a imagem.
- `flask-app`: nome escolhido para a imagem.
- `.`: indica que o Dockerfile e os arquivos necessários estão no diretório atual.

Durante esse processo, o Docker executa as instruções do Dockerfile, prepara o ambiente Python, instala o Flask e copia os arquivos da aplicação.

Ao terminar, teremos uma imagem chamada `flask-app`.

---

## 9. EXECUTANDO O CONTÊINER

Depois de construir a imagem, precisamos criar e executar um contêiner baseado nela.

Comando utilizado:

`docker run -d -p 5000:5000 --name meu-flask flask-app`

**Explicação:**

- `docker`: chama o Docker.
- `run`: cria e inicia um contêiner.
- `-d`: executa o contêiner em segundo plano, sem manter o terminal ocupado.
- `-p 5000:5000`: publica e associa a porta 5000 do computador à porta 5000 do contêiner.
- `--name meu-flask`: define o nome do contêiner como `meu-flask`.
- `flask-app`: identifica a imagem utilizada para criar o contêiner.

A diferença entre imagem e contêiner é importante:

A imagem funciona como um modelo que contém as instruções e os arquivos necessários.

O contêiner é a instância criada a partir dessa imagem, na qual a aplicação efetivamente será executada.

### 9.1. Acessando a aplicação pelo navegador

Com o contêiner em execução, abrimos o navegador do computador principal.

Digitamos o seguinte endereço:

`http://192.168.15.18:5000`

**Entendendo o endereço:**

- `http://`: protocolo utilizado para acessar a aplicação.
- `192.168.15.18`: endereço IP da máquina virtual.
- `:5000`: porta em que o Flask está disponibilizando a aplicação.

Se tudo estiver funcionando corretamente, o navegador apresentará o conteúdo definido no arquivo app.py.

Essa etapa confirmou que conseguimos executar uma aplicação Flask dentro de um contêiner Docker e acessá-la remotamente.

---

## 10. DESAFIO: INTEGRAÇÃO COM MYSQL E DOCKER COMPOSE

Na última parte do trabalho, ampliamos a aplicação para trabalhar com banco de dados e diferentes serviços.

Até esse momento, tínhamos uma aplicação Flask funcionando dentro de um contêiner.

O desafio consistiu em integrar três serviços:

1. MySQL: responsável pelo armazenamento dos dados.
2. Flask: responsável pela aplicação web.
3. Apache HTTP Server: utilizado como servidor web na arquitetura proposta.

Para organizar e executar esses serviços conjuntamente, utilizamos o Docker Compose.

### 10.1. Atualizando o requirements.txt

Primeiramente, abrimos novamente o arquivo:

`nano requirements.txt`

Adicionamos as seguintes bibliotecas:

`Flask==3.1.2`

`mysql-connector-python`

**Explicação:**

- `Flask==3.1.2`: define a utilização da versão 3.1.2 do Flask.
- `mysql-connector-python`: biblioteca que permite estabelecer conexões entre aplicações Python e bancos de dados MySQL.

A utilização do conector possibilita que o Flask envie comandos SQL ao banco de dados.

### 10.2. Modificando o app.py

Depois, modificamos o arquivo principal para incorporar as funcionalidades relacionadas ao MySQL.

Além da importação do Flask, adicionamos:

`import mysql.connector`

Essa instrução importa a biblioteca responsável pela comunicação entre Python e MySQL.

Também adicionamos:

`import os`

O módulo `os` permite acessar recursos relacionados ao sistema operacional. Nesse projeto, foi utilizado para recuperar informações armazenadas em variáveis de ambiente.

### 10.3. Criando a função de conexão com o banco

Uma das principais funções adicionadas foi:

`def conectar_bd():`

Essa função é responsável por estabelecer a conexão com o banco de dados MySQL.

Dentro dela, utilizamos:

`mysql.connector.connect()`

Esse método cria a conexão com o servidor MySQL.

Os parâmetros utilizados foram:

- `host=os.environ.get("DB_HOST", "db")`: define o endereço ou nome do servidor do banco de dados.
- `user=os.environ.get("DB_USER", "flaskuser")`: identifica o usuário utilizado na conexão.
- `password=os.environ.get("DB_PASSWORD")`: recupera a senha do banco.
- `database=os.environ.get("DB_NAME", "meu_banco")`: define qual banco de dados será utilizado.

**O que é os.environ.get()?**

É um método utilizado para recuperar variáveis de ambiente.

Essas variáveis permitem armazenar configurações fora do código principal, facilitando a organização e evitando deixar informações de acesso diretamente no arquivo Python.

O segundo argumento, quando fornecido, representa um valor padrão utilizado caso a variável não esteja definida.

### 10.4. Criando as rotas da aplicação

Além da conexão com o banco, foram criadas diferentes rotas.

**Rota inicial — /**

A rota inicial apresenta o título da aplicação e os links para as outras páginas.

Foram utilizados elementos HTML como:

- `<h1>`: cria um título principal.
- `<ul>`: cria uma lista não ordenada.
- `<li>`: representa um item da lista.
- `<a>`: cria um link para outra página.

**Rota Sobre — /sobre**

Apresenta informações sobre a aplicação.

Nesse caso, foi utilizado o método `return` para devolver um conteúdo HTML ao navegador.

**Rota Contato — /contato**

Apresenta as informações de contato, como o endereço de e-mail utilizado no exemplo.

**Rota Alunos — /alunos**

Essa foi a rota responsável por demonstrar a integração entre Flask e MySQL.

Nela, foram utilizadas funções para conectar ao banco, consultar informações e apresentar os resultados na página.

### 10.5. Criando e consultando a tabela de alunos

Dentro da rota `/alunos`, utilizamos:

`try:`

O bloco `try` permite executar um conjunto de instruções que podem apresentar erros.

Primeiramente, estabelecemos a conexão:

`conexao = conectar_bd()`

Depois, criamos um cursor:

`cursor = conexao.cursor()`

**O que é um cursor?**

O cursor é um objeto utilizado para executar comandos SQL e recuperar os resultados das consultas realizadas no banco de dados.

Em seguida, utilizamos:

`cursor.execute()`

Esse método executa uma instrução SQL no banco.

A primeira instrução utilizada foi:

`CREATE TABLE IF NOT EXISTS alunos (id INT AUTO_INCREMENT PRIMARY KEY, nome VARCHAR(100))`

**Explicação:**

- `CREATE TABLE`: cria uma tabela.
- `IF NOT EXISTS`: evita tentar criar novamente uma tabela que já existe.
- `alunos`: nome da tabela.
- `id INT`: cria uma coluna para armazenar números inteiros.
- `AUTO_INCREMENT`: gera automaticamente um novo número para cada registro.
- `PRIMARY KEY`: define a chave primária da tabela.
- `nome VARCHAR(100)`: cria uma coluna de texto com capacidade de até 100 caracteres.

Depois, verificamos a quantidade de registros:

`SELECT COUNT(*) FROM alunos`

**Explicação:**

- `SELECT`: realiza uma consulta.
- `COUNT(*)`: conta a quantidade de registros encontrados.
- `FROM alunos`: indica a tabela consultada.

Para recuperar o resultado, utilizamos:

`total = cursor.fetchone()[0]`

**Explicação:**

- `fetchone()`: recupera uma linha do resultado da consulta.
- `[0]`: acessa o primeiro elemento dessa linha.

Caso a tabela estivesse vazia, o programa executaria:

`INSERT INTO alunos (nome) VALUES ('João'), ('Maria'), ('Pedro')`

**Explicação:**

- `INSERT INTO`: insere novos registros.
- `alunos`: indica a tabela.
- `(nome)`: indica a coluna que receberá os dados.
- `VALUES`: apresenta os valores que serão inseridos.

Com isso, foram adicionados três alunos de exemplo.

Depois, utilizamos:

`conexao.commit()`

Esse método confirma as alterações realizadas no banco de dados, tornando os registros inseridos permanentes.

Para consultar os alunos:

`SELECT * FROM alunos`

**Explicação:**

- `SELECT`: solicita informações.
- `*`: representa todas as colunas.
- `FROM alunos`: indica a tabela consultada.

Em seguida:

`alunos = cursor.fetchall()`

O método `fetchall()` recupera todas as linhas retornadas pela consulta.

### 10.6. Apresentando os resultados no HTML

Depois de recuperar os registros, utilizamos uma variável para montar o conteúdo HTML:

`html = "<h1>Lista de Alunos</h1><ul>"`

Essa instrução inicia uma página contendo um título e uma lista.

Depois, utilizamos:

`for aluno in alunos:`

A estrutura `for` percorre todos os registros recuperados do banco de dados.

Dentro dela, adicionamos cada aluno à lista HTML.

Acessamos os dados utilizando índices:

- `aluno[0]`: representa o ID do aluno.
- `aluno[1]`: representa o nome do aluno.

Ao final, fechamos a lista e adicionamos um link para voltar à página inicial.

### 10.7. Encerrando a conexão com o banco

Depois de utilizar o banco de dados, precisamos encerrar os recursos utilizados.

Para isso, foram executados:

`cursor.close()`

Fecha o cursor utilizado para executar as consultas SQL.

`conexao.close()`

Encerra a conexão com o servidor MySQL.

Também foi utilizado:

`except Exception as erro:`

O bloco `except` captura erros que possam ocorrer durante a execução do código.

A variável `erro` recebe a descrição do problema, permitindo apresentar uma mensagem de erro ao usuário.

Essa estrutura evita que uma falha na conexão ou na consulta interrompa a aplicação sem apresentar uma resposta.

---

## 11. CRIANDO O ARQUIVO .ENV

Para organizar as informações de acesso ao banco de dados, criamos um arquivo chamado `.env`.

Comando:

`touch .env`

Depois:

`nano .env`

Dentro dele, adicionamos:

`MYSQL_ROOT_PASSWORD=sua_senha_root`

`MYSQL_PASSWORD=sua_senha_flask`

**Qual é a função do arquivo .env?**

O arquivo `.env` armazena variáveis de ambiente que serão utilizadas pelos serviços do projeto.

Nesse caso, armazenamos duas senhas:

- `MYSQL_ROOT_PASSWORD`: senha do usuário administrativo root do MySQL.
- `MYSQL_PASSWORD`: senha do usuário utilizado pela aplicação Flask.

Essas informações serão utilizadas posteriormente pelo Docker Compose.

É importante não compartilhar esse arquivo publicamente, pois ele contém informações de acesso ao banco de dados.

---

## 12. CRIANDO O ARQUIVO COMPOSE.YAML

### 12.1. O que é Docker Compose?

O Docker Compose é uma ferramenta que permite definir e executar vários serviços relacionados a uma aplicação utilizando um único arquivo de configuração.

Em vez de iniciar manualmente cada contêiner, podemos descrever todos os serviços no arquivo compose.yaml e executá-los conjuntamente.

Criamos o arquivo:

`touch compose.yaml`

Depois, abrimos:

`nano compose.yaml`

Nesse arquivo, definimos três serviços: db, flask e server.

### 12.2. Serviço DB — MySQL

A primeira parte da configuração foi:

`services:`

Essa instrução inicia a definição dos serviços que serão utilizados.

Em seguida:

`db:`

Define o nome do serviço responsável pelo banco de dados.

**Imagem utilizada:**

`image: mysql:8.0`

- `image`: indica a imagem Docker utilizada.
- `mysql:8.0`: identifica a versão 8.0 do MySQL.

**Configuração de ambiente:**

`environment:`

Indica as variáveis de ambiente utilizadas pelo serviço.

Foram configuradas:

- `MYSQL_ROOT_PASSWORD`: senha administrativa do MySQL.
- `MYSQL_DATABASE`: nome do banco que será criado.
- `MYSQL_USER`: usuário utilizado pela aplicação.
- `MYSQL_PASSWORD`: senha desse usuário.

**Volumes:**

`volumes:`

Define o armazenamento persistente utilizado pelo serviço.

Foi configurado:

`- mysql_data:/var/lib/mysql`

Essa configuração associa o volume chamado `mysql_data` ao diretório em que o MySQL armazena seus dados.

A principal vantagem é preservar as informações mesmo quando o contêiner é removido e recriado.

**Healthcheck:**

O healthcheck verifica se o serviço MySQL está funcionando e pronto para receber conexões.

No projeto, foi utilizada a instrução:

`test: ["CMD-SHELL", "mysqladmin ping -h 127.0.0.1 -uroot -p\"$${MYSQL_ROOT_PASSWORD}\" --silent"]`

Ela executa um teste utilizando o comando `mysqladmin ping`.

- `CMD-SHELL`: executa o teste por meio de um shell.
- `mysqladmin`: ferramenta administrativa do MySQL.
- `ping`: verifica se o servidor MySQL responde.
- `-h 127.0.0.1`: indica o endereço local do servidor.
- `-uroot`: identifica o usuário root.
- `-p`: informa que será utilizada uma senha.
- `--silent`: reduz a quantidade de mensagens exibidas.

Também foram configurados:

`interval: 10s`

Define que o teste será realizado a cada dez segundos.

`retries: 5`

Define cinco tentativas antes de considerar o serviço como não saudável.

Essa verificação será importante para garantir que o Flask não tente acessar o banco antes que ele esteja pronto.

### 12.3. Serviço FLASK

O segundo serviço é responsável pela aplicação web.

Foi definido:

`flask:`

Esse é o nome do serviço.

Em seguida:

`build: .`

Indica que a imagem será construída utilizando o Dockerfile presente no diretório atual.

**Variáveis de ambiente:**

Foram utilizadas:

- `DB_HOST: db`: indica que o endereço do banco será o nome do serviço db.
- `DB_NAME: meu_banco`: define o banco utilizado.
- `DB_USER: flaskuser`: define o usuário de acesso.
- `DB_PASSWORD: ${MYSQL_PASSWORD}`: recupera a senha armazenada na variável MYSQL_PASSWORD.

A sintaxe `${VARIAVEL}` permite utilizar valores definidos no ambiente ou no arquivo `.env`.

**Portas:**

`ports:`

Foi configurado:

`- "5000:5000"`

Essa configuração publica a porta 5000 do contêiner Flask na porta 5000 da máquina principal.

**Dependências:**

`depends_on:`

Define a relação de dependência entre os serviços.

Foi utilizado:

`db:`

Identifica o serviço do qual o Flask depende.

`condition: service_healthy`

Determina que o Flask deve aguardar até que o serviço MySQL seja considerado saudável pelo healthcheck.

Isso ajuda a evitar problemas de inicialização causados pela tentativa de conexão com um banco ainda indisponível.

### 12.4. Serviço SERVER — Apache

O terceiro serviço é responsável pelo servidor Apache HTTP Server.

Foi definido:

`server:`

Nome do serviço.

**Imagem:**

`image: httpd:2.4`

Indica que será utilizada a imagem oficial do Apache HTTP Server, versão 2.4.

**Portas:**

`ports:`

Foi configurado:

`- "80:80"`

Essa configuração publica a porta 80 do contêiner na porta 80 da máquina principal.

**Volumes:**

Foi utilizado:

`- ./httpd.conf:/usr/local/apache2/conf/httpd.conf:ro`

Essa instrução associa um arquivo de configuração local ao arquivo de configuração utilizado pelo Apache dentro do contêiner.

- `./httpd.conf`: indica o arquivo local.
- `/usr/local/apache2/conf/httpd.conf`: indica o destino dentro do contêiner.
- `ro`: significa read-only, ou seja, somente leitura.

**Dependências:**

`depends_on:`

Foi utilizado:

`- flask`

Isso determina que o serviço Apache depende do serviço Flask para iniciar.

### 12.5. Definindo o volume persistente

Ao final do arquivo, foi adicionada a configuração:

`volumes:`

E dentro dela:

`mysql_data:`

Essa declaração define o volume nomeado utilizado pelo serviço MySQL.

Ele permite armazenar os dados do banco de forma persistente, separando o armazenamento das informações do ciclo de vida do contêiner.

---

## 13. EXECUTANDO O DOCKER COMPOSE

Depois de configurar os três serviços, chegamos à última etapa do desenvolvimento.

Para construir as imagens e iniciar todos os serviços, utilizamos:

`docker compose up -d --build`

**Explicação:**

- `docker`: chama o Docker.
- `compose`: utiliza a ferramenta Docker Compose.
- `up`: cria e inicia os serviços definidos no arquivo compose.yaml.
- `-d`: executa os serviços em segundo plano.
- `--build`: solicita a construção ou reconstrução das imagens necessárias antes da inicialização.

Durante esse processo, o Docker Compose organiza a criação e a inicialização dos serviços MySQL, Flask e Apache, respeitando as dependências configuradas.

Dessa maneira, não precisamos executar cada contêiner individualmente.

---

## 14. RESULTADO FINAL

Após executar o comando do Docker Compose, a aplicação estará organizada em diferentes serviços que trabalham em conjunto.

A estrutura final apresenta:

**MySQL:** responsável por armazenar os dados dos alunos.

**Flask:** responsável por processar as requisições, executar as funções Python e apresentar as páginas da aplicação.

**Apache:** servidor HTTP utilizado na arquitetura proposta.

A aplicação apresenta uma página inicial com links para três seções:

- Sobre: apresenta informações sobre o sistema.
- Contato: apresenta as informações de contato.
- Alunos: apresenta a lista de alunos recuperada do banco de dados MySQL.

Na página de alunos, os registros são consultados diretamente no banco de dados e apresentados dinamicamente na aplicação.

O resultado demonstra a integração entre diferentes tecnologias e a utilização de contêineres para organizar os componentes de um sistema.

---

## 15. CONCLUSÃO

Ao longo deste trabalho, desenvolvemos uma aplicação web partindo da configuração de uma máquina virtual Ubuntu até a integração de diferentes serviços utilizando Docker Compose.

Inicialmente, aprendemos a acessar uma máquina remotamente por SSH e a preparar o ambiente Linux. Em seguida, verificamos a instalação do Docker e criamos uma aplicação utilizando Flask.

Posteriormente, aprendemos a construir imagens Docker por meio de um Dockerfile, executar contêineres e disponibilizar uma aplicação para acesso pelo navegador.

Por fim, ampliamos o projeto com a integração de um banco de dados MySQL, desenvolvemos consultas SQL para cadastrar e recuperar informações e utilizamos o Docker Compose para organizar três serviços diferentes.

O trabalho permitiu compreender, na prática, como diferentes ferramentas podem trabalhar juntas para construir, organizar e executar uma aplicação web em um ambiente baseado em contêineres.

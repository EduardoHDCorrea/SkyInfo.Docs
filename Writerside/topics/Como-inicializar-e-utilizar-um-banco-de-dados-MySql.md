# Como inicializar e utilizar um banco de dados MySql

<secondary-label ref="backend"/>
<secondary-label ref="guia"/>

## Contexto

O sistema de feriados utiliza um banco de dados MySQL para armazenar os dados de feriados e localidades. Com isso, surge a necessidade de saber como levantar um banco de dados MySQL localmente.

## Requisitos

É necessário ter o WSL instalado ou usar uma distribuição Linux. No meu caso, estou usando o Ubuntu no WSL. Também é preciso ter o Docker instalado no sistema, seja WSL ou Linux nativo.

## Instalação via Docker

Como toda instalação de imagem via Docker, é tudo muito simples. Basta rodar o comando abaixo:

    docker run -p {{PortaDesejada}}:3306 --name {{NomeDoContainer}} -e MYSQL_ROOT_PASSWORD={{SenhaDoRoot}} -e MYSQL_ROOT_HOST=% -d mysql/mysql-server

### Parâmetros:

    -p porta em que o banco de dados deve rodar. A porta padrão do MySQL é 3306, então é possível expô-la ao host do WSL com ela;
    --name nome do container;
    -e MYSQL_ROOT_PASSWORD cria-se uma variável de ambiente que armazena a senha root do banco de dados;
    -e MYSQL_ROOT_HOST=% informa o MySQL, por meio de uma variável de ambiente, que qualquer um pode conectar-se a ele, não somente o localhost. Isso permite o acesso via DBeaver ou outro gerenciador de banco de dados;
    -d roda o MySQL no modo Daemon;
    mysq/mysql-server a imagem padrão do MySQL.

<note>
É provável que a versão do MySQL tenha atualizado desde a escrita deste issue. Portanto, é recomendável pesquisar na internet a solução para algum problema de compatibilidade e atualizar este texto.
</note>

## Acesso via CLI

O MySQL vem com uma aplicação CLI que permite realizar qualquer ação no banco de dados. Com o comando abaixo, podemos acessar o container Docker e abrir o CLI do MySQL:

    docker container exec -it {{NomeDoContainer}} mysql -uroot -p

O comando fará com que o terminal entre no shell do MySQL no usuário Root. Dentro, podemos criar um novo banco de dados com o seguinte comando:

    create database {{NomeDoBancoDeDados}};

<note>
É necessário colocar um ponto e vírgula no final de cada comando. Do contrário, o shell apenas quebra a linha.
</note>

## Acesso via DBeaver

Conectar ao MySQL pelo DBeaver é simples, mas não é tão intuitivo.

Em primeiro lugar, selecione o MySQL nas opções de conexão do DBeaver. Se a porta do MySQL for a padrão, não precisa alterar. Do contrário, mude. Insira a senha do usuário Root ali embaixo, e tudo certo.

A parte mais "complicada" é navegar até a aba Driver properties e alterar a propriedade allowPublicKeyRetrieval de false para true.
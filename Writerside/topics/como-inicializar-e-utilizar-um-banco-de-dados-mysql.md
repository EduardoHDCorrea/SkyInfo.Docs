# Como inicializar e utilizar um banco de dados MySQL

<secondary-label ref="backend"/>
<secondary-label ref="guia"/>

## Introdução

Este guia visa ensinar como inicializar e configurar um banco de dados MySQL localmente, utilizando o Docker. 

## Requisitos

Para seguir este guia, você precisará de:

<list>
<li>Um ambiente Linux, ou <tooltip term="WSL">WSL</tooltip>.</li>
<li><a summary="Página oficial do Docker." href="https://www.docker.com/">Docker</a> instalado e configurado no sistema.</li>
</list>

## Instalação via Docker

A instalação de um banco de dados MySQL via Docker é simples. Basta executar o seguinte comando:


<code-block lang="bash">
docker run -p {{PortaDesejada}}:3306 --name {{NomeDoContainer}} \
-e MYSQL_ROOT_PASSWORD={{SenhaDoRoot}} \
-e MYSQL_ROOT_HOST=% \
-d mysql/mysql-server
</code-block>

### Parâmetros:

<deflist type="full" collapsible="true" default-state="collapsed">
<def>
<title>-p</title><p>Define a porta em que o banco de dados MySQL será acessível. A porta padrão do MySQL é 3306, e você pode expor essa porta ao host do WSL com a mesma porta ou uma diferente, se preferir.</p>
</def>
<def>
<title>--name</title><p>Nome do container que será criado.</p>
</def>
<def>
<title>-e MYSQL_ROOT_PASSWORD</title><p>Variável de ambiente que define a senha para o usuário root do MySQL.</p>
</def>
<def>
<title>-e MYSQL_ROOT_HOST=%</title><p>Permite que o MySQL seja acessado de qualquer endereço, e não apenas do localhost. Isso facilita a conexão usando ferramentas como DBeaver ou outros gerenciadores de banco de dados.</p>
</def>
<def>
<title>-d</title><p>Roda o container do MySQL em modo daemon (em segundo plano).</p>
</def>
<def>
<title>mysql/mysql-server</title><p>Especifica a imagem do MySQL a ser utilizada.</p>
</def>
</deflist>

<note> 
A versão do MySQL pode ter sido atualizada desde a criação deste guia. Em caso de erros ao executar o comando, consulte a documentação oficial.
</note>

<procedure title="Acesso via CLI" collapsible="true" type="steps">
<p>
O MySQL inclui uma interface de linha de comando (CLI) que permite a execução de comandos SQL e outras operações no banco de dados.
</p>
<step>
Para acessar o CLI do MySQL dentro do container, use o seguinte comando:
<code-block lang="bash">
docker container exec -it {{NomeDoContainer}} mysql -uroot -p
</code-block>
</step>
<step>
O comando fará com que o terminal entre no shell do MySQL no usuário Root. Dentro, podemos criar um novo banco de dados com o seguinte comando:
<code-block lang="sql">
CREATE DATABASE {{NomeDoBancoDeDados}};
</code-block>
</step>
<note>
Lembre-se de substituir <code>{{NomeDoContainer}}</code>, <code>{{SenhaDoRoot}}</code> e outros parâmetros pelos valores apropriados ao seu ambiente.
</note>
</procedure>

<procedure title="Acesso via DBeaver" collapsible="true" type="steps">
<p>
Para gerenciar o banco de dados MySQL visualmente, você pode usar o **DBeaver**, uma ferramenta de interface gráfica. 
Siga os passos abaixo para conectar-se ao MySQL no container Docker:
</p>
<step>Abra o <a summary="Página oficial do DBeaver." href="https://dbeaver.io/">DBeaver</a></step>
<step>No menu superior, clique em <control>File</control> &gt; <control>New</control> &gt; <control>Database Connection</control>.</step>
<step>Na lista de drivers, selecione <control>MySQL</control> e clique em <control>Next</control>.</step>
<step>
Preencha os seguintes campos de conexão:
<list>
<li><control>Host</control>: <code>localhost</code> ou o endereço IP onde o Docker está rodando.</li>
<li><control>Port</control>: A porta que você mapeou no comando Docker (por padrão, <code>3306</code>).</li>
<li><control>Database</control>: Você pode deixar vazio ou inserir o nome de um banco de dados existente.</li>
<li><control>Username</control>: <code>root</code>.</li>
<li><control>Password</control>: A senha definida na variável <code>MYSQL_ROOT_PASSWORD</code> no comando Docker.</li>
</list>
</step>

<step>Clique em <control>Test Connection</control> para verificar se a conexão está funcionando corretamente.</step>
<step>Se o teste for bem-sucedido, clique em <control>Finish</control> para salvar a conexão.</step>

<p>
Agora, você já pode gerenciar seu banco de dados MySQL com o <control>DBeaver</control>.
</p>

<note>
Caso o Docker esteja rodando no WSL, certifique-se de que a porta configurada está corretamente exposta ao host e de que o MySQL está acessível pelo endereço <code>localhost</code> ou IP correto.
</note>
</procedure>
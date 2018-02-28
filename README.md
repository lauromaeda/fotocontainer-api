Esta é uma documentação resumida sobre o projeto, com o objetivo de explicar como instalar, dependências e a estrutura interna da aplicação. O código neste repositório se refere a API da aplicação, que realiza as operações de persistência, envio de emails entre outras atribuições.

Esta aplicação foi feita de acordo com alguns princípios de domain driven design e clean code, para deixar regras de negócio isoladas do framework e de bibliotecas de terceiros, como por exemplo o envio de emails e persistência de dados.

# Dependências

## PHP
O código foi criado para ser executado minimamente na versão **7.1** do PHP, se valendo das implementações desta versão. O código **não** executa em versões abaixo desta. 

## Framework
Foi utilizado um micro-framework para fazer as implementações, que é o [Slim 3](https://www.slimframework.com/docs/). Este framework que realiza o roteamento e mantêm as dependências do projeto.

## Persistência
Utilizamos uma bridge com o [Eloquent](https://laravel.com/docs/5.5/eloquent) para realizar as dependências.

# Instalação e configuração

Esta seção trata de instalação e configuração da aplicação. Foi criado um makefile que instala a aplicação, e este é o método que **deve** ser utilizado. Esta sessão descreve também a forma manual de instalar a aplicação.

## Instalação automática

Apenas clone o projeto e execute o seguinte comando: `make install`. Deste modo a aplicação será instalada automaticamente, necessitando apenas de configuração, que deve ser feita posteriormente. O banco de dados pode ser migrado de forma similar, sendo obrigatório um servidor MariaDB já estar instalado e rodando. Execute este comando e siga as instruções dadas:

* `./fotocontainer tools:database_install` 

## Instalação manual

Se por algum motivo não foi possível instalar utilizando o make, a instalação pode ser feita de acordo com os seguintes passos.

### Instalar as dependências

É utilizado o [Composer](https://getcomposer.org/download/) para gestão de dependências. Para instalar, siga os seguintes passos:

* Baixe o composer

`wget https://getcomposer.org/composer.phar`

* Instale as dependências:

`php composer.phar install --no-dev --no-progress`

* Torne o console da aplicação executável:

`chmod +x fotocontainer`

* Crie a seguinte estrutura de diretório:

`mkdir var`

`mkdir var/cache`

`mkdir var/logs`

`mkdir var/pool`

`chmod -Rf 775 var/`

* Crie o arquivo .env

`cp public/.env.SAMPLE public/.env`

### Criar o Banco de Dados

Por último, crie o banco de dados para aplicação. O servidor MariaDB já deve estar instalado, e o banco de dados já deve ter sido criado neste servidor. Para gerenciar as migrações, utilizamos o [Phinx](https://phinx.org/). Antes de executar qualquer comando, edite o arquivo [phinx.yml](https://github.com/luizfsnunes/photocontainer-api/blob/master/phinx.yml) com suas configurações de banco.

* Execute o seguinte comando:

`./vendor/bin/phinx migrate`

# Configuração

A configuração da aplicação reside em um arquivo .env. Para facilitar a instalação existe um exemplo deste arquivo, chamado [.env.SAMPLE](https://github.com/luizfsnunes/photocontainer-api/blob/master/public/.env.SAMPLE). Neste exemplo estão todas as configurações disponíveis, com explicações sobre o que cada uma delas significa. Crie um arquivo .env baseado neste exemplo, o altere de acordo com as suas configurações locais e o coloque em `/public`.

## Configurar jobs na cron

A aplicação utiliza alguns jobs que devem ser invocados pela cron, devendo ser executados minuto a minuto. Coloque os seguinte comandos na cron:

* Comando para processar envio de emails em fila

`./fotocontainer queue_process:emails`

* Comando para aplicar marca d'água nas fotos

`./fotocontainer queue_process:images`

## Validar a instalação (Opcional)

Execute o seguinte comando para o diagnóstico da aplicação:
`./fotocontainer tools:verify`

Se o comando retornar que está tudo certo, a aplicação foi instalada com sucesso.
 

Esta é uma documentação resumida sobre o projeto, com o objetivo de explicar como instalar, dependências e a estrutura interna da aplicação. O código neste repositório se refere a API da aplicação, que realiza as operações de persistência, envio de emails entre outras atribuições.

Esta aplicação foi feita de acordo com alguns princípios de domain driven design e clean code, para deixar regras de negócio isoladas do framework e de bibliotecas de terceiros, como por exemplo o envio de emails e persistência de dados.

## Dependências

### PHP
O código foi criado para ser executado minimamente na versão **7.1** do PHP, se valendo das implementações desta versão. O código **não** executa em versões abaixo desta. 

### Framework
Foi utilizado um micro-framework para fazer as implementações, que é o [Slim 3](https://www.slimframework.com/docs/). Este framework que realiza o roteamento e mantêm as dependências do projeto.

### Persistência
Utilizamos uma bridge com o [Eloquent](https://laravel.com/docs/5.5/eloquent) para realizar as dependências.


# WordPress Docker Roots/Sage

Ambiente docker criado para desenvolvimento local usando: Wordpress + Composer + Roots/Sage

<br>

## Imagens usadas

- [Composer](https://hub.docker.com/r/pimlab/composer)
- [WP CLI](https://hub.docker.com/_/wordpress/)
- [phpMyAdmin](https://hub.docker.com/r/phpmyadmin/phpmyadmin/)
- [MySQL](https://hub.docker.com/_/mysql/)

<br>

## Requisitos do sistema

Certifique-se de ter as versões mais recentes do instaladas em sua máquina.

- [Node.js](https://github.com/nvm-sh/nvm#installing-and-updating)
- [Yarn](https://classic.yarnpkg.com/lang/en/docs/install/#debian-stable)
- [Composer](https://getcomposer.org/download/)
- [Docker](https://docs.docker.com/engine/install/)
- [Docker Compose](https://docs.docker.com/compose/install/)

<br>

## Configuração

Copie o ambiente de exemplo em `.env`

```
cp .env.example .env
```

Edite o arquivo `.env` para alterar o endereço IP padrão, a senha raiz do MySQL e o nome do banco de dados WordPress.

<br>

## Instalação

Abra um terminal e `cd` para a pasta na qual o `docker-compose.yml` está salvo e execute:

```
docker-compose up
```

Isso cria duas novas pastas na raiz do projeto:

* `dump` – usado para armazenar e restaurar dumps de banco de dados

* `public` – pasta do site wordpress

Após concluir a execução dos contêineres, Você deve conseguir acessar a instalação do wordpress com o IP: `http://127.0.0.1` ou `http://localhost`

Você também pode adicionar uma nova entrada em seu arquivo hosts.

<br>

## Pós-configuração do sage

Navegue até a pasta do tema `./public/wp-content/themes/sage` e rode os seguintes comandos:

```
composer run post-create-project-cmd
```

Se você usa as versões mais recentes do node, atualize o pacote `node-sass` do sage. Caso contrário, você pode pular para o próximo passo.

```
yarn add node-sass
```

Após preencher as informações do tema, execute:

```
yarn
```

Compile os assets do tema digitando:

```
yarn build
```

Após  baixar todas as dependências, inicie o projeto:

```
yarn start
```

Compile os assets para produção (opcional):

```
yarn build:production
```

### Criando dumps de banco de dados

Na raiz do projeto `./public`, execute o comando:

```
./export.sh
```

O arquivo SQL será exportado para a pasta `./dump`

<br>

### WP CLI

O projeto também fornece um serviço para usar o [WordPress CLI](https://developer.wordpress.org/cli/commands/).

Comando de exemplo para instalar o WordPress:

```
docker-compose run --rm wpcli core install --url=http://localhost --title=test --admin_user=admin --admin_email=test@example.com
```

Ou para listar os plugins instalados

```
docker-compose run --rm wpcli plugin list
```

Para um uso mais fácil, considere adicionar um alias para a CLI:

```
alias wp="docker-compose run --rm wpcli"
```

Dessa forma, você pode usar o comando CLI acima da seguinte forma:

```
wp plugin list
```

<br>

### phpMyAdmin

Você também pode visitar `http://127.0.0.1:8080` para acessar o phpMyAdmin após iniciar os containers.

O nome de usuário padrão é `root`, e a senha é a mesma fornecida no arquivo `.env`.

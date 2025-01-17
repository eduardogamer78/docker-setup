## Setup Docker Para Projetos Laravel (8, 9, 10 ou 11)

### Passo a passo

Copie os arquivos docker-compose.yml, Dockerfile e o diretório docker/ para o seu projeto
```sh
cp -rf setup-docker/* nome-projeto/
```
```sh
cd nome-projeto/
```

Crie o Arquivo .env
```sh
cp .env.example .env
```

Atualize as variáveis de ambiente do arquivo .env
```dosini
APP_NAME="Laravel"
APP_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=root

CACHE_DRIVER=redis
QUEUE_CONNECTION=redis
SESSION_DRIVER=redis

REDIS_HOST=redis
REDIS_PASSWORD=null
REDIS_PORT=6379
```
Suba os containers do projeto
```sh
docker-compose up -d
```
Acessar o container
```sh
docker-compose exec app bash
```

Instalar as dependências do projeto
```sh
composer install
```
Gerar a key do projeto Laravel
```sh
php artisan key:generate
```
Acessar o projeto
[http://localhost](http://localhost)

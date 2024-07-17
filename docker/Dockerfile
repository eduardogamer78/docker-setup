FROM php:8.3-fpm

# set your user name, ex: user=carlos
ARG user=yourusername
ARG uid=1000

## apt-utils é um extensão de recursos do gerenciador de pacotes apt
RUN apt-get update && apt-get install -y --no-install-recommends \
   apt-utils

## dependencias recomendadas de desenvolvimento para ambiente linux
RUN apt-get update && apt-get install -y \
    curl \
    git \ 
    zip \
    unzip \
    libpng-dev \
    libonig-dev \
    libxml2-dev

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd sockets

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Create system user to run Composer and Artisan Commands
RUN useradd -G www-data,root -u $uid -d /home/$user $user
RUN mkdir -p /home/$user/.composer && \
    chown -R $user:$user /home/$user

RUN pecl install -o -f redis \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis

COPY ./docker/php/extra-php.ini "$PHP_INI_DIR/extra-php.ini/"

WORKDIR /var/www

USER $user
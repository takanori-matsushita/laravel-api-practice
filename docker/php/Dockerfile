FROM php:7.4-fpm-alpine

RUN apk update && \
  apk add autoconf \
  gcc \
  g++ \
  make

RUN docker-php-ext-install pdo pdo_mysql

RUN pecl install xdebug \
  && docker-php-ext-enable xdebug

#Composer install
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

ENV  PATH $PATH:/composer/vendor/bin

RUN composer global require "laravel/installer"

RUN mkdir -p /app
WORKDIR /app
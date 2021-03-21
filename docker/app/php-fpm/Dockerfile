FROM php:7.4-fpm-alpine

WORKDIR /usr/share/nginx/html


# install dependent packages...
RUN set -xeu \
  && apk update \
  && apk add autoconf build-base \
  && apk add --no-cache libzip-dev icu-libs zlib-dev \
  && apk add --no-cache zip unzip \
  && apk add --no-cache --virtual build-dependencies icu-dev \
  && apk add --no-cache freetype-dev libjpeg-turbo-dev libmcrypt-dev libpng-dev \
  && pecl install xdebug \
  && docker-php-ext-install zip intl pdo_mysql \
  && docker-php-ext-enable xdebug

# provide root permission to composer
ENV COMPOSER_ALLOW_SUPERUSER 1 \
    COMPOSER_NO_INTERACTION 1

# install composer...
COPY --from=composer:1.9.3 /usr/bin/composer /usr/bin/composer
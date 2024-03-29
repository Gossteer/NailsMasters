# Image
FROM php:7.4.21-fpm

# Starting from scratch
RUN apt-get clean
RUN apt-get -y autoremove
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Dependencies
RUN apt-get update

# Node.js
RUN apt-get install -y nodejs

# NPM
RUN apt-get install -y npm
RUN npm install -g n
RUN n lts

# Zip
RUN apt-get install -y libzip-dev zip && docker-php-ext-configure zip && docker-php-ext-install zip

# Git
RUN apt-get install -y git

# Curl
RUN apt-get install -y libcurl3-dev curl && docker-php-ext-install curl

# GD
RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install gd

# MySQL
RUN apt-get install -y libpq-dev && docker-php-ext-install pdo pdo_mysql

# Human Language and Character Encoding Support
RUN apt-get install -y zlib1g-dev libicu-dev g++
RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl

# PHP pnctl
RUN docker-php-ext-install pcntl

# Custom php.ini config
COPY .docker/traefik/php/php.ini /usr/local/etc/php/php.ini

# Composer installation
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer
RUN chmod 0755 /usr/bin/composer

# Clean up
RUN apt-get clean
RUN apt-get -y autoremove
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ARG APP_ENV
ARG APP_NAME
# COPY . /var/www/$APP_NAME

# Set up default directory
WORKDIR /var/www/$APP_NAME
#
# COPY ./.env /var/www/maybe/.env
# COPY ./backend /var/www/maybe/backend
#
## Composer update
# RUN composer update
#
## Node install
# RUN npm install

FROM php:7.3-fpm-stretch

RUN apt-get update && apt-get install -y wget gnupg g++ locales unzip dialog apt-utils git && apt-get clean

RUN apt-get update && \
    apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libzip-dev \
    libicu-dev \
    libpq-dev \
    vim \
    nano \
    mc \
    htop \
    autoconf && \
    apt-get clean

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

# install necessary tools for running application
RUN docker-php-ext-install \
    bcmath \
    gd \
    intl \
    opcache \
    pgsql \
    pdo_pgsql \
    zip

# install redis extension
RUN pecl install redis-5.1.1 && \
    docker-php-ext-enable redis

# install locales and switch to en_US.utf8 in order to enable UTF-8 support
# see http://jaredmarkell.com/docker-and-locales/ from where was this code taken
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN echo "umask 000" >> /root/.bashrc
SHELL ["/bin/bash", "-c"]

COPY php/php.ini /usr/local/etc/php/

RUN mkdir -p /app

COPY app/ /app

# COPY app/ /var/www/html

RUN mkdir -p /var/www/html/web/cpresources /var/www/html/config/ /var/www/html/storage/ && \
    chmod -R 777 /var/www/html/config/ /var/www/html/storage/ /var/www/html/web/cpresources


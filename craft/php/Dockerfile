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

# RUN tee /etc/apt/sources.list.d/pgdg.list <<END \
#     deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main \
#     END

# RUN wget https://www.postgresql.org/media/keys/ACCC4CF8.asc && apt-key add ACCC4CF8.asc && apt-get update

# # install PostgreSQl client for dumping database
# RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - && \
#     sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -sc)-pgdg main" > /etc/apt/sources.list.d/PostgreSQL.list' && \
#     apt-get update && apt-get install -y postgresql-11 postgresql-client-11 && apt-get clean

# install redis extension
RUN pecl install redis-5.1.1 && \
    docker-php-ext-enable redis

# # install locales and switch to en_US.utf8 in order to enable UTF-8 support
# # see http://jaredmarkell.com/docker-and-locales/ from where was this code taken
# RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
#     locale-gen
# ENV LANG en_US.UTF-8
# ENV LANGUAGE en_US:en
# ENV LC_ALL en_US.UTF-8


COPY ./php/php.ini /usr/local/etc/php/

RUN mkdir -p /app

COPY app /app

RUN mkdir -p /app/web/cpresources && \
    chmod -R 777 /app/config/ /app/storage/ /app/web/cpresources
FROM php:7.3-fpm

USER root

RUN echo 'root:P@ssw0rd' | chpasswd; exit 0
RUN useradd -ms /bin/bash ubuntu; exit 0
RUN usermod -a -G root ubuntu; exit 0

RUN apt-get update && apt-get install -y \
    cron \
    libfreetype6-dev \
    libicu-dev \
    libonig-dev \
    libzip-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libxslt1-dev \
    zip \
    git \
    zlib1g-dev \
    wget \
    gnupg2


RUN docker-php-ext-configure \
    gd --with-freetype-dir=/usr --with-jpeg-dir=/usr

RUN docker-php-ext-install \
    bcmath \
    gd \
    intl \
    mbstring \
    opcache \
    pdo_mysql \
    soap \
    xsl \
    sockets \
    zip

RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/local/bin --filename=composer

RUN composer self-update --1

RUN pecl install -f xdebug-2.9.8 \
    && docker-php-ext-enable xdebug

#ENV PHP_MEMORY_LIMIT 2G
#ENV PHP_PORT 9000
#ENV PHP_PM dynamic
#ENV PHP_PM_MAX_CHILDREN 10
#ENV PHP_PM_START_SERVERS 4
#ENV PHP_PM_MIN_SPARE_SERVERS 2
#ENV PHP_PM_MAX_SPARE_SERVERS 6
ENV APP_MAGE_MODE developer

WORKDIR /app
USER ubuntu

#CMD ["/usr/local/bin/start"]
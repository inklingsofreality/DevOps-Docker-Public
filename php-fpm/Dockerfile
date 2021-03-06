FROM php:7.2-fpm

MAINTAINER Aaron Picht <apicht@users.noreply.github.com>


# Software Installation
#
# Installing dependencies and tools

RUN rm /etc/apt/preferences.d/no-debian-php && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        libicu-dev \
        libmemcached-dev \
        libz-dev \
        libpq-dev \
        libjpeg-dev \
        libpng-dev \
        libfreetype6-dev \
        libssl-dev \
        libxml2-dev \
        php-soap \
        libmcrypt-dev && \
        pecl install mcrypt-1.0.2 && \
    apt-get clean && apt-get autoclean && apt-get --purge -y autoremove && \
    rm -rf /var/lib/apt/lists/*

# Install basic extensions
RUN docker-php-ext-enable mcrypt && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install mysqli && \
    docker-php-ext-install pdo_pgsql && \
    docker-php-ext-install opcache && \
    docker-php-ext-install zip && \
    docker-php-ext-install intl && \
    docker-php-ext-install soap

# Install gd extension
RUN docker-php-ext-configure gd \
        --enable-gd-native-ttf \
        --with-jpeg-dir=/usr/lib \
        --with-freetype-dir=/usr/include/freetype2 && \
    docker-php-ext-install gd

# Install Redis extension
RUN pecl install -o -f redis && \
    docker-php-ext-enable redis && \
    rm -rf /tmp/pear

# Install cachetool
RUN curl -so /usr/local/bin/cachetool http://gordalina.github.io/cachetool/downloads/cachetool.phar && \
    chmod +x /usr/local/bin/cachetool

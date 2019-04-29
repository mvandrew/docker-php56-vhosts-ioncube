#
# Used to support old Web projects, such as OpenCart + Lights Shop.
#

FROM php:5.6-apache

LABEL maintainer "Andrey Mishchenko <info@msav.ru>"

RUN apt-get update && apt-get install -y \
        curl \
        wget \
        git \
        zlib1g-dev \
        bzip2 \
        libpng-dev \
        libjpeg-dev \
        libgif-dev \
    && a2enmod rewrite \
    && docker-php-ext-configure gd --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) mbstring mysqli pdo_mysql zip gd \
    && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

ADD http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.bz2 /tmp/

RUN tar xvjfC /tmp/ioncube_loaders_lin_x86-64.tar.bz2 /tmp/ \
    && cp /tmp/ioncube/ioncube_loader_lin_5.6.so /usr/local/lib/php/extensions/no-debug-non-zts-20131226 \
    && echo "zend_extension = /usr/local/lib/php/extensions/no-debug-non-zts-20131226/ioncube_loader_lin_5.6.so" > /usr/local/etc/php/conf.d/00-ioncube.ini \
    && rm /tmp/ioncube_loaders_lin_x86-64.tar.bz2 \
    && rm -rf /tmp/ioncube

RUN /etc/init.d/apache2 restart

EXPOSE 80

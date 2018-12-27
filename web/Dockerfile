FROM php:7.2-apache

# Use the default production configuration
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

RUN apt-get update && apt-get install -y libpq-dev && docker-php-ext-install pdo pdo_pgsql && a2enmod rewrite

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# Adding sources
RUN echo 'deb http://httpredir.debian.org/debian jessie contrib' >> /etc/apt/sources.list

# Installing packages
RUN apt-get update && apt-get upgrade -y
RUN export DEBIAN_FRONTEND=noninteractive && apt-get install -y --force-yes xorg libssl-dev libxrender-dev fontconfig xfonts-75dpi curl mysql-client libcurl4-gnutls-dev libxml2-dev libpng-dev libicu-dev libmcrypt-dev libjpeg62-turbo-dev libfreetype6-dev libjpeg62-turbo zlib1g-dev libmemcached11 libmemcached-dev git libgmp-dev psmisc xpdf libmagickwand-dev imagemagick xfonts-utils cabextract wget gnupg

# Install nodejs
RUN curl -sL https://deb.nodesource.com/setup_6.x -o nodesource_setup.sh && bash nodesource_setup.sh && apt-get -y --force-yes install nodejs

#RUN php -r "readfile('https://getcomposer.org/installer');" | php
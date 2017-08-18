FROM php:7.0-fpm

RUN apt-get update
RUN apt-get install -y zlib1g-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        sendmail \
        libxml2-dev \
        libicu-dev

# WP cli needs mysql client
RUN apt-get install -y mysql-client

# Clean up
RUN rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install zip
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install gd
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install xmlrpc
RUN docker-php-ext-install soap
RUN docker-php-ext-install intl

RUN pecl config-set php_ini /usr/local/etc/php/config/php.ini
RUN docker-php-ext-enable opcache

# Copy in fresh installation of Moodle
COPY moodle /var/www/html

RUN mkdir /moodledata

RUN ["chmod", "-R", "777", "/var/www/html"]
RUN ["chmod", "-R", "777", "/moodledata"]

WORKDIR /var/www/html

EXPOSE 9000

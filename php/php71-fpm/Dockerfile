FROM php:7.1.33-fpm
WORKDIR /www
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime \
&& echo 'America/Los_Angeles' >/etc/timezone

RUN apt-get update  && apt-get install -y  \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libxml2-dev \
        libc-client-dev \
        libkrb5-dev \
        librabbitmq-dev \
        imagemagick \
        libmagick++-dev \
        libcurl4-gnutls-dev \
        libicu-dev \
        g++  \
        unoconv \
        wget \
        libzip-dev \
        supervisor \
        libsystemd-dev \
        --allow-unauthenticated

RUN docker-php-ext-install -j$(nproc) gd mysqli intl zip pdo_mysql soap bcmath mcrypt

RUN pecl install -o -f mongodb-1.11.1 oauth swoole-4.4.26 imagick \
    && rm -rf /tmp/pear && docker-php-ext-enable  mongodb oauth  swoole imagick




RUN curl -sS https://getcomposer.org/installer | php 
RUN mv composer.phar /usr/local/bin/composer 
RUN chmod +x /usr/local/bin/composer 

EXPOSE 9000

CMD ["php-fpm", "supervisord -c /etc/supervisor/supervisord.conf"]

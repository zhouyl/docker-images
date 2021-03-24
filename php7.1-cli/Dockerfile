FROM php:7.1-cli-stretch

ARG BUILD_DEPENDENCIES="${PHPIZE_DEPS} zlib1g-dev libtool git automake wget unzip libgmp-dev libzip-dev libldap2-dev libmemcached-dev libyaml-dev libmagickwand-dev libmagickcore-dev"

RUN apt-get update && apt-get -y --no-install-recommends install ${BUILD_DEPENDENCIES}

RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

RUN docker-php-ext-enable opcache

RUN docker-php-ext-install ldap
RUN docker-php-ext-install sockets
RUN docker-php-ext-install pcntl
RUN docker-php-ext-install gd
RUN docker-php-ext-install gmp

RUN pecl install msgpack      && docker-php-ext-enable msgpack
RUN pecl install redis        && docker-php-ext-enable redis
RUN pecl install memcached    && docker-php-ext-enable memcached
RUN pecl install mongodb      && docker-php-ext-enable mongodb
RUN pecl install imagick      && docker-php-ext-enable imagick
RUN pecl install yaml         && docker-php-ext-enable yaml
RUN pecl install zip          && docker-php-ext-enable zip
RUN pecl install xdebug-2.9.8 && docker-php-ext-enable xdebug
RUN pecl install grpc         && docker-php-ext-enable grpc

RUN echo 'xdebug.mode=coverage' >> /usr/local/etc/php/php.ini

RUN curl -s https://getcomposer.org/composer.phar -o /usr/bin/composer
RUN chmod +x /usr/bin/composer
RUN /usr/bin/composer config -g secure-http false

WORKDIR /

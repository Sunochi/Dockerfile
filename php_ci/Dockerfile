FROM php:7.3.2-cli
MAINTAINER sunouchi_touga <sunouchiCy@gmail.com>

WORKDIR /tmp


RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y \
       git \
       libxml2-dev
RUN pecl install xdebug-2.7.0beta1
RUN docker-php-ext-install pcntl \
    && docker-php-ext-install soap \
    && docker-php-ext-enable xdebug
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/bin --filename=composer \
    && php -r "unlink('composer-setup.php');" \
    && composer require "phpunit/phpunit:^7.4" --prefer-source --no-interaction \
    && ln -s /tmp/vendor/bin/phpunit /usr/local/bin/phpunit \
    && sed -i 's/nn and/nn, Nicolas Frey (Docker) and/g' /tmp/vendor/phpunit/phpunit/src/Runner/Version.php \
    && composer require "squizlabs/php_codesniffer" --prefer-source --no-interaction \
    && ln -s /tmp/vendor/bin/phpcs /usr/local/bin/phpcs \
    && ln -s /tmp/vendor/bin/phpcbf /usr/local/bin/phpcbf

VOLUME ["/app"]
WORKDIR /app

ENTRYPOINT [""]

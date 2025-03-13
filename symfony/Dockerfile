FROM php:8-1apache

RUN apt-get update && apt-get install -y --no-install-recommends \
php \
php-cli \
php-mbstring \
php-xml \
php-curl \
unzip \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* tmp/* /var/tmp/*

RUN curl -sS https://getcomposer.org/installer | php
COPY composer.phar /usr/local/bin/composer

RUN curl -sS https://get.symfony.com/cli/installer | bash
COPY ~/.symfony/bin/symfony /usr/local/bin/symfony

RUN git clone https://github.com/Pech-App-Dev/pech-app-api.git

WORKDIR ./pech-app-api
RUN composer install

CMD php bin/console doctrine:database:create \
&& php bin/console doctrine:schema:create \
&& php bin/console doctrine:fixtures:load

EXPOSE 

CMD symfony local:server:start

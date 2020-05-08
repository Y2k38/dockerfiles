FROM php:7.2-fpm-alpine

COPY . /tmp/

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories

RUN apk add --no-cache $PHPIZE_DEPS \
    && tar -zxf /tmp/redis-5.2.2.tgz -C /tmp/ \
    && docker-php-ext-configure /tmp/redis-5.2.2 --enable-redis \
    && docker-php-ext-install /tmp/redis-5.2.2 \
    && tar -zxf /tmp/mongodb-1.7.4.tgz -C /tmp/ \
    && docker-php-ext-configure /tmp/mongodb-1.7.4 --enable-mongodb \
    && docker-php-ext-install /tmp/mongodb-1.7.4 \
    && tar -zxf /tmp/xdebug-2.9.5.tgz -C /tmp/ \
    && docker-php-ext-configure /tmp/xdebug-2.9.5 --enable-xdebug \
    && docker-php-ext-install /tmp/xdebug-2.9.5 \
    && tar -zxf /tmp/cphalcon-3.4.5.tgz -C /tmp/ \
    && docker-php-ext-configure /tmp/cphalcon-3.4.5/build/php7/64bits --enable-phalcon \
    && docker-php-ext-install /tmp/cphalcon-3.4.5/build/php7/64bits \
    && docker-php-ext-install pdo pdo_mysql bcmath \
    && docker-php-ext-enable opcache \
    && sed -i 's/listen = 127.0.0.1:9000/listen = 0.0.0.0:9000/g' /usr/local/etc/php-fpm.d/www.conf \
    && mv /tmp/php.ini-development /usr/local/etc/php/php.ini \
    && mv /tmp/composer /usr/local/bin/ \
    && apk del $PHPIZE_DEPS \
    && rm -rf /tmp/*

WORKDIR /var/www/html

FROM php:7.4-fpm

### User

USER root

### Change source

RUN sed -i "s/archive.ubuntu./mirrors.aliyun.com/g" /etc/apt/sources.list && \
    sed -i "s/deb.debian.org/mirrors.aliyun.com/g" /etc/apt/sources.list && \
    sed -i "s/security.debian.org/mirrors.aliyun.com/g" /etc/apt/sources.list

### Update source

RUN apt-get update -yqq && \
    apt-get install -yqq \
        apt-utils libzip-dev zip unzip

### Php extension

RUN docker-php-ext-install zip && \
    docker-php-ext-enable zip

RUN pecl install redis && \
    docker-php-ext-enable redis

RUN pecl install swoole && \
    docker-php-ext-enable swoole

### Set Timezone

ARG TZ=Asia/Shanghai
ENV TZ ${TZ}

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

### Composer

RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

WORKDIR /app
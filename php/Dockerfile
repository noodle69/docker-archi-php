FROM php:7.1-fpm-alpine

ENV PHPIZE_DEPS \
		autoconf \
		file \
		g++ \
		gcc \
		libc-dev \
		make \
		pkgconf \
		re2c

RUN apk add --no-cache --virtual .persistent-deps \
        ca-certificates \
        curl \
        unzip \
        git \
        tar \
        icu-dev \
        build-base \
        python-dev \
        py-pip \
        jpeg-dev \
        zlib-dev \
        xz

RUN set -xe \
    && apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS  \
        libxpm-dev \
        icu-dev \
    && docker-php-source extract \
    && docker-php-ext-configure mysqli --with-mysqli=mysqlnd \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
    && docker-php-ext-install exif mbstring intl zip mysqli pdo_mysql \
    && docker-php-ext-enable opcache \
    && yes | pecl install redis \
    && yes | pecl install memcached \
   && docker-php-source delete 

WORKDIR /var/www

CMD php-fpm

EXPOSE 9000

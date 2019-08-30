ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm-alpine

ARG REPOSITORIES_CDN
ARG PHP_EXTENSIONS

RUN if [ "${REPOSITORIES_CDN}" != "" ]; then \
        sed -i "s/dl-cdn.alpinelinux.org/${REPOSITORIES_CDN}/g" /etc/apk/repositories; \
        cat /etc/apk/repositories; \
    fi

RUN apk update; \
    apk add libjpeg-turbo-dev libpng-dev libwebp-dev freetype-dev libxpm-dev; \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-webp-dir=/usr/include/ --with-xpm-dir=/usr/include/; \
    docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-install -j$(nproc) ${PHP_EXTENSIONS}

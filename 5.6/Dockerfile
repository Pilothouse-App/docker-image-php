FROM php:5.6-fpm-alpine

RUN apk add --no-cache --virtual .build-deps \
	git autoconf g++ libtool make cyrus-sasl-dev imagemagick-dev libjpeg-turbo-dev libpng-dev libxml2-dev pcre-dev zlib-dev \
	&& docker-php-source extract

RUN apk add --no-cache imagemagick mysql-client \
	&& pecl install imagick \
	&& docker-php-ext-install calendar exif gd mysqli opcache pdo_mysql soap zip \
	&& docker-php-ext-enable imagick

RUN pecl install redis \
    && docker-php-ext-enable redis

RUN docker-php-source delete \
	&& apk del .build-deps

RUN apk add --no-cache less ssmtp

RUN ln -s /usr/local/vendor/wp-cli/wp-cli/bin/wp /usr/local/bin/wp
RUN mkdir -p /home/www-data/.wp-cli && chown -R www-data:www-data /home/www-data/.wp-cli

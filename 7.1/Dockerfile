FROM php:7.1-fpm-alpine

ENV COMPOSER_VERSION 1.5.2
ENV WP_CLI_VERSION 1.4.0

RUN apk add --no-cache --virtual .build-deps \
	git autoconf g++ libtool make cyrus-sasl-dev imagemagick-dev libjpeg-turbo-dev libpng-dev libxml2-dev pcre-dev zlib-dev \
	&& docker-php-source extract

RUN apk add --no-cache imagemagick mysql-client \
	&& pecl install imagick \
	&& docker-php-ext-configure gd --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install calendar exif gd mysqli opcache pdo_mysql soap zip \
	&& docker-php-ext-enable imagick

RUN pecl install redis \
	&& docker-php-ext-enable redis

RUN docker-php-source delete \
	&& apk del .build-deps

RUN apk add --no-cache bash git less ncurses ssmtp

RUN curl -sL -o composer.phar https://getcomposer.org/download/${COMPOSER_VERSION}/composer.phar \
	&& chmod +x composer.phar \
	&& mv composer.phar /usr/local/bin/composer \
	&& mkdir -p /home/www-data/.composer \
	&& chown -R www-data:www-data /home/www-data/.composer

RUN curl -sL -o wp-cli.phar https://github.com/wp-cli/wp-cli/releases/download/v${WP_CLI_VERSION}/wp-cli-${WP_CLI_VERSION}.phar \
	&& chmod +x wp-cli.phar \
	&& mv wp-cli.phar /usr/local/bin/wp \
	&& mkdir -p /home/www-data/.wp-cli \
	&& chown -R www-data:www-data /home/www-data/.wp-cli

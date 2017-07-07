FROM php:7.0-fpm-alpine

RUN apk add --no-cache --virtual .build-deps \
	git autoconf g++ libtool make cyrus-sasl-dev imagemagick-dev libmemcached-dev libjpeg-turbo-dev libpng-dev libxml2-dev pcre-dev zlib-dev \
	&& docker-php-source extract

RUN git clone https://github.com/websupport-sk/pecl-memcache.git /usr/src/php/ext/memcache/ \
	&& docker-php-ext-configure memcache \
	&& docker-php-ext-install memcache

RUN git clone --branch php7 https://github.com/php-memcached-dev/php-memcached /usr/src/php/ext/memcached/ \
	&& docker-php-ext-configure memcached \
	&& docker-php-ext-install memcached

RUN apk add --no-cache imagemagick libmemcached mysql-client \
	&& pecl install imagick \
	&& docker-php-ext-install calendar exif gd mysqli opcache pdo_mysql soap zip \
	&& docker-php-ext-enable imagick

RUN rm -rf /usr/src/php/ext/memcache \
	&& rm -rf /usr/src/php/ext/memcached \
	&& docker-php-source delete \
	&& apk del .build-deps

RUN apk add --no-cache bash less ncurses ssmtp

RUN curl -sL -o composer.phar https://getcomposer.org/download/1.4.2/composer.phar \
	&& chmod +x composer.phar \
	&& mv composer.phar /usr/local/bin/composer

RUN curl -sL -o wp-cli.phar https://github.com/wp-cli/wp-cli/releases/download/v1.2.1/wp-cli-1.2.1.phar \
	&& chmod +x wp-cli.phar \
	&& mv wp-cli.phar /usr/local/bin/wp \
	&& mkdir -p /home/www-data/.wp-cli \
	&& chown -R www-data:www-data /home/www-data/.wp-cli

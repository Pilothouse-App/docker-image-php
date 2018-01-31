FROM pilothouseapp/php:5.6-dev

RUN apk add --no-cache --virtual .build-deps \
	autoconf g++ make

RUN pecl install xdebug-2.5.5 && docker-php-ext-enable xdebug

RUN apk del .build-deps

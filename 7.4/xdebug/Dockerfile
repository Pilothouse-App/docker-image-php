FROM pilothouseapp/php:7.4-dev

RUN apk add --no-cache --virtual .build-deps \
	autoconf g++ make \
	&& pecl install xdebug-2.9.1 && docker-php-ext-enable xdebug \
	&& apk del .build-deps

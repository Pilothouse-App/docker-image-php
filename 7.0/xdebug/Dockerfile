FROM pilothouseapp/php:7.0-dev

RUN apk add --no-cache --virtual .build-deps \
	autoconf g++ make \
	&& pecl install xdebug-2.9.0 && docker-php-ext-enable xdebug \
	&& apk del .build-deps

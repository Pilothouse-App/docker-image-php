FROM pilothouseapp/php:7.3-dev

RUN apk add --no-cache --virtual .build-deps \
	autoconf g++ make \
	&& pecl install xdebug && docker-php-ext-enable xdebug \
	&& apk del .build-deps

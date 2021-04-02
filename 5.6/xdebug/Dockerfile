FROM pilothouse_php56:latest

RUN apk add --no-cache --virtual .build-deps \
	autoconf g++ make \
	&& pecl install xdebug-2.5.5 && docker-php-ext-enable xdebug \
	&& apk del .build-deps

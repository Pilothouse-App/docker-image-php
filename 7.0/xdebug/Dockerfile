FROM pilothouse_php70:latest

RUN apk add --no-cache --virtual .build-deps \
	autoconf g++ make \
	&& pecl install xdebug-3.0.3 && docker-php-ext-enable xdebug \
	&& apk del .build-deps

FROM php:8.1.11-fpm
MAINTAINER Leo "leolu9527@163.com"
# set timezome
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# multi-stage get composer
COPY --from=composer /usr/bin/composer /usr/bin/composer

COPY ./mongodb-1.14.1.tgz ./xdebug-3.1.5.tgz /tmp/

RUN pecl install /tmp/xdebug-3.1.5.tgz \
	&& docker-php-ext-enable xdebug

COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
COPY ./www.conf /usr/local/etc/php-fpm.d/www.conf
RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

#RUN usermod -u 1000 www-data

ARG APP_CODE_PATH

WORKDIR ${APP_CODE_PATH}

CMD php-fpm

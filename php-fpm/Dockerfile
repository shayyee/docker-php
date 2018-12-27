FROM php:7.1-fpm

MAINTAINER jiajiale <xiajia08@gmail.com>

COPY ./conf/conf.d/www.conf /usr/local/etc/php-fpm.d/www.conf
COPY ./conf/php.ini /usr/local/etc/php/php.ini
RUN rm -rf /usr/local/etc/php-fpm.d/zz-docker.conf

# module pdo mysqli gd bcmath sockets
RUN apt-get update -q && \
    apt-get install -y libpng-dev libfreetype6-dev libjpeg62-turbo-dev && \
    docker-php-ext-configure gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-enable gd && \
    docker-php-ext-install pdo pdo_mysql mysqli bcmath gd sockets

# module redis
RUN pecl install igbinary && \
    docker-php-ext-enable igbinary && \
    pecl install -o -f redis && \
    rm -rf /tmp/pear && \
    docker-php-ext-enable redis

# module swoole
RUN pecl install swoole && \
    docker-php-ext-enable swoole

VOLUME [ "/var/run/php" ]

CMD ["php-fpm"]

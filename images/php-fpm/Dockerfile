FROM laradock/php-fpm:7.0--1.2

MAINTAINER Larry Eitel <larry@eitel.com>

RUN \ 
    # Install the xdebug extension
    pecl install xdebug && \
    docker-php-ext-enable xdebug

COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini


#####################################
# ZipArchive:
#####################################

RUN \
    # Install the zip extension
    pecl install zip && \
    docker-php-ext-enable zip


RUN docker-php-ext-install opcache && \
    docker-php-ext-enable opcache



#
#--------------------------------------------------------------------------
# Final Touch
#--------------------------------------------------------------------------
#

ADD ./php.ini /usr/local/etc/php/conf.d
ADD ./php-fpm.conf /usr/local/etc/php-fpm.d/

RUN rm -r /var/lib/apt/lists/*

RUN usermod -u 1000 www-data

WORKDIR /var/www/html

CMD ["php-fpm"]

EXPOSE 9000
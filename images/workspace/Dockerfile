FROM phusion/baseimage:latest

MAINTAINER Larry Eitel <larry@eitel.com>

RUN DEBIAN_FRONTEND=noninteractive
RUN locale-gen en_US.UTF-8

ENV LANGUAGE=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV LC_CTYPE=UTF-8
ENV LANG=en_US.UTF-8
ENV TERM xterm

# Add the "PHP 7" ppa
RUN apt-get install -y software-properties-common && \
    add-apt-repository -y ppa:ondrej/php

#
#--------------------------------------------------------------------------
# Software's Installation
#--------------------------------------------------------------------------
#

# Install "PHP Extentions", "libraries", "Software's"
RUN apt-get update && \
    apt-get install -y --force-yes \
        php7.0-cli \
        php7.0-common \
        php7.0-curl \
        php7.0-json \
        php7.0-xml \
        php7.0-mbstring \
        php7.0-mcrypt \
        php7.0-mysql \
        # php7.0-pgsql \
        php7.0-sqlite \
        php7.0-sqlite3 \
        php7.0-zip \
        php7.0-memcached \
        php7.0-gd \
        php7.0-xdebug \
        pkg-config \
        php-dev \
        libcurl4-openssl-dev \
        libedit-dev \
        libssl-dev \
        libxml2-dev \
        xz-utils \
        libsqlite3-dev \
        sqlite3 \
        git \
        curl \
        vim \
        nano \
        telnet \
        # postgresql-client \
    && apt-get clean



#####################################
# Non-Root User:
#####################################

# Add a non-root user to prevent files being created with root permissions on host machine.
ARG PUID=1000
ARG PGID=1000
RUN groupadd -g $PGID wwwuser && \
    useradd -u $PUID -g wwwuser -m wwwuser



#####################################
# Composer:
#####################################

# Install composer and add its bin to the PATH.
RUN curl -s http://getcomposer.org/installer | php && \
    echo "export PATH=${PATH}:/var/www/laravel/vendor/bin" >> ~/.bashrc && \
    mv composer.phar /usr/local/bin/composer && \
    rm -f /etc/service/sshd/down

COPY ./composer.json /home/wwwuser/.composer/composer.json

# Make sure that ~/.composer belongs to wwwuser
RUN chown -R wwwuser:wwwuser /home/wwwuser/.composer

USER wwwuser


RUN composer global install && \
    # install global laravel installer
    composer global require "laravel/installer"


USER root

#####################################
# Node / NVM:
#####################################

ENV NVM_DIR /root/.nvm
ENV NVM_WWWUSER_DIR /home/wwwuser/.nvm
RUN \
    # Install nvm (A Node Version Manager)
    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.6/install.sh | bash && \
        . /root/.nvm/nvm.sh && \
        nvm install stable && \
        nvm use stable && \
        nvm alias stable && \
        npm install -g gulp bower vue-cli 



# Wouldn't execute when added to the RUN statement in the above block
# Source NVM when loading bash since ~/.profile isn't loaded on non-login shell
RUN \
    echo "" >> /home/wwwuser/.bashrc && \
    echo 'export NVM_DIR="/home/wwwuser/.nvm"' >> /home/wwwuser/.bashrc && \
    echo '[ -s "/home/wwwuser/.nvm/nvm.sh" ] && . "/home/wwwuser/.nvm/nvm.sh"  # This loads nvm' >> /home/wwwuser/.bashrc && \

    echo "" >> /root/.bashrc && \
    echo 'export NVM_DIR="/root/.nvm"' >> /root/.bashrc && \
    echo '[ -s "/root/.nvm/nvm.sh" ] && . "/root/.nvm/nvm.sh"  # This loads nvm' >> /root/.bashrc



#####################################
# Git Town:
#####################################
RUN \
    # clone git-town and set environment
    git clone https://github.com/Originate/git-town.git /root/git-town \
    && echo 'export PATH=$PATH:/root/git-town/src' >> /root/.bashrc \
    && echo 'export MANPATH=$MANPATH:/root/git-town/man' >> /root/.bashrc


#####################################
# Spark:
#####################################
RUN \
    # clone spark-installer and set environment
    git clone https://github.com/laravel/spark-installer.git /root/spark-installer \
    && cd /root/spark-installer \
    && composer install \
    && echo 'export PATH=$PATH:/root/spark-installer' >> /root/.bashrc


#
#--------------------------------------------------------------------------
# Final Touch
#--------------------------------------------------------------------------
#

# Clean up
USER root
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*







# Source the bash
RUN . ~/.bashrc

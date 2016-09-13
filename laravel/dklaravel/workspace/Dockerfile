FROM larryeitel/dk_workspace:v01
MAINTAINER Larry Eitel <larry@eitel.com>


ARG COMPOSER_GLOBAL_INSTALL=
ARG INSTALL_AEROSPIKE_EXTENSION=
ARG INSTALL_DRUSH=
ARG INSTALL_GIT_TOWN=
ARG INSTALL_LARAVEL_SPARK=
ARG INSTALL_MONGO=
ARG INSTALL_NODE=
ARG INSTALL_WORKSPACE_SSH=
ARG INSTALL_XDEBUG=
ARG NODE_VERSION=
ARG PGID=
ARG PUID=


COPY .dotfiles/* /root/
COPY .dotfiles/* /home/wwwuser/


#####################################
# xDebug:
#####################################
RUN sed -i 's/^/;/g' /etc/php/7.0/cli/conf.d/20-xdebug.ini

# RUN echo "alias phpunit='php -dzend_extension=xdebug.so /var/www/laravel/vendor/bin/phpunit'" >> ~/.bashrc

# ADD for REMOTE debugging
COPY ./xdebug.ini /etc/php/7.0/cli/conf.d/xdebug.ini


#####################################
# ssh:
#####################################

ADD insecure_id_rsa_dk /tmp/id_rsa
ADD insecure_id_rsa_dk.pub /tmp/id_rsa.pub
ADD known_hosts_dk /tmp/known_hosts

RUN cat /tmp/id_rsa.pub >> /root/.ssh/authorized_keys \
    && cat /tmp/id_rsa.pub >> /root/.ssh/id_rsa.pub \
    && cat /tmp/id_rsa >> /root/.ssh/id_rsa \
    && cat /tmp/known_hosts >> /root/.ssh/known_hosts \
    && rm -f /tmp/id_rsa* /tmp/known_hosts \
    && chmod 644 /root/.ssh/known_hosts /root/.ssh/authorized_keys /root/.ssh/id_rsa.pub \
    && chmod 400 /root/.ssh/id_rsa


# Set default work directory
WORKDIR /var/www/cpo

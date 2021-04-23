FROM debian:stretch-20210408-slim
RUN apt-get update && apt-get -y upgrade

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y install \
    curl zip unzip lynx-cur ssmtp rsyslog cron \
    apache2 libapache2-mod-php7.0 \
    php-pear \
    php7.0-curl \
    php7.0-mbstring \
    php7.0-mysql \
    php7.0-xdebug \
    php7.0-opcache \
    php7.0-xml \
    php7.0-gd

ENV APACHE_RUN_USER=www-data \
    APACHE_RUN_GROUP=www-data \
    APACHE_LOG_DIR=/var/log/apache2 \
    APACHE_LOCK_DIR=/var/lock/apache2 \
    APACHE_RUN_DIR=/var/run/apache2 \
    APACHE_PID_FILE=/var/run/apache2.pid

COPY ./rootfs /

RUN a2enmod remoteip && a2enconf remoteip && a2enmod php7.0 && a2enmod rewrite

RUN usermod -u 1000 www-data

WORKDIR /var/www/html
EXPOSE 80

CMD /usr/sbin/apache2ctl -D FOREGROUND

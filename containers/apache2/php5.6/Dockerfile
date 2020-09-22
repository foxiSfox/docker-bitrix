FROM debian:stretch-slim
RUN apt-get update && apt-get -y upgrade

ENV DEBIAN_FRONTEND noninteractive
# ?? lynx-cur rsyslog php-pear ssmtp
# ?? not found php7.2-mcrypt
RUN apt-get -y install apt-transport-https wget gnupg curl zip unzip ssmtp cron

RUN wget -O sury.gpg https://packages.sury.org/php/apt.gpg && apt-key add sury.gpg && rm sury.gpg
RUN echo "deb https://packages.sury.org/php/ stretch main" | tee /etc/apt/sources.list.d/php.list

RUN apt-get update && apt-get -y install \
    apache2 \
    libapache2-mod-php5.6 \
    php5.6-soap \
    php5.6-curl \
    php5.6-mbstring \
    php5.6-mysql \
    php5.6-xdebug \
    php5.6-opcache \
    php5.6-xml \
    php5.6-pdo-dblib \
    libpng-dev \
    php5.6-gd

ENV APACHE_RUN_USER=www-data \
    APACHE_RUN_GROUP=www-data \
    APACHE_LOG_DIR=/var/log/apache2 \
    APACHE_LOCK_DIR=/var/lock/apache2 \
    APACHE_RUN_DIR=/var/run/apache2 \
    APACHE_PID_FILE=/var/run/apache2.pid

COPY ./rootfs /

RUN a2enmod remoteip && a2enconf remoteip && a2enmod php5.6 && a2enmod rewrite

RUN usermod -u 1000 www-data

WORKDIR /var/www/html

CMD /usr/sbin/apache2ctl -D FOREGROUND

EXPOSE 80

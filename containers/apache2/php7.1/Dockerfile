FROM debian:bullseye-20221024-slim
RUN apt-get update && apt-get -y upgrade

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get -y install apt-transport-https wget gnupg curl zip unzip ssmtp cron

RUN wget -O sury.gpg https://packages.sury.org/php/apt.gpg && apt-key add sury.gpg && rm sury.gpg
RUN echo "deb https://packages.sury.org/php/ bullseye main" | tee /etc/apt/sources.list.d/php.list

RUN apt-get update && apt-get -y install \
    apache2 \
    libapache2-mod-php7.1 \
    php7.1-curl \
    php7.1-mbstring \
    php7.1-mysql \
    php7.1-xdebug \
    php7.1-opcache \
    php7.1-xml \
    php7.1-gd

ENV APACHE_RUN_USER=www-data \
    APACHE_RUN_GROUP=www-data \
    APACHE_LOG_DIR=/var/log/apache2 \
    APACHE_LOCK_DIR=/var/lock/apache2 \
    APACHE_RUN_DIR=/var/run/apache2 \
    APACHE_PID_FILE=/var/run/apache2.pid

COPY ./rootfs /

RUN a2enmod remoteip && a2enconf remoteip && a2enmod php7.1 && a2enmod rewrite

RUN usermod -u 1000 www-data

WORKDIR /var/www/html

CMD /usr/sbin/apache2ctl -D FOREGROUND

EXPOSE 80

FROM debian:bullseye-20230919-slim
RUN apt-get update && \
    apt-get upgrade -y

ENV DEBIAN_FRONTEND=noninteractive \
    APACHE_RUN_USER=www-data \
    APACHE_RUN_GROUP=www-data \
    APACHE_LOG_DIR=/var/log/apache2 \
    APACHE_LOCK_DIR=/var/lock/apache2 \
    APACHE_RUN_DIR=/var/run/apache2 \
    APACHE_PID_FILE=/var/run/apache2.pid

RUN apt-get install -y apt-transport-https gnupg wget curl rsyslog cron zip unzip ssmtp

RUN wget -O sury.gpg https://packages.sury.org/php/apt.gpg && apt-key add sury.gpg && rm sury.gpg && \
    wget -qO- https://packages.sury.org/php/apt.gpg | apt-key add - 2>/dev/null && \
    echo "deb https://packages.sury.org/php/ bullseye main" | tee /etc/apt/sources.list.d/php.list && \
    rm -rf /var/lib/apt/lists/*

RUN apt-get update && \
    apt-get -y install \
    apache2 \
    libapache2-mod-php8.1 \
    php8.1-curl \
    php8.1-mbstring \
    php8.1-mysql \
    php8.1-xdebug \
    php8.1-opcache \
    php8.1-xml \
    php8.1-gd

COPY ./rootfs /

RUN a2enmod remoteip && \
    a2enconf remoteip && \
    a2enmod php8.1 && \
    a2enmod rewrite && \
    update-alternatives --set php /usr/bin/php8.1 && \
    phpenmod -v 8.1 -s apache2 bitrixenv arealenv && \
    phpenmod -v 8.1 -s cli clienv && \
    echo "ServerName 127.0.0.1" >> /etc/apache2/apache2.conf && \
    usermod -u 1000 www-data && \
    touch /var/log/bitrix.log && \
    chown www-data:1000 /var/log/bitrix.log

WORKDIR /var/www/html
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
EXPOSE 80

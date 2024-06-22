
FROM nginx:1.25.1

ARG INSTALL_PHP_VERSION="8.2"

#sshd
RUN apt-get update && apt-get install -y openssh-server

RUN apt-get update && apt-get -y install sudo

RUN apt-get update && apt-get install -y lsb-release apt-transport-https ca-certificates wget
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/php.list
# php-fpm
RUN apt-get update && apt-get install -y php${INSTALL_PHP_VERSION}-fpm

# PHP
RUN apt-get update && apt-get install -y php${INSTALL_PHP_VERSION}-mysql php${INSTALL_PHP_VERSION}-xml php${INSTALL_PHP_VERSION}-xmlrpc \
    php${INSTALL_PHP_VERSION}-curl php${INSTALL_PHP_VERSION}-gd php${INSTALL_PHP_VERSION}-bcmath \
    php${INSTALL_PHP_VERSION}-cli php-dev php${INSTALL_PHP_VERSION}-imap php${INSTALL_PHP_VERSION}-mbstring \
    php${INSTALL_PHP_VERSION}-opcache php${INSTALL_PHP_VERSION}-soap php${INSTALL_PHP_VERSION}-zip unzip

# proxy、php-fpm
COPY ./config/docker_proxy.conf /etc/nginx/conf.d/default.conf
COPY ./config/php-fpm.conf /etc/php/${INSTALL_PHP_VERSION}/fpm/pool.d/zzz-www.conf

# 
COPY ./src /var/www/server

RUN mkdir -p /run/php
CMD /usr/sbin/php-fpm8.2 -D; nginx
RUN echo "exit 0" > /usr/sbin/policy-rc.d
CMD /etc/init.d/php8.2-fpm start && nginx -g "daemon off;"
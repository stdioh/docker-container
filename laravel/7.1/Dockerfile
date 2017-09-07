FROM php:7.1-apache

RUN apt-get update && apt-get install -y \
    libmcrypt-dev \
    curl \
    wget \
    git \
    zlib1g-dev \
    mysql-client \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install zip \
    && docker-php-ext-install pdo pdo_mysql

RUN echo 'export PHP=/usr/bin/php' >> /etc/bash.bashrc
ADD composer-install.sh /tmp/
RUN chmod +x /tmp/composer-install.sh
RUN /tmp/composer-install.sh
RUN a2enmod rewrite
ADD apache.conf /etc/apache2/sites-available
RUN a2dissite 000-default.conf
RUN a2ensite apache.conf
RUN service apache2 restart


WORKDIR /var/www/html

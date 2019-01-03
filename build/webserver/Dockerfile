FROM php:7.2.6-apache

RUN apt-get -y update --fix-missing
RUN apt-get upgrade -y

# Install useful tools
RUN apt-get install -y \
    apt-utils \
    wget \
    python-software-properties \
    vim \
    htop \
    curl \
    git

# Install Apache bits
RUN apt-get install -y \
    libapache2-mod-fastcgi \
    apache2-mpm-worker
RUN a2enmod actions fastcgi
RUN a2enmod rewrite

# Install PHP Extensions
RUN apt-get install -y \
    php7.2.6-fpm \
    php7.2.6-mysql \
    mcrypt \
    php7.2.6-mcrypt \
    php7.2.6-cli \
    php7.2.6-curl \
    php7.2.6-mbstring \
    php7.2.6-xml \
    php7.2.6-json \
    php7.2.6-cgi \
    php7.2.6-gd \
    php7.2.6-imagick \
    php7.2.6-bz2 \
    php7.2.6-zip

# PHP and apache together
RUN apt-get install -y \
    libapache2-mod-php7.2.6
RUN a2enconf php7.2.6-fpm
RUN service apache2 reload

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Drush
RUN composer global require drush/drush && \
    composer global update

#Drush Launcher
RUN wget -O drush.phar https://github.com/drush-ops/drush-launcher/releases/download/0.6.0/drush.phar
RUN chmod +x drush.phar
RUN sudo mv drush.phar /usr/local/bin/drush

#Pimp My Log
RUN composer require "potsky/pimp-my-log"

RUN a2enmod rewrite headers
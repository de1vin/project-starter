FROM phpdockerio/php72-fpm:latest
WORKDIR "/application"

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get -y --no-install-recommends install  php-memcached php7.2-mysql php7.2-pgsql php-redis php7.2-sqlite3 php-xdebug php7.2-bcmath php7.2-bz2 php7.2-gd php-imagick php7.2-intl php-mongodb php-yaml \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install git
#RUN apt-get update \
#    && apt-get -y install git \
#    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

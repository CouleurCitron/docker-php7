FROM php:7.0-apache

RUN a2enmod vhost_alias

RUN service apache2 restart


RUN apt-get update && apt-get install -y \
	mysql-client \
        libapache2-mod-fcgid \
 	&& docker-php-ext-install mysqli \
 	&& docker-php-ext-install pdo_mysql \
        && docker-php-ext-install mbstring


#CMD chown -R www-data:www-data /var/www/html

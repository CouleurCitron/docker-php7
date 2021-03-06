FROM php:7.0-apache

RUN a2enmod vhost_alias
RUN a2enmod rewrite

RUN service apache2 restart
	
# APC
RUN pear config-set php_ini /usr/local/etc/php/php.ini
RUN pecl config-set php_ini /usr/local/etc/php/php.ini
RUN pecl install apc redis memcached

RUN apt-get update && apt-get install -y \
		git \
        libmemcached-dev \
        libmemcached11 \
        mysql-client \
        libapache2-mod-fcgid \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	libmcrypt-dev \
	libpng12-dev \
	sendmail \
        libicu-dev \
 	&& docker-php-ext-install mysqli \
        && docker-php-ext-install zip \
        && docker-php-ext-install intl \
	&& docker-php-ext-install opcache \
 	&& docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mbstring \
	&& docker-php-ext-install -j$(nproc) iconv mcrypt \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install sockets
    
#Memcached support	
RUN git clone --branch php7 https://github.com/php-memcached-dev/php-memcached /usr/src/php/ext/memcached \
  && cd /usr/src/php/ext/memcached \
  && docker-php-ext-configure memcached \
  && docker-php-ext-install memcached

	
RUN ( \
    echo "opcache.memory_consumption=128"; \
    echo "opcache.interned_strings_buffer=8"; \
    echo "opcache.max_accelerated_files=4000"; \
    echo "opcache.revalidate_freq=60"; \
    echo "opcache.fast_shutdown=1"; \
    echo "opcache.enable_cli=1"; \
    echo "opcache.save_comments=1"; \
    ) > /usr/local/etc/php/conf.d/opcache-recommended.ini

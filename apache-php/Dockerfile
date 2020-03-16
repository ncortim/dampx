FROM php:7.4-apache

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

ENV APACHE_DOCUMENT_ROOT /var/www/mywebsite/public

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

RUN apt-get update \
&& apt-get install -y vim \
&& docker-php-ext-install mysqli \
&& pecl install xdebug-2.9.2 \
&& docker-php-ext-enable xdebug \
&& printf '[xdebug]\nzend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20190902/xdebug.so\nxdebug.remote_enable=1\nxdebug.remote_autostart=1\nxdebug.remote_connect_back=1\nxdebug.remote_port=9000\nxdebug.remote_host=192.168.178.34\n' >> /usr/local/etc/php/php.ini \
&& a2enmod rewrite
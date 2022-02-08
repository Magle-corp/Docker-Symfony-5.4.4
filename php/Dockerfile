FROM php:7.4-apache

# Set server name for Apache.
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

# Essential libraries.
RUN apt-get update \
    && apt-get install -y --no-install-recommends locales apt-utils git libicu-dev g++ libpng-dev libxml2-dev libzip-dev libonig-dev libxslt-dev;

# Locales.
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen && \
    locale-gen

# Download and move composer.
RUN curl -sSk https://getcomposer.org/installer | php -- --disable-tls && \
   mv composer.phar /usr/local/bin/composer

# PHP utiles.
RUN docker-php-ext-configure intl
RUN docker-php-ext-install pdo pdo_mysql gd opcache intl zip calendar dom mbstring zip gd xsl
RUN pecl install apcu && docker-php-ext-enable apcu

# Set working directory.
WORKDIR /var/www/

# Install.sh script.
COPY install.sh /web/install.sh
RUN chmod +x /web/install.sh

ENTRYPOINT ["/web/install.sh"]


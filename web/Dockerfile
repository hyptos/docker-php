FROM php:7.0.9-apache
# PHP extension
RUN requirements="zlib1g-dev libicu-dev git curl" \
    && apt-get update && apt-get install -y $requirements && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install intl \
    && docker-php-ext-install zip \
    && apt-get purge --auto-remove -y

# Apache & PHP configuration
RUN a2enmod rewrite
ADD docker/apache/vhost.conf /etc/apache2/sites-enabled/default.conf
ADD docker/php/php.ini /usr/local/etc/php/php.ini

# Add the application
ADD . /app
WORKDIR /app

# Ensure that the production container will run with the www-data user
RUN chown www-data /app

CMD ["/app/docker/apache/run.sh"]

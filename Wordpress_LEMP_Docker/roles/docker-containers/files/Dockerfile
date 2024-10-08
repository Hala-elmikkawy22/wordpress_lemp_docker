FROM php:8.2-fpm

# Install PHP extensions or other dependencies
RUN docker-php-ext-install mysqli pdo pdo_mysql

# Copy custom PHP configuration (if any)
COPY ./php.ini /usr/local/etc/php/php.ini

# Set working directory
WORKDIR /var/www/html

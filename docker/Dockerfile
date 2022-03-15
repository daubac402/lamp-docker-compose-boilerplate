FROM php:7.4-apache

COPY ./php/php.ini /usr/local/etc/php/
COPY ./apache/*.conf /etc/apache2/sites-enabled/

# Install system dependencies
RUN apt-get update && apt-get install -y \
    vim \
    zlib1g-dev \
    libpq-dev \
    mariadb-client \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    zip \
    unzip \
    && docker-php-ext-install zip pdo_mysql mysqli \
    && docker-php-ext-enable mysqli

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

# Set working directory
WORKDIR /var/www/html

# Enable apache modules
RUN a2enmod headers
RUN a2enmod ssl
RUN a2enmod rewrite
RUN a2enmod include
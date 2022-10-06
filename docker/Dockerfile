# Check available tags here: https://hub.docker.com/_/php/tags
FROM php:8.1.11-apache

# If you want to use `ll` in your container
RUN echo 'alias ll="ls -l"' >> ~/.bashrc

# Copy php.ini and apache configurations to the right destination in the container
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
    #
    # for php5.6
    # && docker-php-ext-install zip mysql mysqli pdo pdo_mysql mbstring exif pcntl bcmath gd \
    # && docker-php-ext-enable mysqli
    #
    # for php >= 7
    && docker-php-ext-install zip pdo_mysql mysqli mbstring exif pcntl bcmath gd \
    && docker-php-ext-enable mysqli

# Optional: If you want to work with Redis
# RUN pecl install -o -f redis \
#     &&  rm -rf /tmp/pear \
#     &&  docker-php-ext-enable redis

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Get latest Composer or specify a version (e.g. change: "latest" into "2.2") for using in the container
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
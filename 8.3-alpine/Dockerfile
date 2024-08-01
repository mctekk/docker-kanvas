FROM php:8.3-fpm-alpine

# Set working directory
WORKDIR /var/www/html

# Add docker php ext repo
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

# Install php extensions
RUN chmod +x /usr/local/bin/install-php-extensions && sync && \
    install-php-extensions mbstring pdo_mysql zip exif pcntl gd memcached redis swoole opcache curl readline sqlite3 msgpack igbinary pcov sockets

# Install dependencies
RUN apk update && apk add --no-cache \
    build-base \
    libpng-dev \
    libjpeg-turbo-dev \
    freetype-dev \
    musl-locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    unzip \
    git \
    curl \
    libmemcached-dev \
    nginx \
    vim \
    nodejs \
    npm

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Add user for laravel application
# RUN addgroup -g 1000 www
# RUN adduser -u 1000 -s /bin/sh --disabled-password -G www www 

# Copy code to /var/www
COPY --chown=www:www-data . /var/www/html

# PHP Error Log Files
RUN mkdir /var/log/php \
    touch /var/log/php/errors.log && chmod 777 /var/log/php/errors.log

EXPOSE 9000

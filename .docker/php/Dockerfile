ARG PHP_VERSION
FROM php:8.3-rc-fpm-alpine

# prepare and install additional packages
RUN echo '@legacy https://dl-cdn.alpinelinux.org/alpine/v3.12/community' >> /etc/apk/repositories \
    && apk add -U --no-cache \
        vim \
        wget \
        unzip \
        git \
        redis \
        imagemagick \
        curl \
        git \
    && rm -rf /var/cache/apk/* /tmp/* /var/tmp/* /usr/share/doc/* /usr/share/man/*

# Install PHP extensions using the mlocati script
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/
RUN chmod +x /usr/local/bin/install-php-extensions \
    && sync \
    && install-php-extensions ast \
        bz2 \
        calendar \
        exif \
        gd \
        igbinary \
        imagick \
        intl \
        mysqli \
        msgpack \
        pcntl \
        pdo_mysql \
        redis \
        opcache \
        xdebug \
        zip

# Install Composer globally
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# RUN composer install /var/www/html/whav2/composer.json --no-interaction --no-plugins --no-scripts

# Additional cleanup
RUN apk update && apk upgrade && apk add bash

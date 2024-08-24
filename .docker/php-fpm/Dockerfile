FROM php:8.2-fpm-alpine

WORKDIR /app

RUN apk add nano bash

RUN apk --no-cache add \
    libpng-dev \
    libjpeg-turbo-dev \
    freetype-dev \
    libzip-dev \
    zlib-dev \
    zip \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd mysqli pdo pdo_mysql zip

# Set the max execution time (in seconds), e.g., 300 seconds (5 minutes)
RUN echo "max_execution_time = 300" >> /usr/local/etc/php/conf.d/docker-php-max-execution-time.ini

RUN apk --no-cache add wget curl git && \
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('sha384', 'composer-setup.php') === 'dac665fdc30fdd8ec78b38b9800061b4150413ff2e3b6f88543c636f7cd84f6db9189d43a81e5503cda447da73c7e5b6') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    php -r "unlink('composer-setup.php');"

EXPOSE 9000

ENTRYPOINT ["php-fpm"]
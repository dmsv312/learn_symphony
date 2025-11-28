FROM php:8.3-fpm

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        git \
        curl \
        zip \
        unzip \
        libpq-dev \
        libicu-dev \
        libonig-dev \
        libzip-dev \
        libxml2-dev \
        pkg-config \
        nodejs \
        npm \
    && docker-php-ext-install pdo pdo_mysql zip opcache \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php \
    && php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && rm /tmp/composer-setup.php

WORKDIR /var/www/app

RUN { \
  echo "memory_limit=512M"; \
  echo "upload_max_filesize=32M"; \
  echo "post_max_size=32M"; \
  echo "date.timezone=UTC"; \
} > /usr/local/etc/php/conf.d/custom.ini

CMD ["php-fpm"]

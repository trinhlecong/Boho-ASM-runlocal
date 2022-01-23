FROM webdevops/php-nginx:7.3

# Install Laravel framework system requirements (https://laravel.com/docs/7.x/installation#server-requirements)
RUN apt update \
    && apt install -y \
        libxml2-dev

RUN docker-php-ext-install \
        bcmath \
        ctype \
        fileinfo \
        json \
        mbstring \
        pdo_mysql \
        tokenizer \
        xml

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ENV WEB_DOCUMENT_ROOT /app/public
ENV APP_ENV production
ENV APP_DEBUG=false

WORKDIR /app

COPY ./src .

# Composer install packages
RUN composer install

# Extra entrypoints
COPY ./docker/api/entrypoint.sh /opt/docker/provision/entrypoint.d/.

RUN chown -R application:application .

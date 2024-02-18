FROM php:8.3-cli AS builder

WORKDIR /var/www

RUN apt-get update && \
    apt-get install libzip-dev -y && \
    docker-php-ext-install zip


RUN mkdir app


FROM php:8.3-fpm-alpine

WORKDIR /var/www

COPY --from=builder /var/www/app html

RUN ln -sf public html

RUN chown -R www-data:www-data /var/www

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

EXPOSE 9000

CMD [ "php-fpm" ]
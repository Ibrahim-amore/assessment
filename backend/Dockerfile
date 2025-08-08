FROM php:8.1-cli

RUN apt-get update && apt-get install -y git unzip libzip-dev zip libpng-dev libonig-dev libxml2-dev curl
RUN docker-php-ext-install pdo pdo_mysql mbstring bcmath exif

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html
COPY . .
RUN composer install --no-interaction --prefer-dist || true

EXPOSE 8000
CMD ["sh", "-c", "php artisan migrate --force || true; php artisan serve --host=0.0.0.0 --port=8000"] 

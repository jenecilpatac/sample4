FROM php:8.1-fpm-alpine

# Install system dependencies
RUN apk --no-cache add \
    libpng libjpeg-turbo libwebp freetype \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd \
    && docker-php-ext-install pdo pdo_mysql

# Set working directory
WORKDIR /var/www

# Install Composer (Laravel's dependency manager)
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Copy your Laravel project into the container
COPY . /var/www

# Set file permissions (optional)
RUN chown -R www-data:www-data /var/www

# Expose PHP-FPM port
EXPOSE 9000

CMD ["php-fpm"]

FROM php:8.2-fpm

# Install dependencies
RUN apt update && apt install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    unzip  # Required for Composer installation
RUN apt clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

# Install Composer globally
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set the working directory where the app will live
WORKDIR /var/www

# Copy the application files (including composer.json) into the container
COPY . .

# Install PHP dependencies using Composer (this will populate the 'vendor' directory)
RUN composer install --no-interaction --prefer-dist

# Set permissions for the 'vendor' directory and other necessary directories
RUN chown -R www-data:www-data /var/www

# Expose the port the app will run on
EXPOSE 9000

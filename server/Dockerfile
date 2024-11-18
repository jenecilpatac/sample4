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

# Set the working directory where the app will live
WORKDIR /var/www

# Copy the current directory contents into the container at /var/www
COPY . .


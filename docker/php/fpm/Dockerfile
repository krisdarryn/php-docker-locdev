FROM php:7.3-fpm

# Update apt-get
RUN apt-get update -qq

# Install nano and vim
RUN apt-get install -y nano \
    && nano --version \
    && apt-get install -y vim \
    && vi --version

# Install required PHP extensions
RUN apt-get update && apt-get install -y libpng-dev libjpeg-dev libpq-dev libzip-dev zip \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
    && docker-php-ext-install gd mbstring opcache pdo pdo_mysql pdo_pgsql zip mysqli

# Install drush.
# Download Drush 8.1.16 from github.com/drush-ops/drush/releases.
RUN php -r "readfile('https://github.com/drush-ops/drush/releases/download/8.3.2/drush.phar');" > drush
# Test your install.
RUN php drush core-status
# Make `drush` executable as a command from anywhere. Destination can be anywhere on $PATH.
RUN chmod +x drush
RUN mv drush /usr/local/bin

# Install Node.js and npm.
# Refer to https://github.com/nodesource/distributions#debinstall for specific version to use.
RUN apt-get update && apt-get install curl \
  && curl -sL https://deb.nodesource.com/setup_13.x | bash \
  && apt-get install -y nodejs \
  && node -v \
  && npm -v

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

WORKDIR /var/www/html
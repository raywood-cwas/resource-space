# Use the official image as a parent image
FROM mcr.microsoft.com/vscode/devcontainers/base:ubuntu

# Install necessary packages
RUN apt-get update && apt-get install -y \
    apache2 \
    mysql-server \
    php \
    php-mysql \
    php-gd \
    php-cli \
    libapache2-mod-php \
    subversion \
    wget \
    cron \
    imagemagick \
    ffmpeg

# Enable Apache mods
RUN a2enmod php7.4
RUN a2enmod rewrite

# Set up the Apache server
COPY apache-config.conf /etc/apache2/sites-available/000-default.conf

# Set up the MySQL server
RUN sed -i 's/bind-address/#bind-address/' /etc/mysql/mysql.conf.d/mysqld.cnf

# Expose ports for Apache and MySQL
EXPOSE 80 3306

# Start services
CMD service mysql start && service apache2 start && bash
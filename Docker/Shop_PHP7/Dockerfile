FROM php:7-apache

# enable apache2 modules
RUN a2enmod rewrite
RUN a2enmod ssl

# update package list
RUN apt-get update

# install default binaries
RUN apt-get install -y \
        ant \
        curl \
        git \
        unzip \
        libfreetype6-dev \
        libjpeg-dev \
        libpng12-dev \
        libssl-dev \
        libxml2-dev \
        mysql-client \
        openjdk-7-jdk \
        wget \
        zlib1g-dev

# install npm
RUN curl -sL https://deb.nodesource.com/setup_4.x | bash -
RUN apt-get install -y nodejs

# remove apt lists
RUN rm -rf /var/lib/apt/lists/*

# install php extentions
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-png-dir=/usr --with-jpeg-dir=/usr 
RUN docker-php-ext-install gd mysqli zip mbstring pdo pdo_mysql soap ftp opcache
RUN pecl install apcu
RUN docker-php-ext-enable apcu
RUN pecl install xdebug
RUN touch /usr/local/etc/php/conf.d/xdebug.ini; \
    echo xdebug.remote_enable=1 >> /usr/local/etc/php/conf.d/xdebug.ini; \
    echo xdebug.remote_autostart=0 >> /usr/local/etc/php/conf.d/xdebug.ini; \
    echo xdebug.remote_connephpct_back=1 >> /usr/local/etc/php/conf.d/xdebug.ini; \
    echo xdebug.remote_port=9000 >> /usr/local/etc/php/conf.d/xdebug.ini; \
    echo xdebug.remote_log=/tmp/php5-xdebug.log >> /usr/local/etc/php/conf.d/xdebug.ini;

# install composer
ENV COMPOSER_HOME /root/composer
ENV COMPOSER_VERSION 1.0.0-alpha10

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=${COMPOSER_VERSION}
 
# install grunt
RUN npm install -g grunt-cli

#install bower
RUN npm install -g bower


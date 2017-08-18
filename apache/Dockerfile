FROM php:7.1.7-apache

RUN apt-get update && apt-get install -y --no-install-recommends \
        curl \        
        libz-dev \
        libpq-dev \
        libjpeg-dev \
        libssl-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libmemcached-dev \
        libxml2-dev \
        php-soap \
        zlib1g-dev \
        libicu-dev \
        g++ \
        git

## Install mcrypt and gd
RUN docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd 

## Install Mysql and mysql PDO
RUN docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql 

## Install Postgres 
RUN docker-php-ext-install pdo_pgsql

## Install Soap
RUN docker-php-ext-install soap 

## Install XDEBUG
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug 

## Install Mongodb
RUN pecl install mongodb \
    && docker-php-ext-enable mongodb 

## Install ZIP
RUN docker-php-ext-install zip 

## Install BCMATH
RUN docker-php-ext-install bcmath 

## Install Exif
RUN docker-php-ext-install exif 

## Install TOKENIZER
RUN docker-php-ext-install tokenizer 

## Install Human Language and Character Encodeing Support

RUN docker-php-ext-configure intl \
    && docker-php-ext-install intl 

## Install Redis
RUN pecl install -o -f redis \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis 

## Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

## Install NodeJS and NVM
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - \
    && apt install nodejs \
    && apt install build-essential 

## Install Gulp
RUN npm install -g gulp

## Install wkhtml
RUN apt install wget unzip libaio1 xvfb libfontconfig wkhtmltopdf -y


## Download Oracle instantclient
RUN wget https://s3.amazonaws.com/simonetti-tests/oci8/instantclient-basic-linux.x64-12.1.0.2.0.zip \
    && wget https://s3.amazonaws.com/simonetti-tests/oci8/instantclient-sdk-linux.x64-12.1.0.2.0.zip \
    && unzip instantclient-sdk-linux.x64-12.1.0.2.0.zip \
    && unzip instantclient-basic-linux.x64-12.1.0.2.0.zip \
    && mkdir -p /usr/lib/oracle/12.1/client64 \
    && mv instantclient_12_1/ /usr/lib/oracle/12.1/client64/lib \
    && ln -s /usr/lib/oracle/12.1/client64/lib/libclntsh.so.12.1 /usr/lib/oracle/12.1/client64/lib/libclntsh.so \
    && ln -s /usr/lib/oracle/12.1/client64/lib/libocci.so.12.1 /usr/lib/oracle/12.1/client64/lib/libocci.so 

## Install PHP oci8 extenstion
RUN ldconfig \
    && pecl install oci8 \
    && echo "extension=/usr/local/lib/php/extensions/no-debug-non-zts-20160303/oci8.so" >> /usr/local/etc/php/conf.d/oci8.ini


## Download wkhtmltopdf
RUN wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz \
    && tar -xvf wkhtmltox-0.12.4_linux-generic-amd64.tar.xz \
    && mv wkhtmltox /opt
    
## Enable appache rewrite mode
RUN a2enmod rewrite

## INSTALL BZip
RUN apt-get install -y libbz2-dev
RUN docker-php-ext-install bz2

# INSTALL VIM
RUN apt-get install -y vim

RUN usermod -u 1000 www-data
RUN chown -R www-data:www-data /var/www

WORKDIR /var/www/html

EXPOSE 80
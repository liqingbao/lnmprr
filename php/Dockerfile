FROM php:fpm-stretch

COPY ./etc/apt/sources.list /etc/apt/sources.list

# Set Environment Variables
ENV DEBIAN_FRONTEND noninteractive

# Extensions: ctype, dom, fileinfo, ftp, hash, iconv, json, pdo, pdo_sqlite, session,
# tokenizer, simplexml, xml, xmlreader, xmlwriter and phar are bundled and compiled into
# PHP by default. If missing, install them directly by `docker-php-ext-install extension_name`

# Notice:
# 1. Mcrypt was DEPRECATED in PHP 7.1.0, and REMOVED in PHP 7.2.0.
# 2. opcache requires PHP version >= 7.0.0.
# 3. soap requires libxml2-dev.
# 4. xml, xmlrpc, wddx require libxml2-dev and libxslt-dev.

RUN apt-get update \
    && apt-get install -y --no-install-recommends apt-utils wget unzip\
    && apt-get install -yqq libfreetype6-dev libjpeg62-turbo-dev libpng-dev librabbitmq-dev libicu-dev libbz2-dev libzip-dev curl\
    && pecl channel-update pecl.php.net \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install bcmath \
    # 压缩
    && docker-php-ext-install bz2 \
    # 日历扩展包含了简化不同日历格式间的转换的函数。
    # && docker-php-ext-install calendar \
    # 可交换图像信息
    # && docker-php-ext-install exif \
    # sockets
    && docker-php-ext-install sockets \
    # 国际化扩展
    # must install libicu-dev first
    # && docker-php-ext-install intl \
    # 国际化您的PHP程序 http://php.net/manual/zh/intro.gettext.php
    # && docker-php-ext-install gettext \
    # IMAP 这些函数提供了可以操作 IMAP 以及 NNTP，POP3 和本地邮箱的方法。
    && apt-get install -y libc-client-dev libkrb5-dev\
    && rm -r /var/lib/apt/lists/* \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install imap \
    # IMAP
    # OPCACHE
    # && docker-php-ext-install opcache \
    # OPCACHE
    # xdebug
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    # xdebug
    # redis
    && pecl install redis \
    # && docker-php-ext-enable redis \
    # extension=redis.so
    # redis
    # amqp
    && pecl install amqp \
    # && docker-php-ext-enable amqp \
    # extension=amqp.so
    # amqp
#   && pecl install pdo_msql \
    && docker-php-ext-install pdo pdo_mysql\
    # zip extension
    && pecl install zip \
    # mongodb
    && pecl install mongodb  \
    && docker-php-ext-enable mongodb \
    # pcntl
    && docker-php-ext-install pcntl \
    # install composer
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

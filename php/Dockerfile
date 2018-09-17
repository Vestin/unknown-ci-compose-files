FROM php:7.2-fpm

# source change to aliyun
# RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak
# ADD ./sources.list /etc/apt

# timezone set
ENV TIMEZONE Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TIMEZONE /etc/localtime
RUN echo $TIMEZONE > /etc/timezone

RUN apt-get update && apt-get install -y --allow-unauthenticated \
    git \
    vim \
    openssl \
    zip \
    libpng-dev libjpeg-dev libfreetype6-dev 

RUN docker-php-ext-configure gd --with-jpeg-dir=/usr/lib/x86_64-linux-gnu/ --with-freetype-dir=/usr/lib/x86_64-linux-gnu/ --with-png-dir=/usr/lib/x86_64-linux-gnu/

RUN docker-php-ext-install pdo_mysql gd zip


# composer install
RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" && \
php composer-setup.php && \
php -r "unlink('composer-setup.php');" && \
mv composer.phar /usr/local/bin/composer && \
# source change to china mirror
# composer config -g repo.packagist composer https://packagist.phpcomposer.com && \
composer self-update
# composer path
ENV PATH="/root/.composer/vendor/bin:${PATH}"

#clean
RUN apt-get clean

# php config
ADD php-fpm.conf    /usr/local/etc/php-fpm.conf

WORKDIR /opt

# Write Permission
RUN usermod -u 1000 www-data

EXPOSE 9000
VOLUME ["/opt"]
FROM php:7.2-fpm

#
#--------------------------------------------------------------------------
# Software's Installation
#--------------------------------------------------------------------------
#
# Installing tools and PHP extentions using "apt", "docker-php", "pecl",
#

# Install "curl", "libmemcached-dev", "libpq-dev", "libjpeg-dev",
#         "libpng-dev", "libfreetype6-dev", "libssl-dev", "libmcrypt-dev",
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    curl \
    libmemcached-dev \
    libz-dev \
    libpq-dev \
    libjpeg-dev \
    libpng-dev \
    libfreetype6-dev \
    libssl-dev \
    libmcrypt-dev \
  && rm -rf /var/lib/apt/lists/*



# Install the PHP pdo_mysql extention
RUN docker-php-ext-install pdo_mysql \
# Install the PHP pdo_pgsql extention
&& docker-php-ext-install pdo_pgsql \
# Install the PHP gd library
&& docker-php-ext-configure gd \
  --enable-gd-native-ttf \
  --with-jpeg-dir=/usr/lib \
  --with-freetype-dir=/usr/include/freetype2 && \
  docker-php-ext-install gd


# Install Php Redis Extension
RUN printf "\n" | pecl install -o -f redis \
  &&  rm -rf /tmp/pear \
  &&  docker-php-ext-enable redis

# Install the zip extension
RUN docker-php-ext-install zip

# Install opcache
RUN docker-php-ext-install opcache

# Install Mysqli Modifications
RUN docker-php-ext-install mysqli

# Install Tokenizer Modifications
RUN docker-php-ext-install tokenizer

# Install intl and requirements
RUN apt-get update -yqq && \
  apt-get install -y zlib1g-dev libicu-dev g++ && \
  docker-php-ext-configure intl && \
  docker-php-ext-install intl

# Install Image optimizers
RUN apt-get install -y --force-yes jpegoptim optipng pngquant gifsicle


USER root

RUN apt-get install -y libmagickwand-dev imagemagick && \
  pecl install imagick && \
  docker-php-ext-enable imagick


#
#--------------------------------------------------------------------------
# Final Touch
#--------------------------------------------------------------------------
#

COPY ./myphp.ini /usr/local/etc/php/conf.d
COPY ./xmy.pool.conf /usr/local/etc/php-fpm.d/

USER root

# Clean up
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    rm /var/log/lastlog /var/log/faillog

RUN usermod -u 1000 www-data

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000

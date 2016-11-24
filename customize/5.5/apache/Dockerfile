FROM php:5.5.38-apache

RUN apt-get update

# install font WenQuanYi-Micro-Hei
RUN apt-get -qqy --no-install-recommends install ttf-wqy-microhei

# timezone
RUN echo "Asia/Shanghai" | tee /etc/timezone && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# install libs
RUN apt-get install -qqy --no-install-recommends \
  ImageMagick \
  libmagick++-dev \
  libmagickcore-dev \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libmcrypt-dev \
  libpng12-dev \
  libssl-dev
RUN apt-get install -qqy --no-install-recommends wget

# install ext within official image
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install \
  gd \
  bcmath \
  mbstring \
  mcrypt \
  mysql \
  mysqli \
  pdo_mysql \
  zip

# mongo
RUN cd ~ \
  && wget http://pecl.php.net/get/mongo-1.6.14.tgz \
  && tar zvxf mongo-1.6.14.tgz \
  && cd mongo-1.6.14 \
  && phpize \
  && ./configure \
  && make \
  && make install \
  && make clean

# imagick
RUN cd ~ \
  && wget http://pecl.php.net/get/imagick-3.4.1.tgz \
  && tar zvxf imagick-3.4.1.tgz \
  && cd imagick-3.4.1 \
  && phpize \
  && ./configure \
  && make \
  && make install \
  && make clean

# memcache
RUN cd ~ \
  && wget http://pecl.php.net/get/memcache-2.2.7.tgz \
  && tar zvxf memcache-2.2.7.tgz \
  && cd memcache-2.2.7 \
  && phpize \
  && ./configure \
  && make \
  && make install \
  && make clean

COPY php.ini /usr/local/etc/php

# enable apache rewrite
RUN ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/rewrite.load

# install additional tools
RUN apt-get install -qqy --no-install-recommends curl vim zip unzip

# clean
RUN  apt-get autoclean \
  && apt-get autoremove \
  && rm -rf /var/lib/apt/lists/* \
  && cd ~ \
  && rm -rf * 

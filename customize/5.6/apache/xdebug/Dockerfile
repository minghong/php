FROM registry.aliyuncs.com/syncxplus/php:5.6.28
RUN wget https://github.com/xdebug/xdebug/archive/XDEBUG_2_4_1.zip \
  && unzip XDEBUG_2_4_1.zip \
  && cd xdebug-XDEBUG_2_4_1 \
  && phpize \
  && ./configure --enable-xdebug \
  && make \
  && make install \
  && make clean
RUN cd ~ && rm -rf *
COPY php.ini /usr/local/etc/php

FROM registry.aliyuncs.com/syncxplus/php:5.5.38
RUN wget https://github.com/syncxplus/xdebug/archive/XDEBUG_2_3_3.zip \
  && unzip XDEBUG_2_3_3.zip \
  && cd xdebug-XDEBUG_2_3_3 \
  && phpize \
  && ./configure --enable-xdebug \
  && make \
  && make install \
  && make clean
RUN cd ~ && rm -rf *
COPY php.ini /usr/local/etc/php

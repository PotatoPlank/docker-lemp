FROM php:7.2-fpm


# Get PHP Extensions
RUN apt-get update \
  && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libmcrypt-dev git curl zip unzip libxml2-dev libssh2-1-dev \
  && docker-php-ext-install pdo_mysql mysqli mbstring gd iconv soap sockets zip \
  && pecl install xdebug ssh2-1.1.2 \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) gd \
  && docker-php-ext-enable xdebug ssh2
  
# Get ImageMagick
# -- Installs and enables ImageMagick for PHP (may not always be required except when doing specific tasks on your local machine)
RUN  apt-get install -y libmagickwand-6.q16-dev --no-install-recommends \
  && ln -s /usr/lib/x86_64-linux-gnu/ImageMagick-6.8.9/bin-Q16/MagickWand-config /usr/bin \
  && pecl install imagick

# Get Linux Golang Image
 # -- Required for Mailhog
RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
 
 # Get Mailhog
 # -- Sends mail to http://localhost:8025/ (for debugging PHP mail sends)
 RUN go get github.com/mailhog/mhsendmail
 RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail


#Get composer
RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

COPY php.ini /usr/local/etc/php/

RUN groupadd -g 1002 testuser
RUN useradd -ms /bin/bash testuser -u 1002 -g 1002
USER testuser

WORKDIR /var/www

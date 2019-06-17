FROM php:5.6-fpm-alpine
MAINTAINER Arvin Karimi

# Install build tools
RUN apk --update upgrade \
    && apk add --no-cache autoconf automake make gcc g++ libtool postgresql-libs postgresql-dev php5-cli libxml2-dev\
    pkgconfig libmcrypt-dev re2c libressl libressl-dev ca-certificates \
     php5-bcmath php5-curl php5-mcrypt php5-opcache php5-mysql\
    php5-pgsql php5-soap php5-xml\
    rabbitmq-c rabbitmq-c-dev \
    nginx supervisor tzdata \
    && update-ca-certificates 

# Compile rabbitmq lib for php
RUN pecl install amqp sockets \
&& docker-php-ext-install pcntl bcmath sockets mcrypt pgsql pdo_pgsql mysql soap \
&& docker-php-ext-enable amqp pcntl bcmath sockets mcrypt mysql soap 

# install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer \
# composer install parallel
&& composer global require hirak/prestissimo

# Configure PHP
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" \
&& sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php5/php.ini \
&& sed -i "s/;date.timezone.*/date.timezone=Asia\/Tehran/" /etc/php5/php.ini \ 
&& sed -i "s/memory_limit.*/memory_limit=256M/" /etc/php5/php.ini \
&& sed -i "s/max_execution_time.*/max_execution_time=300/" $PHP_INI_DIR/php.ini \
&& sed -i "s/;date.timezone.*/date.timezone=Asia\/Tehran/" $PHP_INI_DIR/php.ini \
&& sed -i "s/memory_limit.*/memory_limit=256M/" $PHP_INI_DIR/php.ini 

ENV TZ=Asia/Tehran

RUN mkdir -p /var/run/php \
&& mkdir -p /var/run/nginx \
&& mkdir -p /etc/supervisor.d

COPY ./conf/php-fpm5.6-site.conf /usr/local/etc/php-fpm.d/www.conf
ADD ./conf/supervisord.conf /etc/supervisor.d/
ADD ./conf/test.nginx.conf /etc/nginx/conf.d/default.conf
RUN rm -rf /usr/local/etc/php-fpm.d/zz-docker.conf

## test
ADD ./conf/index.php /var/www/html
# ADD ./conf/site.conf /etc/nginx/conf.d/


# # RUN chown -R :www-data
#
VOLUME /etc/nginx/conf.d
# VOLUME /etc/nginx/certs

EXPOSE 80 443

CMD ["/usr/bin/supervisord","-c","/etc/supervisor.d/supervisord.conf"]



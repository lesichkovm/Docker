# usage
# docker run -d -v /you/laravel/folder:/var/www/laravel -p 80:80 -p 443:443 toninho09/apache-laravel
FROM ubuntu:16.04
MAINTAINER Antonio <antoniohls@gmail.com>

COPY endpoint.sh /endpoint.sh

RUN apt-get update \
&& apt-get -y install git curl nginx php7.0-fpm php7.0-soap php7.0-mysql php7.0-curl php7.0-gd php7.0-intl php-pear php-imagick php7.0-imap php7.0-mcrypt php-memcache php-pgsql \
php7.0-pspell php7.0-recode php7.0-sqlite3 php7.0-tidy php7.0-xmlrpc php7.0-xsl php7.0-mbstring php-gettext php7.0-odbc php7.0-sybase php7.0-xml php7.0-json php7.0-zip tdsodbc php-mbstring \
&& apt-get -y autoremove \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* \
&& mkdir -p /run/php \
&& /usr/bin/curl -sS https://getcomposer.org/installer | /usr/bin/php \
&& /bin/mv composer.phar /usr/local/bin/composer \
&& chmod +x \endpoint.sh \
&& rm /etc/nginx/sites-available/default


ADD 000-laravel.conf /etc/nginx/sites-available/
#ADD 001-laravel-ssl.conf /etc/nginx/sites-available/
COPY freetds.conf /etc/freetds/freetds.conf

RUN ln -s /etc/nginx/sites-available/000-laravel.conf /etc/nginx/sites-enabled/000-laravel.conf

COPY 20-xdebug.ini /etc/php/7.0/cli/conf.d/20-xdebug.ini

WORKDIR /

EXPOSE 80
EXPOSE 443

CMD ["./endpoint.sh"]
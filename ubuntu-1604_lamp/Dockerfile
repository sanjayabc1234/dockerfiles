FROM ubuntu:16.04

MAINTAINER Sanjay Maurya <sanjayabc1234@gmail.com>

LABEL Description = "Version 7 new dc setup based on Ubuntu 16.04 LTS. It includes LAMP stack tailored for new dc. Usage='docker run -p [HOST WWW PORT NUMBER]:80 -v [HOST WWW DOCUMENT ROOT]:/var/www/html ubuntu:16.04 bash'"

RUN apt-get update

RUN apt-get install apt-utils -y
RUN apt-get install -y zip unzip
RUN apt-get install -y nano

RUN apt-get install apache2 libapache2-mod-php7.0 -y
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

RUN echo '<IfModule mod_dir.c>\n\t\tDirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm\n</IfModule>'

RUN a2enmod rewrite
RUN chown -R www-data:www-data /var/www/html
RUN service apache2 restart

RUN apt-get install -y \
	php7.0 \
	php7.0-bz2 \
	php7.0-cgi \
	php7.0-cli \
	php7.0-common \
	php7.0-curl \
	php7.0-dev \
	php7.0-enchant \
	php7.0-fpm \
	php7.0-gd \
	php7.0-gmp \
	php7.0-imap \
	php7.0-interbase \
	php7.0-intl \
	php7.0-json \
	php7.0-ldap \
	php7.0-mbstring \
	php7.0-mcrypt \
	php7.0-mysql \
	php-mongodb \
	php7.0-odbc \
	php7.0-opcache \
	php7.0-pgsql \
	php7.0-phpdbg \
	php7.0-pspell \
	php7.0-readline \
	php7.0-recode \
	php7.0-sqlite3 \
	php7.0-sybase \
	php7.0-tidy \
	php7.0-xmlrpc \
	php7.0-xsl \
	libsasl2-dev \
	php7.0-zip

RUN pecl install mongodb

RUN echo "extension=mongodb.so" > /etc/php/7.0/fpm/conf.d/20-mongodb.ini && \
	echo "extension=mongodb.so" > /etc/php/7.0/cli/conf.d/20-mongodb.ini && \
	echo "extension=mongodb.so" > /etc/php/7.0/mods-available/mongodb.ini

COPY index.php /var/www/html/
COPY run-lamp.sh /usr/sbin/
RUN chmod +x /usr/sbin/run-lamp.sh

VOLUME /var/www/html
VOLUME /var/log/httpd
VOLUME /etc/apache2

#RUN groupadd dev
#RUN useradd -r -u 1000 -g dev dev
#USER dev
#ENTRYPOINT ["sleep", "infinity"]

CMD ./usr/sbin/run-lamp.sh

#docker build . -t ubuntu-php7:16.04
#RUN chown -R www-data:www-data /var/www/html
#docker run -it -p 8080:80 -v /home/docker:/var/www/html/ ubuntu-php7:16.04 bash
#https://www.jujens.eu/posts/en/2017/Jul/02/docker-userns-remap/
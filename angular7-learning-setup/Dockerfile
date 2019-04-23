FROM ubuntu:18.04

MAINTAINER Sanjay Maurya <sanjayabc1234@gmail.com>

LABEL Description = "Angular 7 practice with Book Pro Angular 6, 3rd Edition"

RUN echo "LC_ALL=en_US.UTF-8" >> /etc/environment
RUN echo "LANG=en_US.UTF-8" >> /etc/environment
RUN echo "NODE_ENV=development" >> /etc/environment
RUN more "/etc/environment"


RUN apt-get update
RUN apt-get install curl htop git zip nano ncdu build-essential chrpath libssl-dev libxft-dev pkg-config glib2.0-dev libexpat1-dev gobject-introspection python-gi-dev apt-transport-https libgirepository1.0-dev libtiff5-dev libjpeg-turbo8-dev libgsf-1-dev fail2ban nginx -y


# Install Node.js
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash
RUN apt-get install --yes nodejs
RUN node -v
RUN npm -v

# Cleanup
RUN apt-get update && apt-get upgrade -y && apt-get autoremove -y

#RUN mkdir /var/www/html/

RUN apt-get install -y sudo
RUN echo "root:ser_123" | chpasswd

RUN groupadd dev
RUN useradd -d /home/dev -u 1000 -g dev dev
RUN echo 'dev:ser_123' | chpasswd
RUN usermod -aG sudo dev

RUN chown -R "dev:dev" /var/www/
RUN chown -R "dev:dev" /home/

USER dev
WORKDIR /var/www/html

VOLUME /var/www/html

CMD ["cd", "/var/www/html/"]

#docker build . -t ubuntu-php7:16.04
#RUN chown -R www-data:www-data /var/www/html
#docker run -it -p 8080:80 -v /home/docker:/var/www/html/ sanjayabc1234/ubuntu-php7:16.04 bash
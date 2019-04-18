FROM ubuntu:14.04
MAINTAINER spjiang <spjiang@aliyun.com>

RUN sed -i "s/archive\.ubuntu\.com/mirrors.aliyun.com/g" /etc/apt/sources.list
RUN echo "deb http://nginx.org/packages/mainline/ubuntu/ trusty nginx" >> /etc/apt/sources.list
RUN echo "deb-src http://nginx.org/packages/mainline/ubuntu/ trusty nginx" >> /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ABF5BD827BD9BF62
RUN apt-get update && \
    apt-get install -y \
    nginx \
    php5 php5-fpm \
    php5-gd php5-mysql php5-memcached php5-memcached php5-redis php5-mcrypt \
    php5-curl && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN apt-get install -y php5-json
RUN apt-get update && apt-get install -y curl vim net-tools
RUN curl -sS https://getcomposer.org/installer | php
RUN /usr/bin/php composer.phar --version \
    mv composer.phar /usr/local/bin/composer
RUN apt-get install -y git

RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php5/fpm/php.ini
RUN echo "Asia/Shanghai" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata
RUN php5enmod mcrypt

ADD ./ /project
RUN ln -s /project/code /code

RUN chmod 777 /project/script/bootstrap.sh

WORKDIR /code

EXPOSE 2120
EXPOSE 2121

CMD /project/script/bootstrap.sh







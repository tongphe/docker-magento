FROM centos:7
MAINTAINER tongphe <tongphe.org@gmail.com>
LABEL Description="Linux + Apache 2.4 + PHP 5.6. CentOS 7 based for Magento 1 and 2" \
	Usage="docker build -t docker-php56; docker run -d -p [HOST PORT NUMBER]:80 -v [HOST WWW DOCUMENT ROOT]:/var/www/html docker-php56" \
	Version="1.0"


RUN yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN yum -y install https://centos7.iuscommunity.org/ius-release.rpm
RUN yum clean all && yum -y update
RUN yum -y install curl wget net-tools gcc make openssl-devel
RUN yum -y install httpd php56u php56u-common php56u-dba php56u-pear php56u-devel
RUN yum -y install php56u-common php56u-gd php56u-pdo php56u php56u-mysql php56u-xml php56u-mbstring php56u-pear php56u-mcrypt php56u-cli
RUN yum -y install php56u-opcache php56u-pecl-apcu php56u-intl php56u-memcached php56u-pecl-redis php56u-json

# Installing supervisor
RUN yum install -y python-setuptools
RUN easy_install pip
RUN pip install supervisor

ENV LOG_STDOUT **Boolean**
ENV LOG_STDERR **Boolean**
ENV LOG_LEVEL warn
ENV ALLOW_OVERRIDE All
ENV DATE_TIMEZONE UTC

COPY 10-vhosts.conf /etc/httpd/conf.d/
COPY php.ini /etc/php.ini
COPY supervisord.conf /etc/

VOLUME /var/www/html
VOLUME /var/log/httpd

EXPOSE 80

# Executing supervisord
CMD ["supervisord", "-n"]

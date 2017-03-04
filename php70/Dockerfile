FROM centos:7
MAINTAINER Fer Uria <fauria@gmail.com>
LABEL Description="Linux + Apache 2.4 + PHP 7.0.15. CentOS 7 based for Magento 1 and 2" \
	Usage="docker build -t docker-php70; docker run -d -p [HOST PORT NUMBER]:80 -v [HOST WWW DOCUMENT ROOT]:/var/www/html docker-php70" \
	Version="1.0"


RUN yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN yum -y install https://centos7.iuscommunity.org/ius-release.rpm
RUN yum clean all && yum -y update
RUN yum -y install curl wget net-tools gcc make openssl-devel
RUN yum -y install httpd php70u php70u-common php70u-dba php70u-pear php70u-devel
RUN yum -y install php70u-common php70u-gd php70u-pdo php70u php70u-mysql php70u-xml php70u-mbstring php70u-pear php70u-mcrypt php70u-cli
RUN yum -y install php70u-opcache php70u-pecl-apcu php70u-intl php70u-memcached php70u-pecl-redis php70u-json

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

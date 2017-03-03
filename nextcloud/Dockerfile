FROM centos:latest

RUN yum -y update && yum -y install httpd bzip2

RUN yum -y install https://centos7.iuscommunity.org/ius-release.rpm && yum -y install \
  mod_php71u \
  php71u-cli \
  php71u-gd \
  php71u-json \
  php71u-xml \
  php71u-mbstring \
  php71u-mcrypt \
  php71u-mysqlnd

ENV NEXTCLOUD_VERSION 11.0.2

RUN curl -fsSL -o nextcloud-${NEXTCLOUD_VERSION}.tar.bz2 https://download.nextcloud.com/server/releases/nextcloud-${NEXTCLOUD_VERSION}.tar.bz2 \
  && tar xfj nextcloud-${NEXTCLOUD_VERSION}.tar.bz2 --strip 1 -C /var/www/html/

COPY httpd.conf /etc/httpd/conf/httpd.conf
COPY security.conf /etc/httpd/conf.d/
COPY config.php /var/www/html/config/
RUN chown -R apache:apache /var/www/html/
RUN sed -i 's/expose_php = On/expose_php = Off/' /etc/php.ini

EXPOSE 80

ADD run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh

CMD ["/run-httpd.sh"]

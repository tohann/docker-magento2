FROM debian:jessie

ADD bin/* /usr/local/bin/

COPY ./etc/apt/sources.list /etc/apt/sources.list
RUN apt-get update && apt-get install -y apache2 apache2-doc apache2-utils
RUN a2enmod proxy_fcgi
RUN a2enmod rewrite
RUN a2enmod env

RUN ln -sf /proc/self/fd/1 /var/log/apache2/access.log && \
    ln -sf /proc/self/fd/1 /var/log/apache2/error.log

ENV FPM_HOST fpm
ENV FPM_PORT 9000
ENV VIRTUAL_HOST_FILE 25-magento2-httpd.conf
ENV MAGENTO_ROOT /var/www/magento
ENV MAGENTO_RUN_MODE developer
ENV DEBUG false

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

ENTRYPOINT ["/usr/local/bin/docker-environment"]
CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]

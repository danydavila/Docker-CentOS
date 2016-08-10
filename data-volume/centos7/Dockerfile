#===============================================================================
#               CentOS 7 Data volume                                           |
#===============================================================================

FROM centos:latest

MAINTAINER "Dany Davila" <danydavila@gmail.com>

RUN mkdir -p /usr/share/httpd && \
    mkdir -p /var/lib/nginx && \
    groupadd -g 48 apache && \
    groupadd -g 994 nginx && \
    groupadd -g 2001 www-users && \
    useradd --system -c "Apache" -d "/usr/share/httpd" --shell "/sbin/nologin" -g apache -u 48 apache && \
    useradd --system -c "Nginx"  -d "/var/lib/nginx"   --shell "/sbin/nologin" -g nginx  -u 996 nginx && \
    usermod -G apache,www-users nginx && \
    useradd -m -c "Web User" -d "/home/www-user" -s "/bin/bash" -g apache -u 2001 www-user && \
    usermod -G www-users,nginx www-user && \
    mkdir -p /var/www && chown -R www-user:www-users /var/www

USER www-user
VOLUME ["/var/www","/home/www-user","/var/log"]
CMD ["echo", "Data container for www-users"]
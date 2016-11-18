#===============================================================================
#               CentOS 7 Data volume                                           |
#===============================================================================

FROM centos:latest

MAINTAINER "Dany Davila" <danydavila@gmail.com>

RUN ln -snf /usr/share/zoneinfo/Etc/UTC /etc/localtime && echo "Etc/UTC" > /etc/timezone && \
    mkdir -p /usr/share/httpd && \
    mkdir -p /var/lib/nginx && \
    groupadd -g 48 apache && \
    groupadd -g 994 nginx && \
    groupadd -g 2001 www-users && \
    useradd --system -c "Apache" -d "/usr/share/httpd" --shell "/sbin/nologin" -g apache -u 48 apache && \
    useradd --system -c "Nginx"  -d "/var/lib/nginx"   --shell "/sbin/nologin" -g nginx  -u 996 nginx && \
    usermod -G apache,www-users nginx && \
    useradd -m -c "Web User" -d "/home/www-user" -s "/sbin/nologin" -g www-users -u 2001 www-user && \
    usermod -G www-users,nginx www-user && \
    mkdir -p /var/www && mkdir -p /var/log && \
    mkdir -p /var/log/{nginx,httpd,php,php-fpm,mysql,nodejs,ruby,java} && \
    touch /var/log/nginx/{access.log,error.log} && \
    touch /var/log/php/{php_error.log,error.log} && \
    touch /var/log/php-fpm/{php_error.log,error.log,slow.log} && \
    touch /var/log/mysql/{mysql-error.log,mysql-query.log,mysql-slow.log} && \
    touch /var/log/nodejs/{access.log,error.log,exceptions.log,info.log} && \
    chown -R www-user:www-users /var/www

USER www-user
VOLUME ["/var/www","/home/www-user","/var/log"]
CMD ["echo", "Data container for www-users"]
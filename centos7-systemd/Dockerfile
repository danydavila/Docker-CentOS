#==============================================================================#
# CentOS 7 Base file from the official build of CentOS with Systemd integration#
# systemd is now included in centos:latest base containers                     #
# Github: https://github.com/danydavila/Docker-CentOS                          #
#==============================================================================#

# Set the base image to Centos 7
FROM centos:7

# File Author / Maintainer
MAINTAINER "Dany Davila" <danydavila@gmail.com>

# Install  basic tools & dependencies
RUN yum -y update && yum -y install cronie wget curl git which gpg grep \
    sed perl python openssl tar xz xz-libs e2fsprogs

ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;

# Create the user for our web application and create the our app user.
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

RUN yum -y erase openssh-server >/dev/null 2>&1; \
    yum -y clean all && \
    rm -rf /tmp/* && \
    rm -f /var/log/wtmp /var/log/btmp && \
    (find /var/log -type f | while read f; do echo -ne '' > $f; done;)

# For systemd usage this changes to /usr/sbin/init
VOLUME ["/sys/fs/cgroup"]

# Run systemd by default via init.sh script, to start required services.
CMD ["/usr/sbin/init"]
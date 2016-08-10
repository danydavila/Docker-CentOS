FROM busybox:latest

MAINTAINER Dany Davila "<danydavila@gmail.com>"

# Create the www-user user
RUN mkdir -p /home && mkdir -p /home/www-user && \
    mkdir -p /usr/share && mkdir -p /usr/share/httpd && \
    mkdir -p /var/lib && mkdir -p /var/lib/nginx && \
    addgroup -S -g 48 apache && \
    addgroup -S -g 994 nginx && \
    addgroup -S -g 2001 www-users && \
    adduser -S -h "/usr/share/httpd" -s "/sbin/nologin" -G apache -u 48 apache && \
    adduser -S -h "/var/lib/nginx" -s "/sbin/nologin" -G nginx -u 996 nginx && \
    adduser -S -h "/home/www-user" -s /bin/bash -G www-users -u 2001 www-user;

# Create the folders and volume mount points
RUN mkdir -p /var && \
   mkdir -p /var/www && \
   mkdir -p /var && mkdir -p /var/log && mkdir -p /var/log/nginx && \
   chown -R www-user:www-users /var/log/nginx && \
   chown -R www-user:www-users /var/www && \
   chown -R www-user:www-users /home/www-user;

VOLUME ["/var/www","/var/log/nginx","/home/www-user"]

USER www-user
VOLUME ["/var/www"]
CMD ["echo", "Data container for www-user user"]

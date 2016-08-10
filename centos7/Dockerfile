#==============================================================================#
#               CentOS 7 Base file from the official build of CentOS.          #                                #
# Github: https://github.com/danydavila/Docker-CentOS                          #
#==============================================================================#

# Set the base image to CentOS 7
FROM centos:latest

# File Author / Maintainer
MAINTAINER "Dany Davila" <danydavila@gmail.com>

# Install Install dependencies, development tools and basic tools
RUN yum -y update && yum -y install gcc make gcc-c++ curl curl-devel wget \
    zlib zlib-devel bzip2 bzip2-devel patch make openssl openssl-devel sed \
    patchutils automake gettext flex bison autoconf gdb swig subversion \
    libtool intltool libaio-devel diffstat libpq-dev zlib1g-dev libssl-dev \
    sqlite sqlite-devel readline readline-devel postgresql-devel ncurses-devel \
    indent doxygen byacc cscope gcc-gfortran perl kpartx pcre pcre-devel \
    gd-devel libpcre3-dev glibc glibc-common krb5-libs openssl-libs \
    libyaml-devel libffi-devel iconv-devel gdbm-devel postgresql-libs  \
    mysql-devel gpg grep perl git tar xz xz-libs p7zip gawk rsync tree  \
    httpd-tools libxslt-devel nano unrar zip unzip which jq vi

# Installing process management.
RUN yum -y update && yum install -y python-pip python-setuptools; \
    easy_install pip; \
    pip install supervisor;

# Create the user for Nginx, Apache and our application user.
RUN ln -snf /usr/share/zoneinfo/Etc/UTC /etc/localtime && echo "Etc/UTC" > /etc/timezone && \
    mkdir -p /usr/share/httpd && \
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

# Add our default users.
RUN yum -y erase openssh-server >/dev/null 2>&1; \
    yum -y clean all && \
    rm -rf /tmp/* && \
    rm -f /var/log/wtmp /var/log/btmp && \
    (find /var/log -type f | while read f; do echo -ne '' > $f; done;)

CMD ["/bin/bash"]
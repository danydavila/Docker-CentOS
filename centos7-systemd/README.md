#  CentOS systemd docker container

The container was created as a base container for systemd based services.

### Build this base image:

```
docker build --rm -t visioncoder/centos7-systemd .
```

### Build this base image:

```
docker pull visioncoder/centos7-systemd
```

## Sample httpd container

Here we show you how we can create a sample httpd container.

Frist create a Dockerfile and setup the required service or services. Systemd can launch multiple services.

```
mkdir -p Apache2
cd Apache2
nano Dockerfile
```
Copy and paste

```
FROM visioncoder/centos7-systemd
MAINTAINER "Your Name" <you@example.com>
RUN yum -y install httpd; yum clean all; systemctl enable httpd.service
EXPOSE 80
CMD ["/usr/sbin/init"]
```

Then build it.

```
docker build --rm --no-cache -t c7-systemd-httpd .
```

Launch it.

```
docker run -ti -d \
--stop-signal=RTMIN+3 \
--log-driver=journald \
--security-opt seccomp:unconfined \
--cap-add=SYS_ADMIN \
-v /tmp/$(mktemp -d):/run \
-v /sys/fs/cgroup:/sys/fs/cgroup:ro \
-p 80:80 \
--name apache2 \
c7-systemd-httpd
```
or


```
docker run --privileged --name httpd \
-v /sys/fs/cgroup:/sys/fs/cgroup:ro \
-p 80:80 -d  c7-systemd-httpd
```

Finally use it.
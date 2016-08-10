#  CentOS systemd docker container

The container was created as a base container for systemd based services.

### Build this base image:

```
docker build --rm -t visioncoder/centos7-systemd .
```

### Pull the image from Docker hub

```
docker pull visioncoder/centos7-systemd
```

## Running a systemd enabled app container

Here we show you how we can create a sample httpd container.

In order to use the systemd enabled base container created above, you will need to create your `Dockerfile` similar to the one below.

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


In order to run a container with systemd, you will need to mount the cgroups volumes from the host. Below is an example command that will run the systemd enabled httpd container created earlier.

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

# How to install systemd in docker conatiner


step 1: create docker file

FROM centos

ENV container docker

RUN yum -y update; yum clean all

RUN yum -y install systemd; yum clean all;

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done);

RUN rm -f /lib/systemd/system/multi-user.target.wants/*;

RUN rm -f /etc/systemd/system/*.wants/*;

RUN rm -f /lib/systemd/system/local-fs.target.wants/*;

RUN rm -f /lib/systemd/system/sockets.target.wants/*udev*;

RUN rm -f /lib/systemd/system/sockets.target.wants/*initctl*;

RUN rm -f /lib/systemd/system/basic.target.wants/*;

RUN rm -f /lib/systemd/system/anaconda.target.wants/*;

VOLUME [ "/sys/fs/cgroup" ]

CMD ["/usr/sbin/init"]

step 2: create docker image

#docker build -t akhilesh_systemd .

# step 3: create docker conatiner 

#docker create -–privileged  -v /sys/fs/cgroup:/sys/fs/cgroup:ro -p 80:80 --name testing  akhilesh_systemd

# attach docker conatiner

#docker exec -it testing bash 



![Screenshot (811)](https://user-images.githubusercontent.com/64592542/145702578-acb1f5d9-c198-4ee6-938b-d7bbe679db1b.png)


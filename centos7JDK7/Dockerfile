FROM centos:centos7
MAINTAINER Aitor Pazos <mail@aitorpazos.es>

WORKDIR /root/
COPY jdk-7u71-linux-x64.rpm /root/
RUN yum upgrade -y && \
    rpm -i /root/jdk-7u71-linux-x64.rpm


# dockerImages

## Oracle DB on CentOS 7

This image sets up Oracle DB 12c instance with a DB created named ORCL, running
on CentOS 7. This image has a user ORCL_USER (PASSWORD: admin2DB) granted 
ORCL_USERS role with the following grants: CREATE session, CREATE table, 
CREATE sequence, CREATE trigger, CREATE view, CREATE procedure and CREATE synonym.

Due to limitations of docker's /dev/shm mount implementation, it is limited to 64MB,
which might impact Oracle DB performance (https://github.com/docker/docker/issues/2606).
You need to recompile docker yourself in order to increase this value.

You'll see some messages building this image complaining about permission denied
at mount: "mount: permission denied". These errors occur when trying to remount
/dev/shm with a bigger size because build is not ran as privileged. It dosen't 
affect image building process but it's something it should be fixed, and I'm
leaving it there as a reminder ;-).

## Credits

This image has been built based on the one described on: 
https://github.com/wscherphof/oracle-12c

### Prerequisites

Before building the image, you should download these files from Oracle's web 
site (http://www.oracle.com/technetwork/database/enterprise-edition/downloads/index.html):
    - linuxamd64_12c_database_1of2.zip
    - linuxamd64_12c_database_2of2.zip

### Dependencies

aitorpazos/centos7_oracle:centosJdk7
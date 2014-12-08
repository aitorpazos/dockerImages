# dockerImages

## Oracle DB on CentOS 7

This image sets up Oracle DB 12c instance with a DB created named ORCL, running
on CentOS 7.

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
# dockerImages

## Oracle DB on CentOS 7

This image sets up Oracle DB 12c instance with a DB created named ORCL, running
on CentOS 7. This image has a user ORCL_USER (PASSWORD: admin2DB) granted 
ORCL_USERS role with the following grants: CREATE session, CREATE table, 
CREATE sequence, CREATE trigger, CREATE view, CREATE procedure and CREATE synonym.

Oracle DB takes longer than other software to shutdown. You shoud use `docker stop --time=x <container>` where x should give Oracle seconds enough to shutdown properly.

### Running

Docker version >=1.10 is required. This version introduced the hability of setting a SHM size >64MB, which is required by Oracle DB.

Example:
```
docker run -d -v oracleDBVol:/u01/app/oracle/oradata -p 1521:1521 --name oracleDB1 --shm-size=1GB aitorpazos/centos7_oracle:oracle12c
```
## Credits

This image has been built based on the one described on: 
https://github.com/wscherphof/oracle-12c

### Prerequisites

Before building the image, you should download these files from Oracle's web 
site (http://www.oracle.com/technetwork/database/enterprise-edition/downloads/index.html):

 - linuxamd64_12c_database_1of2.zip
 - linuxamd64_12c_database_2of2.zip

### Dependencies

aitorpazos/centos7_oracle:oracle12cBinBase

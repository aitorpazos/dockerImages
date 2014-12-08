FROM aitorpazos/centos7_oracle:centosJdk7
MAINTAINER Aitor Pazos <mail@aitorpazos.es> 

ADD linuxamd64_12c_database_1of2.zip /tmp/install/linuxamd64_12c_database_1of2.zip
ADD linuxamd64_12c_database_2of2.zip /tmp/install/linuxamd64_12c_database_2of2.zip

RUN yum groupinstall "Development Tools" -y && yum install -y binutils compat-libstdc++-33 compat-libstdc++-33.i686 gcc gcc-c++ glibc glibc.i686 glibc-devel glibc-devel.i686 ksh libgcc libgcc.i686 libstdc++ libstdc++.i686 libstdc++-devel libstdc++-devel.i686 libaio libaio.i686 libaio-devel libaio-devel.i686 libXext libXext.i686 libXtst libXtst.i686 libX11 libX11.i686 libXau libXau.i686 libxcb libxcb.i686 libXi libXi.i686 make sysstat unixODBC unixODBC-devel zlib-devel lsof smartmontools && cd /tmp/install && unzip linuxamd64_12c_database_1of2.zip && unzip linuxamd64_12c_database_2of2.zip && rm *.zip

RUN groupadd -g 54321 oinstall && groupadd -g 54322 dba && useradd -m -u 54321 -g oinstall -G dba oracle
RUN echo "oracle:oracle" | chpasswd

ENV ORACLE_BASE /u01/app/oracle

RUN mkdir -p $ORACLE_BASE && chown -R oracle:oinstall $ORACLE_BASE && chmod -R 775 $ORACLE_BASE && mkdir -p /u01/app/oraInventory && chown -R oracle:oinstall /u01/app/oraInventory && chmod -R 775 /u01/app/oraInventory
ADD oraInst.loc /etc/oraInst.loc
RUN chmod 664 /etc/oraInst.loc

ADD sysctl.conf /etc/sysctl.conf
RUN echo "oracle soft stack 10240" >> /etc/security/limits.conf

ENV CVUQDISK_GRP oinstall
RUN cd /tmp/install/database/rpm && rpm -iv cvuqdisk-1.0.9-1.rpm

ADD db_install.rsp /tmp/db_install.rsp
ADD install /tmp/install/install
RUN chmod 755 /tmp/db_install.rsp /tmp/install/install && /tmp/install/install

RUN rm -rf /tmp/install && mv /u01/app/oracle/product/12.1.0/db_1/rdbms/lib/env_rdbms.mk /u01/app/oracle/product/12.1.0/db_1/rdbms/lib/env_rdbms.mk.bak

ENV ORACLE_SID ORCL
ENV ORACLE_HOME $ORACLE_BASE/product/12.1.0/db_1
ENV PATH $ORACLE_HOME/bin:$PATH

ADD env_rdbms.mk /u01/app/oracle/product/12.1.0/db_1/rdbms/lib/env_rdbms.mk
ADD initORCL.ora $ORACLE_HOME/dbs/initORCL.ora
ADD createdb.sql $ORACLE_HOME/config/scripts/createdb.sql
ADD create /tmp/create
RUN chmod 755 /u01/app/oracle/product/12.1.0/db_1/rdbms/lib/env_rdbms.mk $ORACLE_HOME/config/scripts/createdb.sql $ORACLE_HOME/dbs/initORCL.ora /tmp/create && rm -rf $ORACLE_HOME/lib/stubs/* && rm -f /u01/app/oracle/product/12.1.0/db_1/rdbms/lib/config.o && su oracle -c relink all
RUN $ORACLE_HOME/root.sh && mkdir -p $ORACLE_BASE/oradata && chown -R oracle:oinstall $ORACLE_BASE/oradata && chmod -R 775 $ORACLE_BASE/oradata && mkdir -p $ORACLE_BASE/fast_recovery_area && chown -R oracle:oinstall $ORACLE_BASE/fast_recovery_area && chmod -R 775 $ORACLE_BASE/fast_recovery_area

RUN /tmp/create && rm /tmp/create

EXPOSE 1521

ADD start /home/oracle/start
ADD oraStartup.sql $ORACLE_HOME/config/scripts/oraStartup.sql
ADD oraShutdown.sql $ORACLE_HOME/config/scripts/oraShutdown.sql
RUN chmod 755 $ORACLE_HOME/config/scripts/oraStartup.sql $HOME_ORACLE/config/scripts/oraShutdown.sql /home/oracle/start

USER oracle
WORKDIR /home/oracle/
CMD /home/oracle/start 




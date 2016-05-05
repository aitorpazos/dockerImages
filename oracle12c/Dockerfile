FROM aitorpazos/centos7_oracle:oracle12cBinBase
MAINTAINER Aitor Pazos <mail@aitorpazos.es> 

COPY linuxamd64_12c_database_1of2.zip /tmp/install/linuxamd64_12c_database_1of2.zip
COPY linuxamd64_12c_database_2of2.zip /tmp/install/linuxamd64_12c_database_2of2.zip

RUN yum upgrade -y && \
    yum install -y \
		lsof \
		smartmontools \
		sysstat \
		unixODBC unixODBC-devel && \
	cd /tmp/install && unzip linuxamd64_12c_database_1of2.zip && unzip linuxamd64_12c_database_2of2.zip && \
	rm *.zip

ENV CVUQDISK_GRP oinstall
COPY sysctl.conf /etc/sysctl.conf
COPY db_install.rsp /tmp/db_install.rsp
COPY install /tmp/install/install

RUN $(echo "oracle soft stack 10240" >> /etc/security/limits.conf) && \
	cd /tmp/install/database/rpm && \
	rpm -iv cvuqdisk-1.0.9-1.rpm && \
	chmod 755 /tmp/db_install.rsp /tmp/install/install && \
	/tmp/install/install && \
	mv /u01/app/oracle/product/12.1.0/db_1/rdbms/lib/env_rdbms.mk /u01/app/oracle/product/12.1.0/db_1/rdbms/lib/env_rdbms.mk.bak

ENV ORACLE_SID ORCL
ENV ORACLE_HOME ${ORACLE_BASE}/product/12.1.0/db_1/
ENV PATH ${ORACLE_HOME}/bin:$PATH
ENV LD_LIBRARY_PATH ${ORACLE_HOME}/lib:${LD_LIBRARY_PATH}
ENV CLASSPATH ${ORACLE_HOME}/jlib:${ORACLE_HOME}/rdbms/jlib:${CLASSPATH}
COPY env_rdbms.mk ${ORACLE_HOME}/rdbms/lib/env_rdbms.mk
COPY initORCL.ora ${ORACLE_HOME}/dbs/initORCL.ora
COPY createdb.sql ${ORACLE_HOME}/config/scripts/createdb.sql
COPY create /tmp/create
COPY start /home/oracle/start
COPY oraStartup.sql ${ORACLE_HOME}/config/scripts/oraStartup.sql
COPY oraShutdown.sql ${ORACLE_HOME}/config/scripts/oraShutdown.sql

RUN rm -rf /tmp/install && \
	chmod 755 \
		${ORACLE_HOME}/rdbms/lib/env_rdbms.mk \
		${ORACLE_HOME}/config/scripts/createdb.sql \
		${ORACLE_HOME}/dbs/initORCL.ora \
		/tmp/create && \
	rm -rf ${ORACLE_HOME}/lib/stubs/* && \
	rm -f ${ORACLE_HOME}/rdbms/lib/config.o && \
	su oracle -c relink all && \
	${ORACLE_HOME}/root.sh && \
	mkdir -p ${ORACLE_BASE}/oradata/data && \
	mkdir -p ${ORACLE_BASE}/oradata/flash_recovery_area && \
	mkdir -p ${ORACLE_BASE}/oradata/control2 && \
	mkdir -p ${ORACLE_BASE}/oradata/control1 && \
	mkdir -p ${ORACLE_BASE}/oradata/adump && \
	mkdir -p ${ORACLE_BASE}/oradata/diag && \
	chown -R oracle:oinstall ${ORACLE_BASE}/oradata && \
	chmod -R 775 ${ORACLE_BASE}/oradata && \
	chmod 755 \
		${ORACLE_HOME}/config/scripts/oraStartup.sql \
		${ORACLE_HOME}/config/scripts/oraShutdown.sql \
		/home/oracle/start && \
	/tmp/create && \
	rm /tmp/create 

EXPOSE 1521

USER oracle
WORKDIR /home/oracle/
CMD /home/oracle/start 
VOLUME /u01/app/oracle/oradata


FROM aitorpazos/centos7_oracle:oracle12cBinBase
MAINTAINER Aitor Pazos <mail@aitorpazos.es>

WORKDIR /home/oracle
ENV ORACLE_HOME $ORACLE_BASE/product/12.1.0/client_1
ENV PATH $ORACLE_HOME/bin:$PATH

COPY linuxamd64_12102_client.zip /home/oracle/linuxamd64_12102_client.zip
COPY client_install.rsp /home/oracle/client_install.rsp
COPY install /home/oracle/install
RUN chown oracle:oracle \
		/home/oracle/linuxamd64_12102_client.zip \
		/home/oracle/client_install.rsp \
		/home/oracle/install

USER oracle
RUN unzip /home/oracle/linuxamd64_12102_client.zip -d /home/oracle/ && \
	chmod a+x /home/oracle/client/runInstaller /home/oracle/install && \
	/home/oracle/install && \
	rm -rf /home/oracle/*.zip /home/oracle/client


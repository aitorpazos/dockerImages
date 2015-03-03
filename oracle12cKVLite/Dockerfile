FROM aitorpazos/centos7_oracle:centosJDK7
MAINTAINER Aitor Pazos <mail@aitorpazos.es>

RUN useradd -m -u 54321 oracle && \
	$(echo "oracle:oracle" | chpasswd ) && \
    chown -R oracle:oracle /home/oracle/

ADD kv-ce-3.2.5.tar.gz /home/oracle/

EXPOSE 5000 5001

USER oracle
WORKDIR /home/oracle/kv-3.2.5/
CMD java -jar lib/kvstore.jar kvlite -root $HOME/kvroot -store kvstore

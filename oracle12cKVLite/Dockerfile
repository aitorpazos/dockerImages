FROM aitorpazos/centos7_oracle:centosJdk7
MAINTAINER Aitor Pazos <mail@aitorpazos.es>

RUN useradd -m -u 54321 oracle && echo "oracle:oracle" | chpasswd

WORKDIR /home/oracle
ADD kv-ce-3.2.5.tar.gz /home/oracle/
RUN chown -R oracle:oracle /home/oracle/

EXPOSE 5000 5001

USER oracle
WORKDIR /home/oracle/kv-3.2.5/
CMD java -jar lib/kvstore.jar kvlite
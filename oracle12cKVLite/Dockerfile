FROM aitorpazos/centos7_oracle:centosJdk7
MAINTAINER Aitor Pazos <mail@aitorpazos.es> 

RUN useradd -m -u 54321 oracle && echo "oracle:oracle" | chpasswd

WORKDIR /home/oracle
USER oracle
RUN mkdir -p /home/oracle/install
ADD kv-ce-3.1.7.tar.gz /home/oracle/install/kv-ce-3.1.7.tar.gz
RUN tar -xf /home/oracle/install/kv-ce-3.1.7.tar.gz

EXPOSE 5000 5001

WORKDIR /home/oracle/kv-3.1.7/
CMD java -jar lib/kvstore.jar kvlite
FROM aitorpazos/centos7_oracle:centosJDK7
MAINTAINER Aitor Pazos <mail@aitorpazos.es> 

COPY oraInst.loc /etc/oraInst.loc
ENV ORACLE_BASE /u01/app/oracle

RUN yum upgrade -y && \
    yum groupinstall -y "Development Tools"  && \
    yum install -y \
		binutils \
		compat-libstdc++-33 compat-libstdc++-33.i686 \
		gcc gcc-c++ \
		glibc glibc.i686 glibc-devel glibc-devel.i686 \
		ksh \
		libgcc libgcc.i686 libstdc++ libstdc++.i686 libstdc++-devel libstdc++-devel.i686 \
		libaio libaio.i686 \
		libaio-devel libaio-devel.i686 \
		libXext libXext.i686 \
		libXtst libXtst.i686 \
		libX11 libX11.i686 \
		libXau libXau.i686 \
		libxcb libxcb.i686 \
		libXi libXi.i686 \
		make \
		zlib-devel && \
    groupadd -g 54320 oracle && \
    groupadd -g 54321 oinstall && \
    groupadd -g 54322 dba && \
    useradd -m -u 54321 -g oinstall -G dba,oracle oracle && \
    $(echo "oracle:oracle" | chpasswd) && \
    mkdir -p $ORACLE_BASE && \
    chown -R oracle:oinstall $ORACLE_BASE && \
    chmod -R 775 $ORACLE_BASE && \
    mkdir -p /u01/app/oraInventory && \
    chown -R oracle:oinstall /u01/app/oraInventory && \
    chmod -R 775 /u01/app/oraInventory && \
    chmod 664 /etc/oraInst.loc
    


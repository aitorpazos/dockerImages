# dockerImages

## Oracle NoSQL on CentOS 7

This image sets up Oracle NoSQL DB Community Edition instance configured to 
launch KVLite at start up.

Oracle NoSQL uses multiple ports while communicating with it's clients. Once a client connects to a storage node, it informs the client which replication nodes it should connect to, giving the client replication node's hostname (RMI is used here). If the client receive a hostname it doesn't understand, it will fail connecting to these replication nodes. Docker assign different IPs to containers on each start, so the most straightforward solution I've found is to assign `localhost` hostname to Oracle NoSQL containers and map container's exported ports to the same ports in the host machine. This should be fixed as it prevents you from running more than one NoSQL instance in the same host.

Example:

```
docker run -p 5000-5030:5000-5030 -h localhost aitorpazos/centos7_oracle:oracle12cKVLite
```

### Prerequisites

Before building the image, you should download kv-ce-3.1.7.tar.gz from Oracle's 
web site: http://www.oracle.com/technetwork/database/database-technologies/nosqldb/downloads/index.html

### Dependencies

aitorpazos/centos7_oracle:centosJdk7

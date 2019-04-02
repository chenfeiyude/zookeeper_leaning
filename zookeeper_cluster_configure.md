1. unzip zookeeper-3.4.14.tar.gz and copy as  zk_server1, zk_server2, zk_server3  

Folders
```
drwxr-xr-x 17 feiyu feiyu     6144 Apr  2 15:29 zk_server1   
drwxr-xr-x 17 feiyu feiyu     6144 Apr  2 15:32 zk_server2   
drwxr-xr-x 17 feiyu feiyu     6144 Apr  2 15:33 zk_server3   
drwxr-xr-x 16 feiyu feiyu     6144 Apr  2 10:19 zookeeper-3.4.14   
-rw-rw-r--  1 feiyu feiyu 37676320 Apr  1 15:44 zookeeper-3.4.14.tar.gz   
```
create data and dataLog folders
```
mkdir zk_server1/data
mkdir zk_server1/dataLog

mkdir zk_server2/data
mkdir zk_server2/dataLog

mkdir zk_server3/data
mkdir zk_server3/dataLog
```

2. Set myid for each server. myid has to be diff for each server 

```
echo 1 > zk_server1/data/myid   
echo 2 > zk_server2/data/myid   
echo 3 > zk_server3/data/myid
```

3. Edit conf files
As these are in the same server, so clientPort has to be diff. If they are on diff servers, then clientPort will be same, but server.{myid}=127.0.0.1 will be the actual IP

zk_server1/conf/zoo.cfg

```
tickTime = 2000
dataDir = /home/feiyu/zk_server1/data
dataLogDir = /home/feiyu/zk_server1/dataLog
clientPort = 2181
initLimit = 5
syncLimit = 2
server.1=127.0.0.1:2888:3888
server.2=127.0.0.1:2889:3889
server.3=127.0.0.1:2890:3890
```

zk_server2/conf/zoo.cfg

```
tickTime = 2000
dataDir = /home/feiyu/zk_server2/data
dataLogDir = /home/feiyu/zk_server2/dataLog
clientPort = 2182
initLimit = 5
syncLimit = 2
server.1=127.0.0.1:2888:3888
server.2=127.0.0.1:2889:3889
server.3=127.0.0.1:2890:3890
```

zk_server3/conf/zoo.cfg

```
tickTime = 2000
dataDir = /home/feiyu/zk_server3/data
dataLogDir = /home/feiyu/zk_server3/dataLog
clientPort = 2183
initLimit = 5
syncLimit = 2
server.1=127.0.0.1:2888:3888
server.2=127.0.0.1:2889:3889
server.3=127.0.0.1:2890:3890
```

4. Start servers   

```
zk_server1/bin/zkServer.sh start   
zk_server2/bin/zkServer.sh start   
zk_server3/bin/zkServer.sh start   
```

5. Connect to server   

e.g. connect to server2   

```
zk_server1/bin/zkCli.sh -server 127.0.0.1:2182   
```

6. Java connect to zookeeper server

127.0.0.1 should be replaced with the actual server IP

```java
private void createZKInstance() throws IOException {
    zk = new ZooKeeper("127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183", Test.SESSION_TIMEOUT, this.wh);
}
```

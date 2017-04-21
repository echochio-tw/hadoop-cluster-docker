# hadoop-cluster-docker

BASE use alpine & jse 1.8.0_112-b15 & hadoop-2.7.2

Source of echochio/hadoop

```
docker run -itd  -p 50070:50070 -p 8088:8088 --name hadoop-master --hostname hadoop-master echochio/hadoop
docker run -itd --name hadoop-slave1 --hostname hadoop-slave1 echochio/hadoop
docker run -itd --name hadoop-slave2 --hostname hadoop-slave2 echochio/hadoop
```

login hadoop-master
```
docker exec -it hadoop-master bash
```

Edit /etc/hosts
```
vi /etc/hosts
```

info for /etc/hosts
```
172.17.0.2      hadoop-master
172.17.0.3      hadoop-slave1
172.17.0.4      hadoop-slave2
```

copy /etc/hosts to hadoop-slave1 & hadoop-slave2
```
scp /etc/hosts hadoop-slave1:/etc/hosts
scp /etc/hosts hadoop-slave2:/etc/hosts
```

start hadoop
```
 ./start-hadoop.sh
``` 
 
 
 run wordcount
 ```
 ./run-wordcount.sh
 ```
 
 
 
 
 

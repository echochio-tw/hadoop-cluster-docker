# hadoop-cluster-docker

docker run -itd  -p 50070:50070 -p 8088:8088 --name hadoop-master --hostname hadoop-master echochio/hadoop

docker run -itd --name hadoop-slave1 --hostname hadoop-slave1 echochio/hadoop

docker run -itd --name hadoop-slave2 --hostname hadoop-slave2 echochio/hadoop


docker exec -it hadoop-master bash

/etc/hosts

172.17.0.2      hadoop-master
172.17.0.3      hadoop-slave1
172.17.0.4      hadoop-slave2


scp /etc/hosts hadoop-slave1:/etc/hosts
scp /etc/hosts hadoop-slave2:/etc/hosts


 ./start-hadoop.sh
 
 ./run-wordcount.sh

# hadoop-cluster-docker

BASE by Alpine linux & Java 1.8.0_112-b15 & Hadoop-2.7.2

Source of echochio/hadoop

![alt tag](https://github.com/echochio-tw/hadoop-cluster-docker/raw/master/pic/p1.png)

![alt tag](https://github.com/echochio-tw/hadoop-cluster-docker/raw/master/pic/p2.png)

Let try it .....

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
 
 Starting namenodes on [hadoop-master]
hadoop-master: Warning: Permanently added 'hadoop-master,172.17.0.2' (ECDSA) to the list of known hosts.
hadoop-master: starting namenode, logging to /usr/local/hadoop/logs/hadoop-root-namenode-hadoop-master.out
hadoop-master: ps: unrecognized option: p
hadoop-master: BusyBox v1.25.1 (2016-10-26 16:15:20 GMT) multi-call binary.
hadoop-master:
hadoop-master: Usage: ps [-o COL1,COL2=HEADER]
hadoop-master:
hadoop-master: Show list of processes
hadoop-master:
hadoop-master:  -o COL1,COL2=HEADER     Select columns for display
hadoop-slave1: Warning: Permanently added 'hadoop-slave1,172.17.0.3' (ECDSA) to the list of known hosts.
hadoop-slave2: Warning: Permanently added 'hadoop-slave2,172.17.0.4' (ECDSA) to the list of known hosts.
hadoop-slave1: starting datanode, logging to /usr/local/hadoop/logs/hadoop-root-datanode-hadoop-slave1.out
hadoop-slave1: ps: unrecognized option: p
hadoop-slave1: BusyBox v1.25.1 (2016-10-26 16:15:20 GMT) multi-call binary.
hadoop-slave1:
hadoop-slave1: Usage: ps [-o COL1,COL2=HEADER]
hadoop-slave1:
hadoop-slave1: Show list of processes
hadoop-slave1:
hadoop-slave1:  -o COL1,COL2=HEADER     Select columns for display
hadoop-slave2: starting datanode, logging to /usr/local/hadoop/logs/hadoop-root-datanode-hadoop-slave2.out
hadoop-slave2: ps: unrecognized option: p
hadoop-slave2: BusyBox v1.25.1 (2016-10-26 16:15:20 GMT) multi-call binary.
hadoop-slave2:
hadoop-slave2: Usage: ps [-o COL1,COL2=HEADER]
hadoop-slave2:
hadoop-slave2: Show list of processes
hadoop-slave2:
hadoop-slave2:  -o COL1,COL2=HEADER     Select columns for display
Starting secondary namenodes [0.0.0.0]
0.0.0.0: Warning: Permanently added '0.0.0.0' (ECDSA) to the list of known hosts.
0.0.0.0: starting secondarynamenode, logging to /usr/local/hadoop/logs/hadoop-root-secondarynamenode-hadoop-master.out
0.0.0.0: ps: unrecognized option: p
0.0.0.0: BusyBox v1.25.1 (2016-10-26 16:15:20 GMT) multi-call binary.
0.0.0.0:
0.0.0.0: Usage: ps [-o COL1,COL2=HEADER]
0.0.0.0:
0.0.0.0: Show list of processes
0.0.0.0:
0.0.0.0:        -o COL1,COL2=HEADER     Select columns for display
starting yarn daemons
starting resourcemanager, logging to /usr/local/hadoop/logs/yarn--resourcemanager-hadoop-master.out
hadoop-slave1: Warning: Permanently added 'hadoop-slave1,172.17.0.3' (ECDSA) to the list of known hosts.
hadoop-slave2: Warning: Permanently added 'hadoop-slave2,172.17.0.4' (ECDSA) to the list of known hosts.
hadoop-slave1: starting nodemanager, logging to /usr/local/hadoop/logs/yarn-root-nodemanager-hadoop-slave1.out
hadoop-slave2: starting nodemanager, logging to /usr/local/hadoop/logs/yarn-root-nodemanager-hadoop-slave2.out

``` 
 
 
 run wordcount
 ```
 ./run-wordcount.sh
 
 17/04/21 02:20:17 INFO client.RMProxy: Connecting to ResourceManager at hadoop-master/172.17.0.2:8032
17/04/21 02:20:18 INFO input.FileInputFormat: Total input paths to process : 2
17/04/21 02:20:18 INFO mapreduce.JobSubmitter: number of splits:2
17/04/21 02:20:18 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1492741170549_0001
17/04/21 02:20:18 INFO impl.YarnClientImpl: Submitted application application_1492741170549_0001
17/04/21 02:20:18 INFO mapreduce.Job: The url to track the job: http://hadoop-master:8088/proxy/application_1492741170549_0001/
17/04/21 02:20:18 INFO mapreduce.Job: Running job: job_1492741170549_0001
17/04/21 02:20:24 INFO mapreduce.Job: Job job_1492741170549_0001 running in uber mode : false
17/04/21 02:20:24 INFO mapreduce.Job:  map 0% reduce 0%
17/04/21 02:20:29 INFO mapreduce.Job:  map 100% reduce 0%
17/04/21 02:20:35 INFO mapreduce.Job:  map 100% reduce 100%
17/04/21 02:20:36 INFO mapreduce.Job: Job job_1492741170549_0001 completed successfully
17/04/21 02:20:37 INFO mapreduce.Job: Counters: 49
        File System Counters
                FILE: Number of bytes read=56
                FILE: Number of bytes written=352398
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=258
                HDFS: Number of bytes written=26
                HDFS: Number of read operations=9
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=2
        Job Counters
                Launched map tasks=2
                Launched reduce tasks=1
                Data-local map tasks=2
                Total time spent by all maps in occupied slots (ms)=5290
                Total time spent by all reduces in occupied slots (ms)=3542
                Total time spent by all map tasks (ms)=5290
                Total time spent by all reduce tasks (ms)=3542
                Total vcore-milliseconds taken by all map tasks=5290
                Total vcore-milliseconds taken by all reduce tasks=3542
                Total megabyte-milliseconds taken by all map tasks=5416960
                Total megabyte-milliseconds taken by all reduce tasks=3627008
        Map-Reduce Framework
                Map input records=2
                Map output records=4
                Map output bytes=42
                Map output materialized bytes=62
                Input split bytes=232
                Combine input records=4
                Combine output records=4
                Reduce input groups=3
                Reduce shuffle bytes=62
                Reduce input records=4
                Reduce output records=3
                Spilled Records=8
                Shuffled Maps =2
                Failed Shuffles=0
                Merged Map outputs=2
                GC time elapsed (ms)=143
                CPU time spent (ms)=1260
                Physical memory (bytes) snapshot=646254592
                Virtual memory (bytes) snapshot=5852717056
                Total committed heap usage (bytes)=509083648
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=26
        File Output Format Counters
                Bytes Written=26

input file1.txt:
Hello Hadoop

input file2.txt:
Hello Docker

wordcount output:
Docker  1
Hadoop  1
Hello   2

 ```
 
 
 
 
 

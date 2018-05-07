## exec-memory-logger.conf
- 目的：  
 输出到屏幕，测试验证输入源是否OK 

- 启动flume：  
flume-ng agent \
--name exec-memory-logger \
--conf $FLUME_HOME/conf \
--conf-file $FLUME_HOME/conf/exec-memory-logger.conf \
-Dflume.root.logger=INFO,console  
***

## exec-memory-kafka.conf
- 先启动zookeeper：  
zkServer.sh start
- 再启动Kafka:  
kafka-server-start.sh -daemon %KAFKA_HOME/config/server.properties

- 配置 exec-memory-kafka.conf：  
 exec-memory-logger.conf已验证输入源OK，在此基础上配置exec-memory-kafka.conf，测试验证sink到kafka是否OK 

- 启动flume：  
flume-ng agent \
--name exec-memory-kafka \
--conf $FLUME_HOME/conf \
--conf-file $FLUME_HOME/conf/exec-memory-kafka.conf \
-Dflume.root.logger=INFO,console  

- 启动Kafka消费脚本验证：  
kafka-console-consumer.sh --zookeeper 192.168.1.1:2181,192.168.1.2:2181,192.168.1.3:2181 --topic flume2spark
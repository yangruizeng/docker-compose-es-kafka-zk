# docker-compose-es-kafka-zk
docker-compose部署es kafka zk

# 使用  
chmod -R 777 kafka/data  
修改docker-compose.yml里的ip地址，docker-compose up -d启动即可  

# 注意的地方  
## kafka：
`server.properties:`  
broker.id=1 # 各个节点id不能重复
advertised.listeners=PLAINTEXT://10.16.128.23:9092 # 对外提供服务的ip端口
zookeeper.connect=10.16.128.23:2181,10.16.128.48:2181,10.16.128.39:2181 # zk集群地址  
`environment:`  
- KAFKA_ZOOKEEPER_CONNECT="10.16.128.23:2181,10.16.128.48:2181,10.16.128.39:2181" # zk集群地址  
- KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://10.16.128.23:9092 # 对外提供服务的ip端口

## es7：
`environment：`  
- "network.publish_host=10.16.128.23" # ES实例之间通信的ip
- "ES_JAVA_OPTS=-Xms12g -Xmx12g" # 设置ES内存，最大不超过机器内存的1/2，不超过32G。
- "discovery.zen.ping.unicast.hosts=10.16.xx.xx:9300,10.16.xx.xx:9300,10.16.xx.xx:9300" # es集群节点ip
- "cluster.initial_master_nodes=10.16.xx.xx,10.16.xxx.xx,10.16.1xx.xx" #  首次选举的种子节点


















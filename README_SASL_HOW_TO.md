# compile

```
sudo yum install -y java-1.8.0-openjdk-devel cyrus-sasl-devel cyrus-sasl-lib  libzstd-devel openssl openssl-devel openssl-libs openssl-static openssl-perl
./gradlew jar
```

# start zookeeper server 

```
pkill -f 'org.apache.zookeeper.server.quorum.QuorumPeerMain config/zookeeper.properties';
bin/zookeeper-server-start.sh -daemon config/zookeeper.properties
```

# start kafka server

```
export KAFKA_OPTS=-Djava.security.auth.login.config=config/kafka_server_jaas.conf; ./bin/kafka-server-start.sh config/server.properties --override delete.topic.enable=true > 1.txt 2>&1 |tee
```

# start consumer

```
bin/kafka-console-consumer.sh --topic recommend_sample --from-beginning --bootstrap-server localhost:9092  --consumer.config config/consumer.properties
```

# start producer

```
bin/kafka-console-producer.sh --topic recommend_sample --broker-list localhost:9092  --producer.config config/producer.properties
```

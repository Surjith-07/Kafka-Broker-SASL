# Kafka-Broker-SASL

### Zookeeper-Client
`
zookeeper-shell.sh localhost:2184 -zk-tls-config-file zoo-client.properties 
Connecting to localhost:2184
`

### Config USER [Provide ACL]
`
kafka-configs.sh --zookeeper localhost:2184 --zk-tls-config-file zoo-client.properties --entity-type users --entity-name surjith --alter --add-config 'SCRAM-SHA-512=[password=123]'
`

`
kafka-configs.sh --zookeeper localhost:2184 --zk-tls-config-file zoo-client.properties --entity-type users --entity-name producer --alter --add-config 'SCRAM-SHA-512=[password=456]'
`

`
kafka-configs.sh --zookeeper localhost:2184 --zk-tls-config-file zoo-client.properties --entity-type users --entity-name consumer --alter --add-config 'SCRAM-SHA-512=[password=789]'
`

### Describe list of topics
`
kafka-topics.sh --zookeeper localhost:2181 --list
`

### Permissions [ACLS]

`
kafka-acls.sh --authorizer-properties zookeeper.connect=localhost:2184 --zk-tls-config-file zoo-client.properties --add --allow-principal User:producer --operation WRITE --operation DESCRIBE --operation DESCRIBECONFIGS --topic ssl-topic
`

`
 kafka-acls.sh --authorizer-properties zookeeper.connect=localhost:2184 --zk-tls-config-file zoo-client.properties --add --allow-principal User:consumer --operation READ --operation DESCRIBE --topic ssl-topic
`

`
kafka-acls.sh --authorizer-properties zookeeper.connect=localhost:2184 --zk-tls-config-file zoo-client.properties --add --allow-principal User:consumer --operation READ --operation DESCRIBE --group ssl-consumer-group
`

`
kafka-acls.sh --authorizer-properties zookeeper.connect=localhost:2184 --zk-tls-config-file zookeeper-client.properties --list --topic ssl-topic
`


### https://github.com/vinclv/data-engineering-minds-kafka/tree/main/config/sasl_ssl

`
 kafka-console-producer.sh --broker-list localhost:9092,localhost:9093 --topic ssl-topic --producer.config producer.properties
`


`
kafka-console-consumer.sh --bootstrap-server localhost:9092,localhost:9093 --topic ssl-topic --from-beginning --consumer.config consumer.properties 
`


`
zookeeper-shell.sh localhost:2184 -zk-tls-config-file zookeeper-client.properties
`

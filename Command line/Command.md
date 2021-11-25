### xjc

xjc ==> Compiles an XML schema file into fully annotated Java classes.

```shell
xjc -d [target directory]  [source xsd path]
```



### confluent kafka

```shell
# docker
docker ps
#docker exec -it {CONTAINER ID} /bin/bash
docker exec -it 21b14986f276 /bin/bash

# kafka
# list topic
kafka-topics --list --bootstrap-server localhost:9092
# delete topic
kafka-topics --delete --topic cool-topic --bootstrap-server localhost:9092

# run producer to send messages
# kafka-console-producer --topic {topic_name} --bootstrap-server localhost:9092
kafka-console-producer --topic lvc-product-transfer-dev --bootstrap-server localhost:9092

# run consumer to read messages
# kafka-console-consumer --topic {topic_name} --from-beginning --bootstrap-server localhost:9092
kafka-console-consumer --topic lvc-product-transfer-dev --from-beginning --max-messages 2 --bootstrap-server localhost:9092

# print key
kafka-console-consumer --topic lvc-product-transfer-dev --from-beginning --max-messages 2 --bootstrap-server localhost:9092 --property print.key=true

# use config
kafka-console-consumer --bootstrap-server pkc-lgwgm.eastus2.azure.confluent.cloud:9092 --topic lvc-product-transfer-dev --consumer.config config/ptds-dev-credential.properties --from
-beginning --max-messages 2 --property print.key=true
```

> https://docs.confluent.io/platform/current/kafka/kafka-basics.html
>
> https://www.hnbian.cn/posts/8dea4499.html



### mongodb

```shell
# deleteall
db['name'].remove({})
db.getCollection("name").deleteMany({"field":"value"})

# find
db.getCollection("name").find({"field":"value"})
	# regex
	{"field":{$regex : ".*xxxx*"}}
	# orderby
	{$query:{}, $orderby:{"field":-1}} # -1:descend 1:ascend

```


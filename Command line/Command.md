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
kafka-topics --list --bootstrap-server localhost:29092

# create topic
kafka-topics --create --topic {topic_name} --bootstrap-server localhost:29092

# delete topic
kafka-topics --delete --topic mvtds-sap-nom-key-local --bootstrap-server localhost:9092

# run producer to send messages
# kafka-console-producer --topic {topic_name} --bootstrap-server localhost:29092
kafka-console-producer --topic delivery-line-event-dev --bootstrap-server localhost:29092 < message.json
kafka-console-producer --topic user --bootstrap-server localhost:29092 < message.json
kafka-console-producer --broker-list sulky-01.srvs.cloudkafka.com:9094,sulky-02.srvs.cloudkafka.com:9094,sulky-03.srvs.cloudkafka.com:9094 --topic t4x98u0p-qa --producer.config config/dl-dev-credential.properties < message.json

# run consumer to read messages
# kafka-console-consumer --topic {topic_name} --from-beginning --bootstrap-server localhost:29092
kafka-console-consumer --topic lvc-product-transfer-dev --from-beginning --max-messages 2 --bootstrap-server localhost:29092
kafka-console-consumer --topic delivery-line-event-dev --from-beginning --bootstrap-server localhost:29092

# print partition
kafka-console-consumer --topic user --from-beginning --bootstrap-server localhost:29092 --property print.partition=true

# print key
kafka-console-consumer --topic lvc-product-transfer-dev --from-beginning --max-messages 2 --bootstrap-server localhost:29092 --property print.key=true

# use config
kafka-console-consumer --bootstrap-server pkc-lgwgm.eastus2.azure.confluent.cloud:29092 --topic lvc-product-transfer-dev --consumer.config config/ptds-dev-credential.properties --from-beginning --max-messages 2 --property print.key=true

kafka-console-consumer --bootstrap-server sulky-01.srvs.cloudkafka.com:9094,sulky-02.srvs.cloudkafka.com:9094,sulky-03.srvs.cloudkafka.com:9094 --topic t4x98u0p-default --consumer.config config/dl-dev-credential.properties --from-beginning --max-messages 2 --property print.key=true

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



### kubectl 

```shell
kubectl get all -n movement-dev
# get pod
kubectl get pods -n movement-dev
# exec pod
kubectl exec -n movement-dev -it mvtds-api-service-5ccb9d68cc-lk9wd -- bash
# log
kubectl logs mvtds-api-service-5ccb9d68cc-5zpn4 -n movement-dev
# describe pod
kubectl describe pods mvtds-api-service-5ccb9d68cc-lk9wd -n movement-dev
# describe ingress
kubectl describe ingress ingress-movement-dev -n movement-dev

```



### Azure

```shell
az login
az account set --subscription efede11f-18f5-4297-ac13-1e4582c232ff
az aks get-credentials --resource-group rg-lcds-nonprod --name aks-lcds-nonprod --admin

—>/Users/fangyuan.fu/.kube/config

查看nodepool的数量
az aks nodepool list --resource-group rg-lcds-nonprod --cluster-name aks-lcds-nonprod

查看可更新的版本
az aks get-upgrades --resource-group rg-lcds-nonprod --name aks-lcds-nonprod --output table


az login
az account set --subscription efede11f-18f5-4297-ac13-1e4582c232ff
az aks get-credentials --resource-group rg-ptds-nonprod --name aks-ptds-nonprod --admin

az aks get-credentials --resource-group Rg-Enablement-App-USSC-NonProd --name shared-aks-nonprod
```

### Helm

```shell
helm rollback mvtds-transformer-service --namespace movement-dev

kubectl describe pod/mvtds-transformer-service-97685fdb7-jrxpz -n movement-dev

```

### GIT

```
git remote set-url origin https://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@github.com/ExxonMobil/mvtds-transformer-service.git
```


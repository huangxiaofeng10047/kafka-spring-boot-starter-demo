docker run -d --name zookeeper -p 2181:2181  wurstmeister/zookeeper
docker run -d --name kafka -p 9092:9092 -e KAFKA_BROKER_ID=0 -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 --link zookeeper -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://172.21.195.56:9092 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 -t wurstmeister/kafka
docker run -d --name zookeeper1 -p 2182:2182  wurstmeister/zookeeper
docker run -d --name kafka1 -p 9093:9092 -e KAFKA_BROKER_ID=0 -e KAFKA_ZOOKEEPER_CONNECT=zookeeper1:2181 --link zookeeper1 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://kafka1:9092 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 -t wurstmeister/kafka
docker run -d --name zookeeper2 -p 2183:2181  wurstmeister/zookeeper
docker run -d --name kafka2 -p 9094:9094 -e KAFKA_BROKER_ID=0 -e KAFKA_ZOOKEEPER_CONNECT=172.21.195.56:2183  -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://172.21.195.56:9094 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9094 -t wurstmeister/kafka


kcat -b kafkabroker:9093  -L -J | jq .


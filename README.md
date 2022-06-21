# spring-cloud-config
Spring Cloud Config Server

Spring Cloud Config Server

Docker에서 Kafka 구성

docker pull wurstmeister/kafka
docker pull wurstmeister/zookeeper

---
docker-compose.yml파일 생성
```
version: '2'
services:
  zookeeper:
    container_name: local-zookeeper
    image: wurstmeister/zookeeper
    ports:
      - "2181:2181"
  kafka:
    container_name: local-kafka
    image: wurstmeister/kafka
    ports:
      - "9092:9092"
    environment:
      KAFKA_ADVERTISED_HOST_NAME: 127.0.0.1
      KAFKA_ADVERTISED_PORT: 9092
      KAFKA_CREATE_TOPICS: "test_topic:1:1" #topic이름:partition개수:Replica개수
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```

해당 파일 경로에서 기동
docker-compose up -d

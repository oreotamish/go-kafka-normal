# go-kafka-normal

## Setup:

- **Start Docker Daemon**

- **Run Zookeeper:**

    ```bash
    docker run --name zookeeper -p 2181:2181 zookeeper
    ```

- **Run Kafka:**

    ```bash
    docker run --name kafka -p 9092:9092 \
    -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 \
    -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9092 \
    -e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 \
    --link zookeeper:zookeeper \
    confluentinc/cp-kafka
    ```

- **Copy Repository and Run:**

    1. Run the producer:

        ```bash
        go run cmd/producer/producer.go
        ```

    2. Run the consumer:

        ```bash
        go run cmd/consumer/consumer.go
        ```

## Usage:

- **Produce Messages:**

    Use `curl` to send messages:

    ```bash
    curl -X POST http://localhost:8080/send \
    -d "fromID=<id>&toID=<id>&message=<message>"
    ```

- **Consume Messages:**

    Use `curl` to retrieve notifications:

    ```bash
    curl http://localhost:8081/notifications/<id>
    ```

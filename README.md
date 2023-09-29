# kafka-example

This is a simple project to learn how to use Kafka with Spring Boot.

## Installation

First you need to install kafka by following the official guide :
https://kafka.apache.org/quickstart

You need to:

Download last version of Kafka (Current is kafka_2.13-3.5.0).

```bash
$ tar -xzf kafka_2.13-3.5.0.tgz
$ cd kafka_2.13-3.5.0
```

Duplicate your terminal, you need three terminals sessions for this tuto:

* one for ZooKeeper service (1)
* one for Kafka broker service (2)
* one to test everything is Ok (3)

With session (1) run :

```bash
# Start the ZooKeeper service
$ bin/zookeeper-server-start.sh config/zookeeper.properties
```

With session (2) run:

```bash
# Start the Kafka broker service
$ bin/kafka-server-start.sh config/server.properties
```

After ZooKeeper service and Kafka broker service are running, you need to launch the spring boot application.

With session (3) run:

```bash
$ bin/kafka-console-consumer.sh --topic first --from-beginning --bootstrap-server localhost:9092
```

You can test the application with Curl:

```bash
curl --header "Content-Type: application/json" --request POST --data '{"message": "Curl test"}' http://localhost:8080/api/v1/message
```

If everything is OK, you need to see in the third session (3):
```bash
message from API : [Curl test]
```

If you prefer postman (You have the KafkaAPITest.postman_collection.json in the folder), you can test that everything is working well, by trying the only API in the collection.

In this case, the message will be:
```bash
message from API : [Postman test]
```

## API Reference

#### Test Kafka API

```http
  POST /api/v1/message
```

JSON Body :
```json
{
    "message" : "Postman test"
}
```

## Terminate the kafka environment

Now that you reached the end of the quickstart, feel free to tear down the Kafka environment—or continue playing around.

Stop the consumer clients with Ctrl-C, if you haven't done so already. (Session (3))
Stop the Kafka broker with Ctrl-C. (Session (2))
Lastly stop the ZooKeeper server with Ctrl-C. (Session (1))

If you also want to delete any data of your local Kafka environment including any events you have created along the way, run the command:
```bash
$ rm -rf /tmp/kafka-logs /tmp/zookeeper /tmp/kraft-combined-logs
```

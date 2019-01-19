# 1.  Introduction
In this Wiki page, we will see what is a RAW message and how to produce this kind of records to a Kafka topic.

For more details about Kafka testing, please visit [Kafka Testing Introduction - Baby Steps](https://github.com/authorjapps/zerocode/wiki/Kafka-Testing-Introduction)

# 2.  What is RAW message
RAW messages can be any kind of messages which may not have or may have structures, as well as the records may or may not conform to a specific data schema.


# 3.  How to produce a RAW message to a Kafka topic
We just need to specify the "recordType" as RAW while producing the record to a Kafka topic.
>      "recordType" : "RAW"

And the operation here is
>      "operation" : "produce"

The test request will look like below
```
"request": {
    "recordType": "RAW",
    "records": [
        {
            "key": "KEY-101",
            "value": "Hello World"
        }
    ]
}
```
Please observe above, the "value" field which is a simple text message.
>   "value": "Hello World"

You can put anything into it and send to Kafka topic and Kafka broker will accept it.
> e.g. "value": "bla bla"  or "value": "10478ABCDG1234-HEXA-VALUE" etc

Then the consumer needs to decide how it should consume it, the best way to consume this kind of message is same as RAW. See the consumer example [Consume RAW message]() in the side bar.

# 4.  Which SerDe is used for this kind of record
What is SerDe? Ans: Serializer, Deserializer
The best way to produce and consume RAW messages is use,
+ StringSerializer
  + key.serializer=org.apache.kafka.common.serialization.StringSerializer
  + value.serializer=org.apache.kafka.common.serialization.StringSerializer
+ StringDeserializer
  + key.deserializer=org.apache.kafka.common.serialization.StringDeserializer
  + value.deserializer=org.apache.kafka.common.serialization.StringDeserializer


# 5.  How the SerDe is configured for a Kafka producer
+ See [kafka_test_server.properties](https://github.com/authorjapps/zerocode/blob/master/kafka-testing/src/test/resources/kafka_servers/kafka_test_server.properties) here how they are configured.
+ Look for these two configs in the same resource folder.
  + kafka.producer.properties=kafka_servers/kafka_producer.properties
  + kafka.consumer.properties=kafka_servers/kafka_consumer.properties

You can update/add/remove the desired key-value depending on your test-requirement.

# 6.  How does the full "produce" operation step looks like
Now we have all the details to invoke the "produce" operation. The step looks like,
```java

test_kafka_produce_raw.json
---------------------------

{
    "name": "produce_raw_msg",
    "url": "kafka-topic:demo-raw-topic-1",
    "operation": "produce",
    "request": {
        "recordType": "RAW",
        "records": [
            {
                "key": "KEY-101",
                "value": "Hello World"
            }
        ]
    },
    "assertions": {
        "status": "Ok",
        "recordMetadata": "$NOT.NULL"
    }
}
```

# 7.  How to run the test
The test looks like below and we can run the test as usual JUnit test,
```java
@TargetEnv("kafka_servers/kafka_test_server.properties")
@RunWith(ZeroCodeUnitRunner.class)
public class KafkaProduceTest {

    @Test
    @JsonTestCase("kafka/produce/test_kafka_produce_raw.json")
    public void testProduce_raw() throws Exception {
    }

}
```

The "kafka_test_server.properties" file contains,
```properties
kafka.bootstrap.servers=localhost:9092
kafka.producer.properties=kafka_servers/kafka_producer.properties
kafka.consumer.properties=kafka_servers/kafka_consumer.properties
```

And the "kafka_producer.properties" contains,
```properties
# =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
#          kafka producer properties
# =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
client.id=zerocode-producer
key.serializer=org.apache.kafka.common.serialization.StringSerializer
value.serializer=org.apache.kafka.common.serialization.StringSerializer

```

## :::Note:::
You can use many variation of "Serializer" depending upon your "key" and "value" data types of your tests.
e.g. 
A "DoubleSerializer" if the Key is a Double or Integer or Long value.
> key.serializer=org.apache.kafka.common.serialization.DoubleSerializer



# 1.  Introduction

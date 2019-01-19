# 1.  Introduction
In this Wiki page we will see various concepts of Kafka distributed streams and how to test an Application built using Kafka and REST apis. 

For more details about Kafka streams and how to develop a streaming application, please visit [Developing Streaming Applications](https://www.confluent.io/blog/stream-processing-part-1-tutorial-developing-streaming-applications).

# 2.  Kafka Testing Concepts
Kafka is a distributed messaging system.When we deal with a Kafka application, we need to know where the `topic` resides and what types of messages aka `records` are written aka `produced` to the topic, then what happens when the messages are `consumed` by the listeners.

Once we know these three things, we should be able to test a Kafka application easily.

# 2.1.  What is a Kafka topic
Kafka topics are divided into a number of partitions. Partitions allow you to parallelize a topic by splitting the data in a particular topic across multiple brokers — each partition can be placed on a separate machine to allow for multiple consumers to read from a topic in parallel.

# 2.2.  What is produce and consume
`Produce` is simply writing one or more records to a topic.

`Consume` is simply reading one or more records from a topic.

# 2.3.  Writing tests only to produce
When you write or produce to a topic you can verify the acknowledgement from Kafka broker which is in the format of `recordMetadata`.

e.g.
```java

Response from broker after a successful "produce".

{
    "recordMetadata": {
        "offset": 0,
        "timestamp": 1547760760264,
        "serializedKeySize": 13,
        "serializedValueSize": 34,
        "topicPartition": {
            "hash": 749715182,
            "partition": 0,
            "topic": "demo-topic"
        }
    }
}
```

# 2.4.  Writing tests only to consume
When you read or consume from a topic you can verify the record(s) from the topics.
Here you can validate/assert some of the meta data too, but most of the times you only need to deal with the records.

e.g.
```java

Response from broker after a successful "consume".
{
    "records": [
        {
            "topic": "demo-topic",
            "key": "1547792460796",
            "value": "Hello World"
        }
    ]
}
```
The full record with meta data information looks like below, which too you can validate/assert in case you have a test requirement to do so.
```java
{
    "records": [
        {
            "topic": "demo-topic",
            "partition": 0,
            "offset": 3,
            "timestamp": 1547792461364,
            "timestampType": "CREATE_TIME",
            "serializedKeySize": 13,
            "serializedValueSize": 11,
            "headers": {
                "headers": [],
                "isReadOnly": false
            },
            "key": "1547792460796",
            "value": "Hello World",
            "leaderEpoch": {
                "value": 0
            }
        }
    ]
}
```
# 2.5.  Writing tests for both produce and consume

# 3.  Writing your first produce and consume test

# 8.  Validating Kafka response after producing

# 9.  Validating Kafka response after consuming

# 10.  Combining Kafka testing with REST api testing

# 11.  Producing RAW messages vs JSON messages

# 12.  Why do I need Zerocode testing lib
Zerocode is a light-weight, simple and extensible open-source framework for writing test intentions in simple JSON format that facilitates both declarative configuration and automation. The framework manages the request payload handling and response assertions at the same time.

It has got best of best ideas and practices from the community and the adoption is rapids growing in the developer/tester community. Even many times manual test engineers come out and help in automation due to the simplicity of writing tests.

# 13.  Conclusion
In this tutorial, we looked at some of the Kafka concepts and how to test Kafka applications using the Zerocode Testing Framework.

The complete source code and all example code snippets for this Wiki page can be found over on [GitHub]().

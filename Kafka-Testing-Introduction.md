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
Here you can validate/assert some of the meta data too, but most of the times you only need to deal with the records only(not the metadata).

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
In the same test, you can hook two steps like below <br/>
+ Step-1) Produce to a topic e.g. `demo-topic` and validate `recordMetadata`
  + e.g. Produce a record with "key":"1234", "value":"Hello World"

+ Step-2) Consume from the same topic i.e. `demo-topic` and validate `records`
  + Assert that the same record was in the consumed records "key":"1234", "value":"Hello World", because we might have consumed more that one record if they were produced to the same topic. 


# 3.1.  Writing your first produce test
To write the tests for any of 'Produce' or 'Consume' tests, we need to know the following details
+ The topic name which is our "end point" aka "url"
```

"url": "kafka-topic: demo-topic"

```

+ The operation i.e. `'produce' or 'consume'` 
```

"operation": "produce"

```
_Also you can use the `'load' or 'unload'` aka `'send' or 'receive'` which means the same._

+ While sending a message to the topic, we need to send as below
```java

"request": {
    "records": [
        {
            "key": "KEY-1234",
            "value": "Hello World"
        }
    ]
}

```

Please visit these pages for examples and explanations.
+ [Produce a RAW message]()
+ [Produce a JSON message]()

# 3.2.  Writing our first consume test
+ The topic name which is our "end point" aka "url"
```

"url": "kafka-topic: demo-topic"

```

+ The operation i.e. 'consume'` 
```

"operation": "consume"

```
_Also you can use the `'unload'` aka `'receive'` which exactly means the same._

+ While consuming message(s) from the topic, we need to send as below
```java

"request": { },

```
That's do nothing, but simply consume.

Or we we can configure our test to do certain stuff while consuming or after consuming the records.
```
"request": {
    "consumerLocalConfigs": {
        "commitSync": true,
        "showRecordsConsumed": true,
        "maxNoOfRetryPollsOrTimeouts": 3
    }
}

```

>         "commitSync": true,

Here, we are telling the test to do a `commitSync` after consuming the message, that means, it won't read the message again when you `poll` next time. It will only read the new messages if any arrives on the topic.

>        "showRecordsConsumed": true,  // Default is true
Here, we are telling the test to show the consumed records in the response. If you set `"showRecordsConsumed": false`, then it will only show the size, not the actual records.

>        "maxNoOfRetryPollsOrTimeouts": 3
Here, we are telling the test to show poll 3 times maximum, then stop polling. If we have more records, we can set to a larger value. Default value is `100` mili sec.

>        "pollingTime": 500   // Default is 100 mili sec
Here, we are telling the test to poll for 500 mili sec each time it polls.

- Visit this page [All configurable keys - ConsumerLocalConfigs]() for the source code.
- Visit the [HelloWorld example]() to try it at home.

### :::Note:::
These config values can be set in the properties file, which means it will apply to all the tests in our test suite or test pack. Also any of the configs can be overridden by any particular test inside the suite. **Hence it gives us very flexibility for covering all test scenarios.**

Please visit these pages for examples and explanations.
+ [Consume a RAW message]()
+ [Consume a JSON message]()


# 8.  Validating Kafka response after producing
We can simply tell the test to check that it has been produced successfully as below
```json
"assertions": {
    "status": "Ok"
}
```

Or we can ask the test to assert that we have received `not null` "recordMetadata" from the Kafka brokers
```json
"assertions": {
    "status": "Ok",
    "recordMetadata": "$NOT.NULL"
}
```

Or we can ago further amd ask the test to assert the "recordMetadata" to verify it has written to correct `partition` of the correct `topic` and much more as below. 
```json
"assertions": {
    "status": "Ok",
    "recordMetadata": {
        "offset": 0,
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
Yes, just stick the JSON block as it is. Isn't it awesome and clean? Hasn't it take away lot of hassles from us of doing a vicious deserialization of the `acknowledgement` or asserting field-by-field after that, making the test almost not-readable?

Or if you are not really bothered about some fields, you can simply put as `$NOT.NULL` against them as below or completely skip them.
:::NOTE:::
Field orders doesn't really matter as long as the structure is maintained. 👍 

```json
{
    "status": "Ok",
    "recordMetadata": {
        "topicPartition": {
            "partition": 0,
            "topic": "demo-2"
        },
        "offset": "$NOT.NULL",
        "timestamp": "$NOT.NULL",
        "serializedKeySize": "$NOT.NULL",
        "serializedValueSize": "$NOT.NULL"
    }
}
```

# 9.  Validating Kafka response after consuming
We can simply tell the test to check that we have received number of records we intended to consume.
```java
"assertions": {
    "size" : 1
}
```

Or we can ask the test to assert number of records as well as the records i.e. field-by-filed of key/values. 
```java
"assertions": {
    "size": 1
    "records": [
        {
            "key": "1547792460796",
            "value": "Hello World"
        }
    ]
}
```

Or we can ask the test to assert the records along with some metadata e.g. topic and partition info too. 

```java
"assertions": {
    "records": [
        {
            "key": "1547792460796",
            "value": "Hello World",
            "topic": "demo-ksql",
            "partition": 0,
            "offset": 3,
            "timestamp": 1547792461364
        }
    ],
    "size": 1
}
```
:::NOTE:::
Field orders doesn't really matter as long as the structure is maintained. 👍 

# 10.  Combining Kafka testing with REST api testing
Most of the time we have situations to deal with Kafka and REST api testing. With `Zerocode` it's just zero effort when comes to this kind of situation or any API testing situation. You need to know four things only to write the tests 
```
1) The "url"
2) The "operation"
3) The "request"
4) The "assertions" i.e. the expected response
```

Let's see how we can fit REST api validation along with Kafka produce/consume validation at same time.
//WIP TODO

# 11.  Producing RAW messages vs JSON messages

# 12.  Why do I need Zerocode testing lib
Zerocode is a light-weight, simple and extensible open-source framework for writing test intentions in simple JSON format that facilitates both declarative configuration and automation. The framework manages the request payload handling and response assertions at the same time.

It has got best of best ideas and practices from the community and the adoption is rapids growing in the developer/tester community. Even many times manual test engineers come out and help in automation due to the simplicity of writing tests.

# 13.  Conclusion
In this tutorial, we looked at some of the Kafka concepts and how to test Kafka applications using the Zerocode Testing Framework.

The complete source code and all example code snippets for this Wiki page can be found over on [GitHub]().

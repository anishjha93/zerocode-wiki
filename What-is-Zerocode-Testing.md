Advantages of _Declarative_ Testing
===
Instead of writing code to achieve the testing goals, we write the test intentions in a defined structure.<br/>
Here the framework, behind the scene, generates the necessary code to do the job for us. 

+ In this style we attempt to minimize or eliminate side effects by describing what the `test` must accomplish in terms of the business functionality, rather than describe how to accomplish it via programming or coding.

> That makes things a lot easy and clean.

<br/>

In the _Declarative Style_ **we don't need to write** any of the below.
+ The Http Client (or Kafka Client) calls for REST APIs
+ Request payload parsing
+ Response payload parsing
+ Code for assertions e.g. comparing actual vs expected response



| Declarative Style                            | Traditional Style                                        |
| -------------------------------------------- | -------------------------------------------------------- |
| `"url":"/api/v1/register/persons"`    | Create an _HttpClient_ object. Set the `url` to `"/api/v1/register/persons"` <br/> e.g. `RequestBuilder.setUri(httpUrl);`  |
| `"operation": "POST"`  | Set this `POST` operaton to the _HttpClient_ object <br/> e.g. `RequestBuilder.create(methodName).setUri(httpUrl);`| 
| `"request": { ... }` | Parse the request payload and set to HttpEntity. <br/> e.g. `HttpEntity httpEntity = EntityBuilder.create().setContentType(APPLICATION_JSON).setText(reqBody).build();` |
| _None. Nothing to do._ | Parse the response to Java object or JSON String  |
| `"assertions": {JSON structure} ` | Compare the actual response against expected field by field. <br/> - Use multiple `assertThat(...)`. <br/> - Traverse through the response Object field by field <br/> - Or use `JSON Path` to extract value |
| Display **all** the mismatches and fail the test(time saver) | Stop at **first** mismatch and fail the test(unwanted delay in getting feedback)  |
| Straight forward and easy | Step chaining is not straight forward   |

Drawing a _Simile_
===

To draw a _simile_, we can observe an interesting thing in docker-compose. In `docker-compose` we tell the `Docker-Compose` framework(in a YAML file) to spin up certain things at certain ports etc, and then, things are done for us by the framework. 

> _That's declarative way of doing things_

How neat is that? 
Just think of it, for instance, if we had to write code/shell-scripts for the same repetitive tasks, how much hassle we would have gone through!


Introduction
===

> _Testing_ without writing code.

[Zerocode](https://github.com/authorjapps/zerocode) is an open source lib/framework enables API testing via simple declarative JSON steps - REST, SOAP, KAFKA, DB services and much more.

<img width="540"  height="426" alt="ZerocodeLand" src="https://user-images.githubusercontent.com/12598420/52103949-15ca6b00-25e0-11e9-9d7b-b809a24f3659.png">


Test Case Fields
===

### URL

REST end-point or a SOAP end-point or a Kakfa topic or a fully qualified Java class name.

```java
    "url": "/api/v1/register/persons",
```

Or you can mention the FQDN with http or https with port 

```
    "url": "https://apphost.gov.uk/api/v1/register/persons",
```

Or you can mention the Kafka topic name

```
    "url": "kafka-topic:heathrow-inbound",
```

Or you can mention the qualified Java class name,

```
    "url": "uk.gov.DbSqlExecutor",
```

### OPERATION

REST end-point or SOAP end-point
All Http methods such as: POST, PUT, GET, PATCH, DELETE etc

```
    "operation": "POST",
```

Or when we need to call a Java function
```
    "operation": "executeSql",
```

Or when we need to `produce` or `consume` from/to a Kafka topic
```
    "operation": "produce",
```

### REQUEST

For REST end-point or SOAP end-point, request details with _Headers_ and _Body_ payload

```
           "request": {
                "body": {
                    "id": 1000,
                    "name": "Titan"
                }
            },
```

Or when we need to call a _Java_ function with a SQL query as method parameter
```
    "request": "select id, name from customers"
```

Or when we need to _Produce_ or _Consume_ to/from a Kafka topic,
- a `RAW` record
```
           "request": {
                "records": [
                    {
                        "key": "key-101",
                        "value": "Hello Kafka"
                    }
                ]
            },
```

- a JSON record
```
           "request": {
                "recordType" : "JSON",
                "records": [
                    {
                        "key": "key-101",
                        "value": {
                            "name" : "Jey"
                        }
                    }
                ]
            },
```

Or while _Consuming_ we can specify whether to `commitSync` after consuming, `recordType` as RAW or JSON etc.

```
            "request": {
                "consumerLocalConfigs": {
                    "recordType" : "JSON",
                    "commitSync": true,
                    "maxNoOfRetryPollsOrTimeouts": 3
                }
            },
```

### HEADERS
Request with headers and body payload,
```
           "request": {
                "headers": {
                    "X-GOVT-TOKEN": "9-090-9-09-0-99"
                },
                "body": {
                    "id": 1000,
                    "name": "Titan"
                }
            },
```

### ASSERTIONS

For REST services, we need to put the expected response with response _Status_, _Headers_ and _Body_ payload.

Only `status` assertion
```
           "assertions": {
                "status": 200
            }
```

Or `status` and payload `id` assertions
Only `status` assertion
```
           "assertions": {
                "status": 200,
                "body": {
                    "id" : 583231
                }
            }
```

Or `partial` or `full` payload assertions 

```
            "assertions": {
                "status": 200,
                "body": {
                    "login" : "octocat",
                    "id" : 583231,
                    "type" : "User"
                }
            }
```

Or with response `headers` details
```
           "assertions": {
                "status": 200,
                "headers":{
                  "Server":"sit2.hsbc.co.uk",
                  "X-HSBC-BANK":"$NOT.NULL" //<--- "$NOT.NULL" if value is undeterministic
                },
                "body": {
                    "login" : "octocat",
                    "id" : 583231,
                    "type" : "User"
                }
            }
```


For Kafka services, we can put the expected response with response _Status_, _RecordMetadata_.

Only `status` assertion
```
           "assertions": {
                "status": "Ok"
            }
```

Or `status` with `recordMetadata` assertion while _Producing_
```
           "assertions": {
                "status": "Ok",
                "recordMetadata": "$NOT.NULL"
            }
```

Or `size` with `records` assertion while _Consuming_
```
           "assertions": {
                "size": 1,
                "records": [
                    {
                        "key": 101,
                        "value": {
                            "name" : "Jey"
                        }
                    }

                ]
            }
``` 

### STATUS

For REST services or SOAP, we need to put the expected response with response _Status_, _Headers_ and _Body_ payload.

Only `status` assertion
```
           "assertions": {
                "status": 200
            }
```

More Practical Examples (Try at home)
===
+ Http examples are here in [GitHub-Http](https://github.com/authorjapps/zerocode-hello-world/tree/master/src/test/resources)
+ Kafka examples are here in [GitHub-Kafka](https://github.com/authorjapps/hello-kafka-stream-testing/tree/master/src/test/resources/kafka)
+ Java Function Call examples are here in [GitHub-Java](https://github.com/authorjapps/zerocode-hello-world/tree/master/src/test/resources/helloworldjavaexec)


Both Declarative and Extensible
===

It is a light-weight, simple and extensible framework for writing test intentions in simple JSON format that facilitates both declarative configuration and automation. The framework manages the request payload handling and response assertions at the same time, same place. 

It eliminates the repetitive code such as step definitions, test assertions, payload parsing/SerDe and API calls such as Http, Kafka and DB Services. See an example [how](https://github.com/authorjapps/zerocode/wiki/User-journey:-Create,-Update-and-GET-Employee-Details). Its powerful JSON comparison and assertions make the testing cycle a lot easy and clean.

<details>
  <summary>Click to expand</summary>

+ [Kafka application testing](https://github.com/authorjapps/zerocode/wiki/Kafka-Testing-Introduction)

+ [Database persistence testing](https://github.com/authorjapps/zerocode/wiki/Sample-DB-SQL-Executor)

+ [OAuth2 testing](https://github.com/authorjapps/zerocode-hello-world/blob/master/src/test/java/org/jsmart/zerocode/testhelp/tests/OAuth2/OAuth2Test.java)

+ [Many more HelloWorld examples](https://github.com/authorjapps/zerocode/blob/master/README.md#hello-world-), such as Spring boot app testing, Performance testing, Kotlin app testing etc.

</details>

![zc_blocks2](https://user-images.githubusercontent.com/12598420/51440172-1dbf0c80-1cbc-11e9-925c-2afa2ef507c3.png)

> The purpose of Zerocode lib is to make your API tests easy to write, easy to change, easy to share.

See the [Table Of Contents](https://github.com/authorjapps/zerocode#table-of-contents--) for usages and examples.

For Kafka testing approach, visit this page [Kafka-Testing Quick Start](https://github.com/authorjapps/zerocode/wiki/Kafka-Testing-Introduction).
Introduction
===

> _Testing_ without writing code.

[Zerocode](https://github.com/authorjapps/zerocode) is an open source lib/framework enables API testing via simple declarative JSON steps - REST, SOAP, KAFKA, DB services and much more.

<img width="607"  height="479" alt="ZerocodeLand" src="https://user-images.githubusercontent.com/12598420/52103949-15ca6b00-25e0-11e9-9d7b-b809a24f3659.png">


TestCase Fields
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
    "url": "okg.gov.DbSqlExecutor",
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

Or with headers and body payload,
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


Or when we need to call a _Java_ function with a SQL query as method parameter
```
    "request": "select id, name from customers"
```

Or when we need to produce or consume to/from a Kafka topic,
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


### ASSERTIONS

For REST services, we need to put the expected response with response _Status_, _Headers_ and _Body_ payload

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
                  "X-HSBC-BANK":"0909-unique-token" //<--- We can put "$NOT.NULL" here if undeterministic
                },
                "body": {
                    "login" : "octocat",
                    "id" : 583231,
                    "type" : "User"
                }
            }
```

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

It has got the best of best ideas and practices from the community to keep it super simple and the adoption is rapidly growing among the developer/tester community. It alleviates the pain and brings the simplicity in validating the APIs.

It also helps in mocking/stubbing interfacing APIs during the testing cycle. Its approach to IDE based performance testing to generate load/stress on the target application is quite simple, flexible and efficient - It goes a step further enabling you to simply reuse the test(s) from your regression pack.

> The purpose of Zerocode lib is to make your API tests easy to write, easy to change, easy to share.


e.g. Your below User-Journey or ACs(Acceptance Criterias) or a scenario,
```java
AC1:
GIVEN- the POST api end point '/api/v1/users' to create an user,     
WHEN- I invoke the API,     
THEN- I will receive the 201 status with the a user ID and headers 
AND- I will validate the response

AC2:
GIVEN- the REST api GET end point '/api/v1/users/${created-User-Id}',     
WHEN- I invoke the API,     
THEN- I will receive the 200(Ok) status with body(user details) and headers
AND- I will assert the response
```
translates to the below executable JSON in `Zerocode` - Simple and clean ! <br/>
_(See here [a full blown CRUD operation scenario](https://github.com/authorjapps/zerocode/wiki/User-journey:-Create,-Update-and-GET-Employee-Details) with POST, PUT, GET, DELETE example.)_ <br/>

<img width="624" alt="post_get_user" src="https://user-images.githubusercontent.com/12598420/47145467-bc089400-d2c1-11e8-8707-8e2d2e8c3127.png">

Keep in mind: It's simple JSON. <br/>
~~_No feature files, no step-definition code, no extra plugins, no assertThat(...), no statements or grammar syntax overhead._~~ 

And it is simple **declarative** JSON DSL, with the `request/response` fields available for the next steps via the `JSON Path`.

See the [Table Of Contents](https://github.com/authorjapps/zerocode#table-of-contents--) for usages and examples.

For Kafka testing approach, visit this page [Kafka-Testing Quick Start](https://github.com/authorjapps/zerocode/wiki/Kafka-Testing-Introduction).
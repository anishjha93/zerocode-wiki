                        Welcome to the zerocode wiki

Use the sidebar on the right to locate a topic or use **"Ctrl+f"** to find a topic. 👉

If you are not sure where to start, why not take a look at the [What is Zerocode](https://github.com/authorjapps/zerocode/wiki/What-is-Zerocode-testing), then jump to the [Developer's Guide]() below.

Features
===
   * [Introduction](#introduction)
   * [Super Easy and Zero Complexity](#super-easy-and-reduced-complexity)
   * [Lenient and Strict Matching](#lenient-and-strict-matching)
   * [Validation and Verification](#validation-and-verification)
   * [Load Testing Made Easy](#load-testing-made-easy)
   * [Security Testing Made Easy](#security-testing-made-easy)
   * [Dev/Test/BA Collaboration Made Easy](#collaboration-made-easy)
   * [Useful Reports and Dashboards](#useful-reports-and-dashboards)
   * [Smart Projects Using Zerocode](#smart-projects-using-zerocode)

Developer Guide
===
* [Getting started ⛹‍♂](https://github.com/authorjapps/zerocode/wiki/Getting-Started)
* [Supported testing frameworks](#supported-testing-frameworks)
* [A HTTP REST scenario or an user journey](https://github.com/authorjapps/zerocode/wiki/User-journey:-Create,-Update-and-GET-Employee-Details)
* [Running one or more scenarios](#running-a-scenario)
* [Performance Testing - Auto HTTP load generation](https://github.com/authorjapps/zerocode/wiki/Load-or-Performance-Testing-(IDE-based))
* [Performance Testing - JUnit4](https://github.com/authorjapps/performance-tests#multi-scenario-parallel-load)
* [Performance Testing - JUnit5](https://github.com/authorjapps/zerocode/wiki/JUnit5-Jupiter-Parallel-Load-Extension)
* [Kafka Validation](https://github.com/authorjapps/zerocode/wiki/Kafka-Testing-Introduction)
* [Parameterized Scenario](#parameterized-scenario)
* [Using Custom HttpClient](#using-custom-httpclient)
* [Sending query params to HTTP hosts](#sending-query-params-to-http-hosts)
* [Http Basic-Auth security validation](#)
* [Boundary End Point Mocking](#place-holders-for-end-point-mocking)
* [Externalizing RESTful host and port](#externalizing-restful-host-and-port-into-properties-files)
* [Running a scenario in loop](#running-with-scenario-loop)
* [Passing Content-Type header](#passing-content-type-applicationx-www-form-urlencoded-header)
* [Http Max TimeOut or Implicit Wait](#http-max-timeout-or-implicit-wait)
* [Dealing with dynamic arrays](#step-dealing-with-arrays)
* [Chaining multiple steps for a scenario](#chaining-multiple-steps-for-a-scenario)
* [Ignoring step failures](#enabling-ignorestepfailures-for-executing-all-steps-in-a-scenario)
* [Running a Suite of Tests](#running-a-suite-of-tests)
* [Zerocode test-input tokens](#generating-random-strings-random-numbers-and-static-strings)
* [Verifying HTTP error messages](#asserting-general-and-exception-messages)
* [Invoking java utility methods](#calling-java-methodsapis-for-doing-specific-tasks)
* [Re-Using custom properties](#using-any-properties-file-key-value-in-the-steps)
* [Bare JSON Strings as payload](#bare-json-string-still-a-valid-json)
* [Empty HTTP body payload](#bare-json-string-still-a-valid-json)
* [Handling Content-Type with charset-16 or charset-32](#handling-content-type-with-charset-16-or-charset-32)
* [Environment switching in build pipeline](#)
* [SOAP method invocation with xml input](#soap-method-invocation-example-with-xml-input)
* [SOAP method invocation via Corporate Proxy](#soap-method-invocation-where-corporate-proxy-enabled)
* [Chatbot Validation](#chatbot-validation)
* [Python DSL](#python)
* [YAML and JSON Slice And Dice - Solved](#json-slice-and-dice---solved)
* [Inspired by and credits]()
* [References, Discussions and articles](#references-dicussions-and-articles)

Introduction
===
[Zerocode](https://github.com/authorjapps/zerocode/blob/master/README.md) helps you to design better Test Cases for your business functionalities and then maintain them easily to avoid sleepless nights. You do this simply by configuring, declaring and executing the scenario-files enabling you to completely eliminate the glue or boilerplate coding.

Super Easy and Reduced Complexity
===
Simply annotate your test method with **@Test** and run like `JUnit` tests. 

Testing becomes an easy and effortless job due to the **simplicity** nature of YAML/JSON formats and their native support by popular IDEs e.g. `Eclipse /IntelliJ /NetBeans` etc with no extra plugin. Super easy!

### Reduced Complexity
It enables us to write automation tests for our 
+ `API End Point Validations`, 
+ `Performance(Load/Stress) Validations`, 
+ `Consumer Contract Validations`, 
+ `End to End User Journey`, 
+ `In Memory Application Validations`  and 
+ `API Security Validations` etc, 

at the **speed** of writing **JUnit** tests.

> It makes the tests declarative, configurable, and accurate.

Lenient and Strict Matching
===
Zerocode provides both [LENIENT and STRICT](https://github.com/authorjapps/zerocode/wiki/Strict-Mode-Payload-Comparison) matching mode for result comparison.


Validation and Verification
===
Zerocode enables you to achieve both [Verification and Validation](https://en.wikipedia.org/wiki/Verification_and_validation).


Load Testing Made Easy
===
Visit here to learn [JUnit way of load and stress generation](https://github.com/authorjapps/zerocode/wiki/Load-or-Performance-Testing-(IDE-based))

Security Testing Made Easy
===
Zerocode gives you out of the box **SSL** enabled Http Client and **SOAP** Client along with the optional MIME type converters e.g. XML to JSON if needed to increase test readability. It provides you with the options to configure **Corporate Proxy** at runtime to allow API invocations via `corporate-proxies`.

Zerocode has built general functionality which enables you to **extend** and enrich the **framework** behaviour by simply executing external Java methods as utility-functions to achieve business goals rather than putting every feature into the core framework. 


Useful Reports and Dashboards
===
Zerocode prints the request, response into the console as well as to the log file in the `/target` folder in a **human/business readable** format, along with producing granular report in the `CSV format` and `Interactive Fuzzy Search Enabled Chart report`. 

You can `search and filter` the test report by `author` or `test-scenario` or `test-step` or any relevant matching text making it super easy to trace a step in the context of a scenario or user-journey.

### Sample Test Report

Test reports are generated into  `/target`  folder every time the tests are run. Sample [reports are here](https://github.com/authorjapps/zerocode/blob/master/README.md#6) format. 

### Traceable Test Logs

Test logs are generated in the console as well as an user-defined log file. Default log location is  `target/logs/zerocode_rest_bdd_logs.log` . 

_::Note::_
Every **step** can be traced with an **auto** generated **STEP-ID** to correlate a request with its response.

e.g.
### If the test passed: 
```java
--------- CORRELATION-ID: e6170365-94e7-49dc-a1a3-5e102468acd9 ---------
requestTimeStamp:2017-12-20T10:00:48.840
step:get_same_employee
url:http://localhost:9999/api/testing/v1/persons/UK1001
method:GET
request:
{ } 
--------- CORRELATION-ID: e6170365-94e7-49dc-a1a3-5e102468acd9 ---------
Response:
{
  "status" : 200,
  "headers" : {
    "Date" : [ [ "Wed, 20 Dec 2016 03:00:48 GMT" ] ]
  },
  "body" : {
    "id" : "UK1001",
    "name" : "Gov UK",
    "addresses" : [ {
      "line1" : "HOME, AECS Layout, ZIP-56094"
      }
    ]
  }
}
*responseTimeStamp:2017-12-20T10:00:48.847 
*Response delay:7.0 milli-secs 
---------> Expected Response: <----------
{
  "status" : 200,
  "body" : {
    "id" : "UK1001"
  }
} 
-done-
```

### If the test failed: 

Scenario failed for :- 

```java
[test_get_request_response_rainy_scene.json] 
	|
	|
	+---Step --> [get_an_employee_detail] 

Failures:
--------- 
Assertion path '$.status' with actual value '200' did not match the expected value '400'
```

Collaboration Made Easy
===
Zerocode aims to make development and testing **easier and faster**, not _harder and slower_. Enables both Dev-team and Test-team to collaborate towards the highest **quality** of the software. 

<br/>
<br/>

                                               Developer's Guide


Supported testing frameworks
===
 * [JUnit4](http://junit.org)
 * [JUnit5 Jupiter](https://github.com/authorjapps/zerocode/wiki/JUnit5-Jupiter-Parallel-Load-Extension)


Running a scenario
===
`ZeroCodeUnitRunner` is the JUnit runner which enables us to run a single or more test-cases from a JUnit test-class.

e.g.
```java
@TargetEnv("app_sit1.properties")
@RunWith(ZeroCodeUnitRunner.class)
public class GitHubHelloWorldTest {

   @Test
   @Scenario("screening_tests/test_happy_flow.yml")
   public void testHappyFlow(){
   }

   @Test
   @Scenario("screening_tests/test_negative_flow.yml")
   public void testNegativeFlow(){
   }

}
```

Parameterized scenario
===
To run the scenario steps for each parameter from a list of values or CSV rows.

Examples:
+ YAML
<img width="460" alt="para yaml" src="https://user-images.githubusercontent.com/12598420/63848014-35304780-c9b9-11e9-85da-8419b5e49ded.png">

+ JSON
<img width="470" alt="para json" src="https://user-images.githubusercontent.com/12598420/63848012-35304780-c9b9-11e9-9e49-99b475ed0fa8.png">

Visit Wiki for details.
+ [Parameters as values - Wiki](https://github.com/authorjapps/zerocode/wiki/Parameterized-Testing-From-List-of-Values)
+ [Parameters as CSV rows - Wiki](https://github.com/authorjapps/zerocode/wiki/Parameterized-Testing-From-CSV-rows)

Using Custom HttpClient
===
Visit [HelloWorld](https://github.com/authorjapps/zerocode-hello-world) repo to see an example.

See example code:
> http-testing/src/main/java/org/jsmart/zerocode/zerocodejavaexec/httpclient/CustomHttpClient.java

e.g.
```java
@TargetEnv("apihost_env1.properties")
@UseHttpClient(CustomHttpClient.class) //<--- Use your own HTTP client.
@RunWith(ZeroCodeUnitRunner.class)
public class HelloWorldCustomHttpClientSuite {
}
```

Sending query params to HTTP hosts
===
You can pass query params in the usual way in the URL e.g. `?page=1&page_size=5` -or-
You can pass them in the request as below.
```
...
            "request": {
                "queryParams":{
                    "page":1,
                    "per_page":6
                }
            }
...
```

Http Basic-Auth security validation
===
You can validate `Basic Auth` in so many ways, it depends on your project requirement. Most simplest one is to pass the `base64 basicAuth` in the request headers as below - e.g. `USERNAME/PASSWORD` as `charaanuser/passtwitter`

Zerocode framework helps you to achieve this, but has nothing to do with Basic-Auth. It uses `Apache Http Client` behind the scenes, this means whatever you can do using `Apache Http Client`, you can do it simply using `Zerocode`.

+ Positive scenario
```javaScript
{
    "name": "get_book_using_basic_auth",
    "url": "http://localhost:8088/api/v1/white-papers/WP-001",
    "method": "GET",
    "request": {
        "headers": {
            "Authorization": "Basic Y2hhcmFhbnVzZXI6cGFzc3R3aXR0ZXI=" // You can generate this using Postman or java code
        }
    },
    "verify": {
        "status": 200, // 401 - if unauthorized. See negative test below
        "body": {
            "id": "WP-001",
            "type": "pdf"
        }
    }
}        
```

+ Negative scenario
```
{
    "name": "get_book_using_wrong_auth",
    "url": "http://localhost:8088/api/v1/white-papers/WP-001",
    "method": "GET",
    "request": {
        "headers": {
            "Authorization": "Basic aWRONG-PASSWORD"
        }
    },
    "verify": {
        "status": 401 //401(or similar code whatever the server responds), you can assert here.
        "body": {
            "message": "Unauthorized" 
        }
    }
}        
```
+ If your requirement is to put basic auth for all the API tests e.g. GET, POST, PUT, DELETE etc commonly in the regression suite, then you can put this `"Authorization"` header into your SSL client code. 

Visit here to see an [example scenario](https://github.com/authorjapps/consumer-contract-tests/blob/master/src/test/java/org/jsmart/zerocode/testhelp/tests/basicauth/BasicAuthContractTest.java).

+ In your custom http-client, you add the header to the request at one central place, which is common to all the API tests.
See: `org.jsmart.zerocode.httpclient.CorpBankApcheHttpClient#addBasicAuthHeader` in the [http-client code](https://github.com/authorjapps/consumer-contract-tests/blob/master/src/main/java/org/jsmart/zerocode/httpclient/CorpBankApcheHttpClient.java) it uses.

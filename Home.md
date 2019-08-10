<br/>

> _Use the sidebar on the right for all topics or "Ctrl+f" search for any topic_

Welcome To Zerocode
===

_(For helps and usage- Visit [Table of Contents](https://github.com/authorjapps/zerocode#table-of-contents--). Visit here for a [Quick Introduction to Hassle-Free Declarative Testing](https://github.com/authorjapps/zerocode/wiki/What-is-Zerocode-testing))_

## Table Of Contents
   * [Welcome To Zerocode](#welcome-to-zerocode)
   * [Super Easy to Write BDD Tests](#super-easy-to-write-bdd-tests)
   * [Zerocode Tokens](#zerocode-tokens)
   * [No Complexity Involved](#no-complexity-involved)
   * [Plug and Play Security Testing](#plug-and-play-security-testing)
   * [Beautiful and Useful Reporting](#beautiful-and-useful-reporting)
   * [Easy to Collaborate](#easy-to-collaborate)
   * [Handy Even For Manual Testers or Architects](#handy-even-for-manual-testers-or-architects)
      * [Why?](#why)
      * [How?](#how)
      * [Sample Test Report](#sample-test-report)
      * [Sample Test Logs](#sample-test-logs)
   * [Inspired By](#inspired-by)
      * [Honorable references and credits](#honorable-references-and-credits)
   * [Contribute](#contribute)

Super Easy to Write BDD Tests
===

[Zerocode](https://github.com/authorjapps/zerocode/blob/master/README.md) helps you to design better Test Cases for your business features, then maintain and update them easily to avoid sleepless nights. It is built on extending the **Junit core runners**. You simply annotate your test method with JUnit **@Test** and run like JUnit tests, as well as optionally you can use `Suite` Runners for CI builds and env switching. Testing becomes an easy and effortless job due to the **simplicity** nature of JSON and the native support by popular IDEs e.g. Eclipse /IntelliJ /NetBeans etc with no extra plugin. Super easy !

Zerocode Tokens
===

[Zerocode](https://github.com/authorjapps/zerocode/blob/master/README.md) provides built-in tokens that help with your testing ranging from generating random numbers through to accessing system properties, currently Zerocode offers the following tokens:

+ [PREFIX_ASU](#todo)
+ [RANDOM_NUMBER](#todo)
+ [RANDOM_STRING_PREFIX](#todo)
+ [STATIC_ALPHABET](#todo)
+ [LOCALDATE_TODAY](#todo)
+ [LOCALDATETIME_NOW](#todo)
+ [SYSTEM_PROPERTY](#todo)
+ [SYSTEM_ENV](#todo)
+ [XML_FILE](#todo)
+ [RANDOM_UU_ID](#todo)
+ [RECORD_DUMP](#todo)

No Complexity Involved
===

Your tests will not be cumbersome and complex anymore. Zerocode makes your tests independent, complete and structured and easily maintainable by the team or the new comers. It enables you to write your `API End Point Tests`, `Consumer Contract Tests`, `End to End Tests` and `Performance Tests(Load/Stress)` etc, at the **speed** of writing **JUnit** tests with accuracy transparent to all stakeholders. 

Zerocode at its core uses simple and powerful libs like `Jackson` for JSON assertions, `Apache HttpClient` for invoking REST and SOAP APIs, `Google Guice` for `DI` and Spring style place holders `${JSON Path}` for result assertions. It does not limit you to use Apache HttpClient, it enables you to easily override the framework behaviour with `@UseHttpClient` to use e.g. `UniRest` HttpClient, `RestEasy` HttpClient or any of your custom HttpClient that suits your project needs. 

Plug and Play Security Testing
===
Zerocode gives you out of the box **SSL** enabled Http Client and **SOAP** Client along with the optional MIME type converters e.g. XML to JSON if needed to increase test readability. It provides you with the options to configure **Corporate Proxy** at runtime to allow API invocations via proxies.

Zerocode has built general functionality which enables you to **extend** and enrich the **framework** behaviour by simply executing external Java methods to achieve business goals rather than putting every feature into the core framework. 

Beautiful and Useful Reporting
===

Zerocode prints the request, response into the console as well as to the log file in the `/target` folder in a **human/business readable** format, along with producing granular report in the `CSV format` and `Interactive Fuzzy Search Enabled Chart report`. You can `search and filter` the test report by `author` or `test-scenario` or `test-step` or any relevant matching text making it super easy to trace a step in the context of a scenario or user-journey.

Easy to Collaborate
===

Zerocode aims to make development and testing **easier and faster**, not harder and slower. Allows both Dev team and Test team to collaborate towards better better **quality** of the software. Even the managers and BAs can read and understand the tests easily if they want to.


Handy Even For Manual Testers or Architects
===

Handy tool even for manual testers dealing with `REST api`, `SOAP api` and `DB integration` tests [much more](https://github.com/authorjapps/zerocode#table-of-contents--) to keep it side by side of Postman rest-client!

Learn how the ZeroCode testing library can make your life easier and writing tests faster by simply putting your **thoughts** into **executable test** scenarios and **not enforcing** you to write boiler plate glue code and sticky wrappers around your tests adding extra overhead/maintenance.

It allows you to **override** the framework behavior by your own **java code** which becomes not only **reusable** but becomes a **part of the framework**.

See the [HelloWorldTest](https://github.com/authorjapps/zerocode-hello-world/blob/master/src/test/java/org/jsmart/zerocode/testhelp/tests/helloworld/JustHelloWorldTest.java)

## Why?
Because there is a clear and obvious pattern for REST api or SOAP or any other api testing which Zerocode solves efficiently without adding any syntax overhead, that means it makes your testing process very very easy and accurate.

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

and it is **declarative** DSL, with the `request/response` fields available for the next steps via the `JSON Path`.
Then you just stick this into a JSON file named e.g. `post_n_get_user_journey_test.json`, anywhere in the  `test/resources` folder,

and run the code like below by pointing to that JSON file. That's it.
```
@TargetEnv("github_host.properties")
@RunWith(ZeroCodeUnitRunner.class)
public class MyRestApiTest{

    @Test
    @JsonTestCase("post_n_get_user_journey_test.json")
    public void testPostAndGet_happy() throws Exception {
    }
}
```

Keep in mind: It's simple JSON. <br/>
~~_No feature files, no extra plugins, no statements or grammar syntax overhead._~~ 

## How?
* HelloWorld Examples and samples are here to [download or clone](https://github.com/authorjapps/zerocode/blob/master/README.md#hello-world)  

* The  **latest**  maven dependency can be found here at 
[Maven central - Old releases](https://mvnrepository.com/artifact/org.jsmart/zerocode-rest-bdd)
[Maven central - New releases](https://mvnrepository.com/artifact/org.jsmart/zerocode-tdd)

```xml
<dependency>
    <groupId>org.jsmart</groupId>
    <artifactId>zerocode-rest-bdd</artifactId>
    <version>1.3.x</version>
</dependency>
```
* You can organize and arrange the tests to suit your requirements, by folder/feature/release wise

## Sample Test Report

Test reports are generated into  `/target`  folder every time the tests are run. Sample [reports are here](https://github.com/authorjapps/zerocode/blob/master/README.md#6) format. 

## Sample Test Logs

Test logs are generated in the console as well as into the log file in a readable JSON format  `target/logs/zerocode_rest_bdd_logs.log` . In case of a test failure it exactly lists which field or fields didn't match with their  JSON Path in a tree view.
Note-
Every **step** is assigned with an **auto** generated **STEP-ID** to relate request with response of that **step**.

e.g.
If test passed: 
```
--------- CORRELATION-ID: e6170365-94e7-49dc-a1a3-5e102468acc2 ---------
requestTimeStamp:2017-12-20T10:00:48.840
step:get_same_employee
url:http://localhost:9999/api/testing/v1/persons/UK1001
method:GET
request:
{ } 
--------- CORRELATION-ID: e6170365-94e7-49dc-a1a3-5e102468acc2 ---------
Response:
{
  "status" : 200,
  "headers" : {
    "Date" : [ [ "Wed, 20 Dec 2017 03:00:48 GMT" ] ],
    "Last-Modified" : [ [ "Wed, 20 Dec 2017 03:00:48 GMT" ] ],
    "Transfer-Encoding" : [ [ "chunked" ] ],
    "Content-Type" : [ [ "application/json" ] ],
    "Connection" : [ [ "keep-alive" ] ]
  },
  "body" : {
    "id" : "UK1001",
    "name" : "Bobby Lion",
    "addresses" : [ {
      "line1" : "HOME, AECS Layout, ZIP-56094"
    }, {
      "line1" : "OFFICE, Newark, ZIP-730290"
    } ]
  }
}
*responseTimeStamp:2017-12-20T10:00:48.847 
*Response delay:7.0 milli-secs 
---------> Assertion: <----------
{
  "status" : 200,
  "body" : {
    "id" : "UK1001"
  }
} 
-done-
```

If test failed: 
```
--------- CORRELATION-ID: 8ad5c1fe-31cb-4e46-a8ba-7500a00c2199 ---------
requestTimeStamp:2017-12-20T10:02:01.163
step:get_an_employee_detail
url:http://localhost:9999/api/testing/v1/persons/UK1001
method:GET
request:
{ } 
--------- CORRELATION-ID: 8ad5c1fe-31cb-4e46-a8ba-7500a00c2199 ---------
Response:
{
  "status" : 200,
  "headers" : {
    "Date" : [ [ "Wed, 20 Dec 2017 03:02:01 GMT" ] ],
    "Last-Modified" : [ [ "Wed, 20 Dec 2017 03:02:01 GMT" ] ],
    "Transfer-Encoding" : [ [ "chunked" ] ],
    "Content-Type" : [ [ "application/json" ] ],
    "Connection" : [ [ "keep-alive" ] ]
  },
  "body" : {
    "id" : "UK1001",
    "name" : "Bobby Lion",
    "addresses" : [ {
      "line1" : "HOME, AECS Layout, ZIP-56094"
    }, {
      "line1" : "OFFICE, Newark, ZIP-730290"
    } ]
  }
}
*responseTimeStamp:2017-12-20T10:02:01.315 
*Response delay:152.0 milli-secs 
---------> Assertion: <----------
{
  "status" : 400,
  "body" : {
    "id" : "UK1001"
  }
} 
-done-

java.lang.RuntimeException: Assertion failed for :- 

[test_get_request_response_rainy_scene.json] 
	|
	|
	+---Step --> [get_an_employee_detail] 

Failures:
--------- 
Assertion path '$.status' with actual value '200' did not match the expected value '400'

```

Inspired By
===
### Honorable references and credits

- [SkyScreamer](https://github.com/skyscreamer/JSONassert) 
- [Pyresttest](https://github.com/svanoort/pyresttest) 
- [Spring](https://spring.io)
- [Apache JMeter](https://jmeter.apache.org/) 
- [JUnit5 Jupiter Engine](https://junit.org/junit5/) 

Pyresttest's JSON/YAML based test-DSL inspired many of Zerocode's Http DSL and test-config features.

Apache JMeter's intuitive load configuration inspired various Zerocode's declarative Load Testing DSL.

SkyScreamer's lenient mode smart JSON comparison inspired Zerocode's lenient JSON comparison feature.

Spring's popular token/placeholder resolver inspired Zerocode's runtime token/placeholder resolver feature.

Jupiter Junit5's easy and declarative approach to parameterized testing inspired Zerocode's parameterized testing feature.

We also give credit to the team members at HomeOffice(GOV.UK), Mizuho Bank, CMC Markets, HSBC Bank, Barclays and Zohocorp whose comments have helped to shape the lib.

## Contribute
Raise [issues](https://github.com/authorjapps/zerocode/issues) and [contribute](https://github.com/authorjapps/zerocode/blob/master/CONTRIBUTING.md) to improve zerocode by becoming a contributor yourself.

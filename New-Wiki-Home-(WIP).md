Welcome To Zerocode Wiki. Use the sidebar on the right to locate a topic or use **"Ctrl+f"** to find a topic 👉

If you are not sure where to start, why not take a look at the [What is Zerocode](https://github.com/authorjapps/zerocode/wiki/What-is-Zerocode-testing), then jump to the [Developer's Guide]().

Features
===
   * [Introduction](#introduction)
   * [Super Easy and Reduced Complexity](#super-easy-and-reduced-complexity)
   * [Lenient and Strict Matching](#lenient-and-strict-matching)
   * [Validation and Verification](#validation-and-verification)
   * [Load Testing Made Easy](#load-testing-made-easy)
   * [Security Testing Made Easy](#security-testing-made-easy)
   * [Useful Reports and Dashboards](#useful-reports-and-dashboards)
   * [Dev/Test/BA Collaboration Made Easy](#collaboration-made-easy)
   * [Smart Projects Using Zerocode](#smart-projects-using-zerocode)

Developer Guide
===
* [Getting started ⛹‍♂](#getting-started-)
* [Running a scenario](#running-a-single-scenario-test)
* [Performance Testing - Automating HTTP load generation](#)
* [Performance Testing - JUnit4](#)
* [Performance Testing - JUnit5](#)
* [Supported testing frameworks](#supported-testing-frameworks)
* [A HTTP REST scenario or an user journey](#single-scenario-with-single-step)
* [Kafka Validation](#kafka-testing)
* [Parameterized Scenario](#paramterized-scenario)
* [Using Custom HttpClient](#overriding-with-custom-httpclient-with-project-demand)
* [Http Basic-Auth security validation](#http-basic-authentication-step-using-zerocode)
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
* [Using WireMock for mocking dependent end points](#using-wiremock-for-mocking-dependent-end-points)
* [Sending query params to HTTP hosts](#sending-query-params-in-url-or-separately)
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
Zerocode aims to make development and testing **easier and faster**, not _harder and slower_. Allows both Dev-team and Test-team to collaborate towards the highest **quality** of the software. 

Welcome To Zerocode Wiki. Use the sidebar on the right to locate a topic or use **"Ctrl+f"** to find a topic 👉

If you are not sure where to start, why not take a look at the [What is Zerocode](), then jump to the [Developer's Guide]().

Features
===
   * [Introduction](#introduction)
   * [Super Easy and Reduced Complexity](#super-easy-and-reduced-complexity)
   * [Lenient and Strict Matching](#lenient-and-strict-matching)
   * [Validation and Verification](#validation-and-verification)
   * [Load Testing Made Easy](#load-testing-made-easy)
   * [Security Testing Made Easy](#security-testing-made-easy)
   * [Useful Reports and Dashboards](#useful-reports-and-dashboards)
   * [Collaboration Made Easy](#collaboration-made-easy)

Developer Resources
===
   * [Zerocode Tokens](#zerocode-tokens)
   * [Inspired By and Credits](#inspired-by)
   * [Contribute](#contribute)
   * [Copyrights](#copyright)

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


Zerocode Tokens
===
[Zerocode](https://github.com/authorjapps/zerocode/blob/master/README.md) provides built-in tokens that help with your testing ranging from generating random numbers through to accessing system properties. Currently Zerocode offers the following tokens:

+ [LOCALDATE.TODAY](https://github.com/authorjapps/zerocode/wiki/Token:-LocalDate-Today)
+ [LOCALDATETIME.NOW](https://github.com/authorjapps/zerocode/wiki/Token:-LocalDateTime-Now)
+ [RANDOM.NUMBER](https://github.com/authorjapps/zerocode/wiki/Token:-Random-Number)
+ [RANDOM.STRING.PREFIX](https://github.com/authorjapps/zerocode/wiki/Token:-Random-String)
+ [RANDOM.UUID](https://github.com/authorjapps/zerocode/wiki/Token:-Random-UUID)
+ [RECORD.DUMP](https://github.com/authorjapps/zerocode/wiki/Token:-Record-Dump)
+ [STATIC.ALPHABET](https://github.com/authorjapps/zerocode/wiki/Token:-Static-Alphabet)
+ [SYSTEM.ENV](https://github.com/authorjapps/zerocode/wiki/Token:-System-Environment)
+ [SYSTEM.PROPERTY](https://github.com/authorjapps/zerocode/wiki/Token:-System-Property)
+ [XML.FILE](https://github.com/authorjapps/zerocode/wiki/Token:-XML-File)

_Verifications/Assertions Tokens:_
+ [CONTAINS.STRING]()
+ [CONTAINS.STRING.IGNORECASE]()
+ [MATCHES.STRING]()
+ [IS.ONE.OF]()
+ [IS.NULL]()
+ [IS.NOTNULL]()
+ [GT]()
+ [LT]()
+ [SIZE]()
+ [LOCAL.DATETIME.AFTER]()
+ [LOCAL.DATETIME.BEFORE]()


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

SkyScreamer's lenient/ and strict mode JSON comparison inspired Zerocode's result matching features.

Spring's popular token/placeholder resolver inspired Zerocode's test-input token/placeholder resolving feature.

JUnit5 Jupiter engine's easy and declarative approach to parameterized testing inspired Zerocode's parameterized testing feature.

Powered by [open-source software](https://github.com/authorjapps/zerocode/wiki/Powered-by-open-source-software).

IDE Credits
![Jetbrains](https://github.com/authorjapps/zerocode/blob/master/images/jetbrains.svg)

## Contribute
Raise [issues](https://github.com/authorjapps/zerocode/issues) and [contribute](https://github.com/authorjapps/zerocode/blob/master/CONTRIBUTING.md) to improve zerocode by becoming a contributor yourself.

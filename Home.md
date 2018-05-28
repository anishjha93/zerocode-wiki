## Zerocode Wiki

(For helps and usage- Visit [Table of Contents](https://github.com/authorjapps/zerocode#table-of-contents--))

Zerocode helps you to design better Test Cases for your business features, maintain and update easily to avoid sleepless nights. It is built on extending the **Junit core runners**. You simply annotate your test method with JUnit **@Test** and run like unit tests, as well optionally you can use`Suite` Runner for CI builds. Testing becomes an easy and effortless job due to the **simplicity** nature of JSON and the native support by popular IDEs e.g. Eclipse /IntelliJ /NetBeans etc with no extra plugin. 

Your tests will not be cumbersome and complex anymore. Zerocode makes your tests independent, complete and structured and easily maintainable by the team or the new comers. It enables you to write your `API End Point Tests`, `Consumer Contract Tests` and `End to End Tests` etc, at the **speed** of writing **JUnit** tests.

Zerocode at its core uses simple and powerful libs like `Google Jackson` for JSON assertions, `Apache HttpClient` for invoking REST and SOAP APIs, and Spring style place holders `${JSON Path}` for result assertions. It does not limit you to use Apache HttpClient, it enables you to easily override the framework behaviour with `@UseHttpClient` to use e.g. UniRest HttpClient, RestEasy HttpClient or any of your custom HttpClient that suits your project needs. 

Zerocode gives you out of the box **SSL** enabled Http Client and **SOAP** Client along with the optional MIME type converters e.g. XML to JSON if needed to increase test readability. It provides you with the options to configure **Corporate Proxy** at runtime to authenticate API invocations.

Zerocode has built general functionality which enables you to **extend** and enrich the **framework** behaviour by simply executing external Java methods to achieve busines goals rather than putting every feature into the core framework. 

Zerocode prints the request, response into the console as well as to the log file in the `/target` folder in a **human readable** format, along with producing granular report in the `CSV format` and `Interactive Fuzzy Search Enabled Chart report`. You can `search and filter` the junit report by `author` or `test-scenario` or `test-step` or any relevant matching text making it easy to trace the step in the context of a scenario or user journey.

Zerocode aims to make development and testing **easier and faster**, not harder and slower. Allows both Dev team and Test team to contribute towards better test cases which finally makes a product better **quality**. Even the managers and BAs can read and understand the tests as the tests don't involve programming.
Testing REST apis with Zero Code JSON assertion based REST test framework lib. Great tool for `REST api`, `SOAP api` and `DB integration` test automation and [much more](https://github.com/authorjapps/zerocode#table-of-contents--)!

Learn how the ZeroCode testing library can make your life easier and writing tests faster by simply putting your **thoughts** into **executable test** scenarios and **not enforcing** you to write boiler plate glue code and sticky wrappers around your tests. Tests become neat and clean as well as easily maintainable.

You have still options to write the `glue code` if you have a need to do, also it allows to **override** the framework behavior by your own **java code** which becomes not only **reusable** but becomes **part of the framework**.

See the [HelloWorldTest](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/java/org/jsmart/zerocode/testhelp/tests/HelloWorldTest.java)

## Why?

* It's simple and easy to use, no boiler-plate code needed for testers and developers or any stakeholders to understand what's being tested.

* Automate and write your end-to-end tests and integration-tests at the speed of writing unit tests 

* Imagine you have a  REST api  to test with following behavior e.g.

```
Usecase scenario: REST API to get an empoyee details,
URL: http://host:port/api/v1/persons/1001,
Operation: GET,
Expected JSON Response body as-
{
   "id": 1001,
   "name": "Larry P",
   "job": "Full Time"
},
Expected Response status: 200
```

and your happy scenario test case code exactly looks like below e.g.

```javaScript
{
      "name": "get_emp_details",
      "url": "http://host:port/api/v1/persons/1001,",
      "operation": "GET",
      "request": {},
      "assertions": {
          "status": 200,
          "body": {
             "id": 1001,
             "name": "Larry P",
             "job": "Full Time"
          }
      }
}
```

, your negative scenario test case code exactly looks like below e.g.
```
{
      "name": "get_not_existing_emp_details",
      "url": "http://host:port/api/v1/persons/9999",
      "operation": "GET",
      "request": {},
      "assertions": {
          "status": 404,
          "body": {
             "message": "No such employee exists"
          }
      }
}
```

and if you need them together as a scenario, then the code looks exacly like below
```
{
    "scenarioName": "GET Employee Details Happy and Sad path",
    "steps": [
        {
            "name": "get_emp_details",
            "url": "http://host:port/api/v1/persons/1001,",
            "operation": "GET",
            "request": {},
            "assertions": {
                "status": 200,
                "body": {
                    "id": 1001,
                    "name": "Larry P",
                    "job": "Full Time"
                }
            }
        },
        {
            "name": "get_non_existing_emp_details",
            "url": "http://host:port/api/v1/persons/9999",
            "operation": "GET",
            "request": {},
            "assertions": {
                "status": 404,
                "body": {
                    "message": "No such employee exists"
                }
            }
        }
    ]
}
```

, then you just stick these into a JSON file named e.g.  `"get_happy_and_sad.json"`  anywhere in the  `test/resources` folder,

and run the code like below  pointing to that JSON file  and then you are done with testing.
```
@RunWith(ZeroCodeUnitRunner.class)
@HostProperties(host="http://localhost", port=8088, context = "")
public class MyRestApiTest{

    @Test
    @JsonTestCase("get_happy_and_sad.json")
    public void testGetHappyAndSad() throws Exception {
    }
}
```
## How?
* Zerocode Examples and samples are here to [download or clone](https://github.com/authorjapps/helpme/tree/master/zerocode-rest-help)  

* The  **latest**  maven dependency can be found here at [latest-maven-central-zerocode](http://search.maven.org/#search%7Cga%7C1%7Czerocode-rest-bdd)

```
<dependency>
    <groupId>org.jsmart</groupId>
    <artifactId>zerocode-rest-bdd</artifactId>
    <version>1.1.27</version>
</dependency>
```
* You can organize and arrange the tests to suit your requirements, by folder/feature/release wise

* You can add as many tests as you want by just annotating the test method. See [here](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/java/org/jsmart/zerocode/testhelp/tests/ZeroCodeSampleUnitRunner.java) some examples

You can assert the entire JSON in the assertion block however complex and hierercical structure it might be, just by  copy paste  of the entire JSON. Hassle free, no serialize/deserialze is needed !

You can also use only the perticular section or even an element of a JSON using JSON path e.g.  `$.get_emp_details.response.body.id`  which will resove to  1001  in the above case.

You can test the consumer contract APIs by creating specific runners specific to clients.

## Examples

* Working examples of various use cases are here. 

* You can use place holders for various outcomes when you need.

* Examples of some features are here

    * * Re-using [Request/Response](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/00_sample_test_scenarios/13_random_and_static_string_number_place_holders.json) via [JSON Path](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/00_sample_test_scenarios/15_place_holders_of_request_response.json)

    * * Asserting [NULL or NOT NULL](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/00_sample_test_scenarios/06_asserting_null_or_notnull_json_content.json)

    * * Executing [External Java Method](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/00_sample_test_scenarios/11_execute_local_java_program.json)

    * * Chaining steps [using previous request or response](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/00_sample_test_scenarios/12_chaining_multiple_steps_with_prev_response.json) 

    * * Generating [Custom ID example](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/01_vanila_placeholders/01_generatinng_ids_and_sharing_among_steps.json) .

    * * Asserting  part of a string . See [$CONTAINS.STRING](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/00_sample_test_scenarios/09_asserting_string_messages.json)
    
    * * Using custom Http Client upon project demand. See [Using Custom Http Clinet](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/java/org/jsmart/zerocode/testhelp/zcmore/ZeroCodeUnitRunnerWithCustomHttpClient.java)
    
    * * Passing value in headers. See [headers example](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/00_sample_test_scenarios/16_passing_headers_to_rest_apis.json)

    * *  More place holders and their usages are [here](https://github.com/authorjapps/zerocode#99) and the link to the [README](https://github.com/authorjapps/zerocode/blob/master/README.md) file is here.

## Test Report

Test reports are generated into  `/target`  folder everytime the tests are run. Sample [reports are here](https://github.com/authorjapps/zerocode#generated-reports-and-charts) format. 

## Test Logs

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

## Contribute
Raise [issues](https://github.com/authorjapps/zerocode/issues) and [contribute](https://github.com/authorjapps/zerocode/blob/master/CONTRIBUTING.md) to improve zerocode library and add more essential features which you might need by yourself.

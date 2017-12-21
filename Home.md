
**Testing REST apis with Zero Code JSON based BDD test framework lib. Great tool for test automation!**

Get rid of lot of boilerplate codes! Learn how the ZeroCode testing library will make your life easier.

See the [HelloWorldTest](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/java/org/jsmart/zerocode/testhelp/tests/HelloWorldTest.java)

## Why?

* It's simple and easy to use, no clutters or boiler-plate code for testers and developers or any stakeholders to understand what's being tested. Great time saver!

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

```
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

* The  latest  maven dependency can be found here at [latest-maven-central-zerocode](http://search.maven.org/#search%7Cga%7C1%7Czerocode-rest-bdd)

```
<dependency>
    <groupId>org.jsmart</groupId>
    <artifactId>zerocode-rest-bdd</artifactId>
    <version>1.1.18</version>
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

    * * Using [GREATER THAN or LESS THAN](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/00_sample_test_scenarios/07_asserting_greaterthan_lesserthan_number.json)

    * * Executing [External Java Method](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/00_sample_test_scenarios/11_execute_local_java_program.json)

    * * Chaining steps [using previous request or response](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/00_sample_test_scenarios/12_chaining_multiple_steps_with_prev_response.json) 

    * * Using [Random Number or Random String](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/00_sample_test_scenarios/13_random_and_static_string_number_place_holders.json) as ID

    * * Generating [Custom ID example](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/01_vanila_placeholders/01_generatinng_ids_and_sharing_among_steps.json) .

    * * Using  loop  for  performance testing . See [loop example](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/00_sample_test_scenarios/02_using_step_loop.json) 

    * * Asserting [empty array](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/00_sample_test_scenarios/05_asserting_empty_array.json) 

    * * Asserting  part of a string . See [$CONTAINS.STRING](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/00_sample_test_scenarios/09_asserting_string_messages.json)
    
    * * Using custom Http Client upon project demand. See [Using Custom Http Clinet](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/java/org/jsmart/zerocode/testhelp/zcmore/ZeroCodeUnitRunnerWithCustomHttpClient.java)
    
    * * Passing value in headers. See [headers example](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/tests/00_sample_test_scenarios/16_passing_headers_to_rest_apis.json)

    * *  More place holders and their usages are [here](https://github.com/authorjapps/zerocode#99) and the link to the [README](https://github.com/authorjapps/zerocode/blob/master/README.md) file is here.

    * * Asserting size or length of an array. Use  $<path.to.array>.SIZE e.g. in the assertion JSON use
```
"persons.SIZE": 4  
or 
"addresses.SIZE": 2 etc
```

## Test Report

Test reports are generated into  /target  folder everytime the tests are run. Sample reports are here in [.html spike chart](http://htmlpreview.github.io/?https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/zz_reports/zerocode_results_chart_2016-07-30T09-55-53.056.html) and [.csv tabular](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/zz_reports/zerocode_full_report_2016-07-30T11-44-14.512.csv) format. 

## Test Logs

Test logs are generated in the console as well as into the log file in a readable JSON format  `target/logs/zerocode_rest_bdd_logs.log` . In case of a test failure it exactly lists which field or fields didn't match with their  JSON Path in a tree view.

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
  "status" : "$EQ.200",
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

## Source Code in GitHub
Visit the source here in  GitHub [zerocode](https://github.com/authorjapps/zerocode).

## Contribute
Raise [issues and contribute](https://github.com/authorjapps/zerocode/issues) to imrpove zerocode library and add more essential features you need by writing to the author.

Welcome to the zerocode wiki!

Get rid of lot of boilerplate codes! Learn how the ZeroCode testing library will make your life easier.

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

, then you just stick these into a JSON file named e.g.  "get_happy_and_sad.json"  anywhere in the  test/resources  folder,

and run the code like below  pointing to that  JSON file  and then you are done with testing.
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

* You can add as many tests as you want by just annotating the test method. See here some examples

![https://dzone.com/storage/temp/7566618-screen-shot-2017-12-17-at-101840-pm.png](IDE setup)

## Why using an IDE ?
Performance testing could be simple, easy and flexible to match your project need if it is based from your IDE!
- Go to the [Download or Browse Demo Test Maven project](https://github.com/authorjapps/zerocode/wiki/Load-or-Performance-Testing%28using-your-IDE%29/_edit#download-or-browse-demo-project) section towards the trail of this page

There are many standalone tools available in the market which you need to install and configure in order to generate load. But you need to spent much time in installing and learning the product on Windows/Mac/Linux, to be able to fire tests in parallel.

JUnit framework already provides various mechanisms to run the tests in parallel e.g. [ParallelComputer](https://junit.org/junit4/javadoc/4.12/org/junit/experimental/ParallelComputer.html) class or fork-options-and-parallel execution in the [Sure-Fire](http://maven.apache.org/surefire/maven-surefire-plugin/examples/fork-options-and-parallel-execution.html). These mechanisms also helps you to fire all tests in the suite in parallel and at the same time, as you can set it up simply inside a maven plugin; you don't need the pain of installing standalone or fancy products to this job.

Furthermore when it comes to running a business scenario for your project need, you still need it be more flexible in terms of changing it, configuring it easily, picking and firing a particular test(s) at a particular time intervals, asserting the result, chaining one or more business test cases, running the tests for a certain configurable amount of time and retrieve an useful report and be able to share it with the stakeholders about the behaviour of the system under load/stress. 

This is where an extended custom JUnit runner specifically designed to do this job, can make your life easy.

The load test class which does the job of generating the load, looks like the following-
```java
@LoadWith("your_load_config.properties")
@TestMapping(testClass = AnyTestEndPoint.class, testMethod = "anyTestMethod")
@RunWith(ZeroCodeLoadRunner.class)
public class LoadTest {

}
```

## In essence the performance testing is all about : 
+ [How to run a test in parallel in the context of a scenarios or usecase ?](https://github.com/authorjapps/zerocode/wiki/Load-or-Performance-Testing%28using-your-IDE%29/_edit#how-to-run-tests-in-parallel-in-context-of-one-or-more-scenarios-)

+ [How to run the tests in a gap of configurable amount of time ?](https://github.com/authorjapps/zerocode/wiki/Load-or-Performance-Testing%28using-your-IDE%29/_edit#how-to-run-tests-in-a-gap-of-configurable-amount-of-time-)

+ [How to dynamically change the payload for every request during the load ?](https://github.com/authorjapps/zerocode/wiki/Load-or-Performance-Testing%28using-your-IDE%29/_edit#how-to-dynamically-change-the-payload-for-every-request-during-the-load-)

+ [How to assert the result once the response is received ?](https://github.com/authorjapps/zerocode/wiki/Load-or-Performance-Testing%28using-your-IDE%29/_edit#how-to-assert-the-result-once-the-response-is-received-)

+ [How to configure number of users to be launched in parallel ?](https://github.com/authorjapps/zerocode/wiki/Load-or-Performance-Testing%28using-your-IDE%29/_edit#how-to-configure-number-of-users-to-be-launched-in-parallel-)

+ [How to configure how long the tests to be run?](https://github.com/authorjapps/zerocode/wiki/Load-or-Performance-Testing%28using-your-IDE%29/_edit#how-to-configure-how-long-the-tests-to-be-run)

+ [How to generate useful report(s) or statistics to explain the behaviour of the system under test?](https://github.com/authorjapps/zerocode/wiki/Load-or-Performance-Testing%28using-your-IDE%29/_edit#how-to-generate-useful-reports-or-statistics-to-explain-the-behaviour-of-the-system-under-test)

+ [How to reuse your existing test to feed it to generate load?](https://github.com/authorjapps/zerocode/wiki/Load-or-Performance-Testing%28using-your-IDE%29/_edit#how-to-reuse-your-existing-test-to-feed-it-to-generate-load)

+ [And how to achieve/run the above by using your IDE e.g. Eclipse or IntelliJ etc?](https://github.com/authorjapps/zerocode/wiki/Load-or-Performance-Testing%28using-your-IDE%29/_edit#and-finally-how-do-you-run-the-load-test-using-your-ide-eg-eclipse-or-intellij-etc)

+ [Download or browse the demo project](https://github.com/authorjapps/zerocode/wiki/Load-or-Performance-Testing%28using-your-IDE%29/_edit#download-or-browse-demo-project)

Lets address one by one of the above aspects in details in the following section.

### How to run tests in parallel in context of one or more scenarios ?
Annotate your load test class with :
```java
@RunWith(ZeroCodeLoadRunner.class)
```
Here, the JUnit runner `org.jsmart.zerocode.core.runner.parallel.ZeroCodeLoadRunner` picks the JUnit test `anyTestMethod` from `AnyTestEndPoint` class and generates load configured in the properties file `your_load_config.properties` i.e. fires the test in parallel the number of times.

The test class looks like below:
```java
import org.junit.Test;

public class AnyTestEndPoint {

    @Test
    public void anyTestMethod() throws Exception {
       ...
    }
}
```

The properties needed are as follows-
***

```properties
# You can enter as many threads to stimulate a load test. A single user is represented by each Thread. So if you wish
# to simulate a load test with 5 concurrent users then you need to enter 5 as the value for this property. A high end
# machine will be able to spawn more number of threads. To keep the consistent(or nearly consistent) gap between the
# threads, adjust this number with 'ramp.up.period.in.seconds' and the actual response time of the API end point.
number.of.threads=2

# It indicates the time taken to create all of the threads needed to fork the requests. If you set 10 seconds as the
# ramp-up period for 5 threads then the framework will take  10 seconds to create those 5 threads, i.e. each thread
# will be at work appx 2 secs gap between the requests. Also by setting its value to 0 all the threads can be created
# at once at the same time. Note- If you want to fire more threads/user-requests in less ramp up time e.g. 5 threads
# in 2secs(or 5 threads in 1 sec), then, use '@UseHttpClient(SslTrustHttpClient.class)' as this closes the connection
# before making the next connection.
ramp.up.period.in.seconds=10

# By specifying its value framework gets to know that how many times the test(s), i.e. the number of requests will be
# repeated per every 'ramp.up.period.in.seconds'.
# Supposing number.of.threads = x, ramp.up.period.in.seconds = y, loop.count = i
# then (x * i) = number of requests will be fired over (y * i) seconds. If x=5, i=3, y=20, then 15 requests will be
# fired in 60 seconds which means- every request in 4 seconds gap. 60/15 or 20/5 = 4seconds.
loop.count=1

# If you have set the loop count to a higher digit which e.g. should take 3hrs(3*60*60=10800sec),
# but due to load or network delay it could take more time(you are speculating) e.g. 4hrs, then you can
# set this abort value to 3hrs i.e. 3*60*60=10800sec.
abort.after.time.lapsed.in.seconds=600

```

### How to run tests in a gap of configurable amount of time ?
The `your_load_config.properties` file defines the load you want to generate on the server. 
e.g.
- If `number.of.threads=2`, `ramp.up.period.in.seconds=10`, then the gap between the test invocation is 5secs.
- If `number.of.threads=2`, `ramp.up.period.in.seconds=4`, then the gap between the test invocation is 2secs.
- If `number.of.threads=10`, `ramp.up.period.in.seconds=10`, then the gap between the test invocation is 1sec.
- If `number.of.threads=10`, `ramp.up.period.in.seconds=5`, then the gap between the test invocation is 0.5sec.
- If `number.of.threads=10`, `ramp.up.period.in.seconds=2`, then the gap between the test invocation is 200milisec.

### How to dynamically change the payload for every request during the load ?
Suppose you have a payload in the `request` block below to invoke `POST` method using url `/api/v1/abc-bank/employees`. 

So the test case looks like:
```javaScript
        {
            "name": "create_emp",
            "url": "/api/v1/abc-bank/employees",
            "operation": "POST",
            "request": {
                "body": {
                    "id": "EMP-300000001",
                    "name": "Sindrella Holmes",
                    "address": "Piscataway, NJ Turn Pike, ZIP-300009"
                }
            }
        }
```
You are using this payload to load-test your POST end point i.e. load-testing the `createEmployee` feature.
This load needs to be dynamic in terms of `id, name, address` every time test is fired.

- Let's make the `id` different every time the test runs!
To achieve this, use:
> "id": "EMP-${RANDOM.NUMBER}"

or 

> "id": "EMP-${RANDOM.UUID}"

where the full test case will actually look like below which asserts the result status to `201` every time it runs:
```javaScript
        {
            "name": "create_emp",
            "url": "/api/v1/abc-bank/employees",
            "operation": "POST",
            "request": {
                "body": {
                    "id": "EMP-${RANDOM.NUMBER}",
                    "name": "Sindrella Holmes",
                    "address": "Piscataway, NJ Turn Pike, ZIP-300009"
                }
            },
            "assertions": {
                "status": 201
            }
        }
```

- To make the `name` different every time the test test runs,
Use:
> "name": "Sindrella ${RANDOM.STRING}"

- To make the `address` different every time the test test runs,
Use:
> "address": "Piscataway, ${RANDOM.STRING}, ZIP-${RANDOM.NUMBER}"

### How to assert the result once the response is received ?
e.g. if the response of your API produces the following-
```javaScript
{
    "status": 201,
    "body": {
        "id": "EMP-300000001"
    }
}                 
```
Then, you simply put your expectations into the `assertions` section as below-
```javaScript
{
    ...
    "assertions": {
        "status": 201,
        "body": {
            "id": "EMP-300000001"
        }
    }
}
```
and the entire test case looks like following-
```
        {
            "name": "create_emp",
            "url": "/api/v1/abc-bank/employees",
            "operation": "POST",
            "request": {
                "body": {
                    "id": "EMP-${RANDOM.NUMBER}",
                    "name": "Sindrella Holmes",
                    "address": "Piscataway, NJ Turn Pike, ZIP-300009"
                }
            },
            "assertions": {
                "status": 201,
                "body": {
                    "id": "EMP-300000001"
                }
            }
        }
```

### How to configure number of users to be launched in parallel ?
> The `number.of.threads=2` above creates number of users.

You can configure as many threads to simulate a load test. A single user is represented by each Thread. So if you wish to simulate a load test with 10 concurrent users then you need to enter 10 as the value for this property. A high end machine will be able to spawn more number of threads. To keep the consistent(or nearly consistent) gap between the threads, you need to adjust this number with `ramp.up.period.in.seconds` and the actual response time of the API end point, which you will get to know better in couple of dry runs.

### How to configure how long the tests to be run?
> ramp.up.period.in.seconds=10
> loop.count=1
in combination will decide how long the tests will run. This means- if you set `loop.count=5` and `ramp.up.period.in.seconds=60`, then the load test will run `60x5=300` seconds(5mins) firing in total `number.of.threads x 10` test requests.

### How to generate useful report(s) or statistics to explain the behaviour of the system under test?
The test reports are generated under `/target` folder with name `zerocode-junit-granular-report.csv` which attaches a `correlation-id` to each test it runs. If more number of steps are run for each scenario, attaches a `correlation-id` to each step making your life easier to track **which test/step failed** for what reason.

A sample load report looks like this in [CSV format](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/zz_reports/sample-load-junit-granular-report.csv), but when you draw charts/graphs you get a **fancy** looks along with a **throughput** statistics, a sample one looks like [this (download and view in MS Excel)](https://github.com/authorjapps/helpme/blob/master/zerocode-rest-help/src/test/resources/zz_reports/sample-load-junit-granular-report.xlsx)
![Load throughput report](https://github.com/authorjapps/zerocode/blob/master/img/load/load_sample_throughput.png)

### How to reuse your existing test to feed it to generate load?
If you have an existing test case e.g. a `POST` call or a scenario with `POST, PUT then GET`, then you can simply feed this test into the load runner as below-
> @TestMapping(testClass = YourExistingTest.class, testMethod = "testPost")

or

> @TestMapping(testClass = YourExistingTest.class, testMethod = "testPostPut_thenGet")

, existing test is-
```java
@HostProperties(host="https://api.yourserver.com", port=443, context = "")
@UseHttpClient(SslTrustHttpClient.class)
@RunWith(ZeroCodeUnitRunner.class)
public class YourExistingTest {

    @Test
    @JsonTestCase("all_tests/post_api_existing_test.json")
    public void testPost() throws Exception {

    }

    @Test
    @JsonTestCase("all_tests/post_put_get_api_existing_test.json")
    public void testPostPut_thenGet() throws Exception {

    }

}
```

and the load test will be as following:
```java
@LoadWith("your_load_config.properties")
@TestMapping(testClass = YourExistingTest.class, testMethod = "testPost") //or testMethod = "testPostPut_thenGet"
@RunWith(ZeroCodeLoadRunner.class)
public class LoadTest {

}
```

### And finally how do you run the load-test using your IDE e.g. Eclipse or IntelliJ etc?
- Simply right click on the `LoadTest` class and run as JUnit. (Eclipse)
- Click on the tiny play arrow besides the `LoadTest`, then press `Run` (IntelliJ)

Note-
<br/>
Before running the load test, please make sure you are able to run the unit test successfully which you intend to feed to the load runner(in this case @Test annotated `testPost` method of `YourExistingTest.class`).

Hope this wiki page helps you in doing your performance testing easy, accurate and fun! 

For any queries please write to `author.japps@gmail.com`

### Download or browse demo project
1. Browse 
- [the load generating test class](https://github.com/authorjapps/zerocode-hello-world/blob/master/src/test/java/org/jsmart/zerocode/testhelp/tests/loadtesting/LoadGetEndPointTest.java), 
- [the test-case containing the payload with assertions](https://github.com/authorjapps/zerocode-hello-world/blob/master/src/test/resources/loadtesting/github_get_api_test_case.json) and 
- [the JUnit test method pointing the JSON testcase](https://github.com/authorjapps/zerocode-hello-world/blob/master/src/test/java/org/jsmart/zerocode/testhelp/tests/loadtesting/restendpoint/TestGitGubEndPoint.java)

or

1. [Download the demo maven project](https://github.com/authorjapps/zerocode-hello-world/archive/master.zip) and run the `org.jsmart.zerocode.testhelp.tests.loadtesting.LoadGetEndPointTest` as simple JUnit, from your IDE or using `maven` command e.g.
> mvn test -Dtest=org.jsmart.zerocode.testhelp.tests.loadtesting.LoadGetEndPointTest

or

1. Browse [the demo test project source](https://github.com/authorjapps/zerocode-hello-world)

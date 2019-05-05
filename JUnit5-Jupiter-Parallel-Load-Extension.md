## Table of Contents

* [Parallel Running as well as Load and Stress Testing of JUnit5 tests](#parallel-running-as-well-as-load-and-stress-testing-of-junit5-tests)
 * [Existing JUnit5 tests](#existing-junit5-tests)
 * [Generating Load](#generating-load)
 * [What does JUnit5LoadTest example do?](#what-does-junit5loadtest-example-do)
 * [What does JUnit5LoadCommonLoadTest example do?](#what-does-junit5loadcommonloadtest-example-do)
 * [What does JUnit5LoadDifferentLoadTest example do?](#what-does-junit5loaddifferentloadtest-example-do)
 * [Load Test Reports](#reports)
 * [Running the Load tests as a Suite](#running-the-load-tests-as-a-suite)

## Parallel Running `as well as` Load and Stress Testing of JUnit5 tests

### Existing JUnit5 tests

> In the `HelloWorld` performance test repo, the below are the JUnit5 tests

![image](https://user-images.githubusercontent.com/12598420/57195971-0563bc80-6f50-11e9-9d68-ef86ed4c4a57.png)

### Generating Load

> Or we can alternatively say - Running the tests in parallel as configured

![image](https://user-images.githubusercontent.com/12598420/57195957-e06f4980-6f4f-11e9-975c-2f8e3bfb6967.png)

### What does JUnit5LoadTest example do?
+ This generates load as configured in the `@LoadWith("load_generation.properties")`

### What does JUnit5LoadCommonLoadTest example do?
+ If your load generation configuration is same for all kind of load you are setting up to generate, then
you can annotate the config at the `Class` level `@LoadWith("load_generation.properties")`

e.g.

```java
@LoadWith("load_generation.properties")
@ExtendWith({ParallelLoadExtension.class})
public class JUnit5LoadCommonLoadTest {
   //...
}
```

### What does JUnit5LoadDifferentLoadTest example do?
+ If your load generation configuration is different for different kind of load you are setting up to generate, then, you need to annotate the config at the `Method` level `@LoadWith("load_generation.properties")`

e.g.
```java
@ExtendWith({ParallelLoadExtension.class})
public class JUnit5LoadDifferentLoadTest {

    @Test
    @DisplayName("1sec gap per user - Firing parallel load for X and Y scenarios")
    @TestMappings({
            @TestMapping(testClass = JUnit5Test.class, testMethod = "testX"),
            @TestMapping(testClass = JUnit5Test.class, testMethod = "testY")
    })
    @LoadWith("load_generation.properties")
    public void testLoad_xy() {
        // This space remains empty
    }

```

### Reports
+ This generates CSV report only which is useful and efficient for tracing the failures
+ We have deliberately suppressed the HTML reports as they are not particularly useful for load tests
+ CSV gives us flexibility to `slice n dice` for analysis purpose.
+ Using CSV we can generate various throughput, 2D, 3D metrices of our performance testing


### Running the Load tests as a Suite
+ This setup(JUnit5LoadDifferentLoadTest, JUnit5LoadCommonLoadTest) is already like a Suite setup
  + which means you don't need another Suite-Runner 

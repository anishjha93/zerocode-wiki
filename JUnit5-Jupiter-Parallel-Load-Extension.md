## Parallel Running `as well as` Load and Stress Testing of JUnit5 tests

### Existing JUnit5 tests

> In the `HelloWorld` performance test repo, the below are the JUnit5 tests

![image](https://user-images.githubusercontent.com/12598420/57195971-0563bc80-6f50-11e9-9d68-ef86ed4c4a57.png)

### Generating Load

> Or we can call running the tests in parallel as configured

![image](https://user-images.githubusercontent.com/12598420/57195957-e06f4980-6f4f-11e9-975c-2f8e3bfb6967.png)

### What is JUnit5LoadTest ?
+ This generates load as configured in the `@LoadWith("load_generation.properties")`

### What is JUnit5LoadCommonLoadTest ?
+ If your load generation configuration is same for all kind of load you are setting up to generate, then
you can annotate the config at the class level `@LoadWith("load_generation.properties")`

e.g.

```java
@LoadWith("load_generation.properties")
@ExtendWith({ParallelLoadExtension.class})
public class JUnit5LoadCommonLoadTest {
   //...
}
```

### What is JUnit5LoadDifferentLoadTest ?
+ If your load generation configuration is different for different kind of load you are setting up to generate, then, you need to annotate the config at the method level `@LoadWith("load_generation.properties")`

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


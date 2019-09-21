Table of contents
===
   * [Steps](#steps)
   * [Try-at-home examples](#try-at-home-examples)

Steps
===
Add this maven dependencies in `test` scope which transitively brings in `JUnit` lib.
```xml
<dependency>
    <groupId>org.jsmart</groupId>
    <artifactId>zerocode-tdd</artifactId>
    <version>1.3.x</version> 
    <scope>test</scope>
</dependency>
```

Then annotate your `JUnit` test method pointing to the JSON/YAML scenario-file as below via `@Scenario` and `run` as a JUnit test. That's it really!

```java
@TargetEnv("github_host.properties")
@RunWith(ZeroCodeUnitRunner.class)
public class JustHelloWorldTest {

    @Test
    @Scenario("helloworld/hello_world_scenario_happy_path.json")
    public void testGet() throws Exception {

    }
}
```
Where, the `hello_world_scenario_happy_path.json` looks like below.

```javaScript
                                     hello_world_scenario_happy_path.json
                                     ------------------------------------
{
    "scenarioName": "Validate the GET api @@Richard",
    "steps": [
        {
            "name": "get_user_details",
            "url": "/users/octocat",
            "method": "GET",
            "request": {
                "headers" : { 
                   "Content-Type" : "application/json"
                }
            },
            "verify": {
                "status": 200,
                "headers" : { 
                   "Content-Type" : [ "application/json; charset=utf-8" ]
                },
                "body": {
                    "login" : "octocat"
                }
            }
        }
    ]
}
```

the `github_host.properties` looks as below:
```
web.application.endpoint.host=https://api.github.com
web.application.endpoint.port=443
web.application.endpoint.context=
```

***

YAML Test case:
```yaml
                                     hello_world_scenario_happy_path.yaml
                                     ------------------------------------

---
scenarioName: Validate the GET api @@Richard
steps:
- name: get_user_details
  url: "/users/octocat"
  method: GET
  request:
    headers:
      Content-Type: application/json
  verify:
    status: 200
    headers:
      Content-Type:
      - application/json; charset=utf-8
    body:
      login: octocat
```

Runner:
```java
@TargetEnv("github_host.properties")
@RunWith(ZeroCodeUnitRunner.class)
public class JustHelloWorldTest {

    @Test
    @Scenario("helloworld/hello_world_scenario_happy_path.yaml")
    public void testGet() throws Exception {

    }
}
```

Try-at-home examples
===

Clone or Download the [HelloWord](https://github.com/authorjapps/zerocode-hello-world) project, and follow the [Steps](https://github.com/authorjapps/zerocode-hello-world/blob/master/README.md)  to Run Hello World


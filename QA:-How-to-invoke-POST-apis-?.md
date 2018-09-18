Hello, It's as simple as above calls, nothing different, Just instead of method GET, use POST or PUT etc. e.g.

`- How to invoke POST calls ?`

e.g. below- (Also check in the [Hello World demo repo](https://github.com/authorjapps/zerocode-hello-world))
```javaScript
        {
            "scenarioName": "Invoke POST, and receive the 201 status with an ID",
            "steps": [
                {
                    "name": "create_emp",
                    "url": "/api/v1/google-uk/employees",
                    "operation": "POST",
                    "request": {
                        "body": {
                            "id": 1000,
                            "name": "Larry Pg",
                            "addresses": [
                                {
                                    "gpsLocation": "x9000-y9000z-9000-home"
                                }
                            ]
                        }
                    },
                    "assertions": {
                        "status": 201,
                        "body": {
                            "id": 1000
                        }
                    }
                }
            ]
        }
```
       
`- How to pass headers e.g. auth info etc in the `headers` into the RESTful APIs ?`
        
e.g. below- (Also check in the [TOC README file](https://github.com/authorjapps/zerocode#passing-headers-to-the-rest-api))

```javaScript
{
    "scenarioName": "Passing  headers to a rest api @@JohnSmart",
    "steps": [
        {
            "name": "create_new_employee",
            "url": "http://localhost:9999/google-emp-services/home/employees",
            "operation": "POST",
            "request": {
                "headers": {
                    "clientId": "client-sadfsdf-twertert-13123",
                    "clientSecret": "pwd-sadfasdf1234234-sdfsdf-4234",
                    "customParam1": "customParam1Value"
                },
                "body": {
                    "id": 1000,
                    "name": "Larry ${RANDOM.STRING:5}",
                    "password": "${RANDOM.STRING:10}"
                }
            },
            "assertions": {
                "status": 201
            }
        }
    ]
}
``` 

### Note-
The host and port can be externalized into a properties file too for the regression suites-
e.g.

```java
@TargetEnv("hello_world_host.properties")
@RunWith(ZeroCodeUnitRunner.class)
public class JustHelloWorldMoreTest {

    @Test
    @JsonTestCase("helloworld_more/hello_world_post_201.json")
    public void testHelloWorld_post() throws Exception {
    }

}
```

where "hello_world_host.properties" is like below-
```properties
# Web Server host and port
restful.application.endpoint.host=http://localhost
restful.application.endpoint.port=9999
# Web Service context; Leave it blank in case you do not have a common context
restful.application.endpoint.context=
```

`- Does it support https connections?`

The current apache http client used in the framework supports both `http` and `https` ssl/tls connections. But you can customize this if(your project needs) you need to add anything extra e.g. more authentication mechanism like tokens in the headers for your entire regression suite in a single/central place. Note- You can add token to the headers without customizing it(http client) too, that means you need to add to every test case. This depends on the use case and how we go about it.

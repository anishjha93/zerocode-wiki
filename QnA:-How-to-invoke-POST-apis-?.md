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
       

`- Does it support https connections?`

The current apache http client used in the framework supports both `http` and `https` ssl/tls connections. But you can customize this if(your project needs) you need to add anything extra e.g. more authentication mechanism like tokens in the headers for your entire regression suite in a single/central place. Note- You can add token to the headers without customizing it(http client) too, that means you need to add to every test case. This depends on the use case and how we go about it.

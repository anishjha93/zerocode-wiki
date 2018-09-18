GitHub Link : https://github.com/authorjapps/zerocode

#### Why is it useful?
- It's Open-Source and very easy to write an API tests using JSON
- E.g. if you have an `url`, `method`, and you know the expected result, simply you can assert keeping JSON structure as it is. 
e.g.
```
{
    "scenarioName": "Invoke the GitHub REST api and assert the result",
    "steps": [
        {
            "name": "get_user_details",
            "url": "/users/octocat",
            "operation": "GET",
            "request": {
            },
            "assertions": {
                "status": 200,
                "body": {
                    "login" : "octocat",
                    "type" : "User"
                }
            }
        }
    ]
}
```

#### What problem it solves?
- You can chain multiple steps to create a `scenario` or an `user journey`
- Http/Https calling is handled by the framework
- Test Reports are fuzzy search and filter enabled

See examples in the [README](https://github.com/authorjapps/zerocode)


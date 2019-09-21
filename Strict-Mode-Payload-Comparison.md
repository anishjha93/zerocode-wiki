## Table Of Contents
* [Introduction](#introduction)
* [Strict comparison DSL flag](#strict-comparison-dsl-flag)
* [Using STRICT mode for Payload verification](#using-strict-mode-for-payload-verification)
* [Conclusion](#conclusion)

## Introduction
Strict mode Payload comparison makes strict comparison of the expected payload with the actual response payload. 

The default mode of comparison is `LENIENT` i.e. the actual response can have more properties than the expected payload and the test will still pass. 

In `STRICT` mode, **the response is not allowed to have extra properties** as compared to the expected payload. It should always find EXACT match else the test will fail. 


## Strict comparison DSL flag
To use `STRICT` comparison you just need to add the flag `verifyMode` to the test case

For example, if we have an `GET` API `/api/v1/search/persons` which returns the Http status as `200` and the below response payload,
```json
{
    "scenarioName": "As simple GET API - Strict validation",
    "steps": [
        {
            "verifyMode":"STRICT",
            "verify": {
                 ...
            }
        }
    ]
}
```
then we can write the automation Test-case as below.

```yaml
---
scenarioName: Validate a GET API
steps:
-     
  ...
  verifyMode: STRICT
  verify:
      ...
``` 

## Using STRICT mode for Payload verification
The test will pass only if the actual response exactly contains the expected fields, if there are extra properties in the actual response, then you will receive the following message:
```java
Assertion jsonPath [extra property name]' with actual value 'Unexpected: [extra property name]' did not match the expected value
```

## Conclusion
`STRICT` mode can be very useful in testing use cases where the application wants to restrict the response only to the expected fields both qualitatively as well as quantitatively.
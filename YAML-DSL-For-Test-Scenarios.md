## Introduction
Sometimes testers or developers need to describe their automation scenarios in YAML format. Zerocode provides the mechanism to achieve this using YAML.

## A Test Scenario in YAML DSL format
For example, if we have an `GET` API `/api/v1/search/persons` which returns the Http status as `200` and the below response payload,
```json
{
	"exactMatches": true,
	"name": "Mr Bean",
	"city": "Lon"
}
```
then we can write the automation Test-case as below.

```yaml
---
scenarioName: As simple GET request response
steps:
- name: "find_match"
  url: "/api/v1/search/persons"
  operation: "GET"
  request:
    queryParams:
      lang: "Amazing"
      city: "Lon"
  verifications:
    status: 200
    body:
      exactMatches: true
      name: "Mr Bean"
      city: "Lon"
``` 

Where
+ `scenarioName`: Unique Free text string describing precisely what is being tested
+ `name`: Unique name of this step wrt this scenario
+ `url` : Relative URL path or FQDN of the API end points
+ `operation` : An http operation e.g. GET, POST, PUT, DELETE, HEAD etc
+ `request` : The request `payload` with http `headers` and/or `query parameters`
+ `verifications` : The expected http status and response payload
+ `status`: An http status code e.g. 200 is OK, 201 is CREATED etc.

## Using JayWay JSON Path Between The Steps
The JSON Path can be used to pick an element/field and reuse it in subsequent steps

## Using Array in YAML

## Conclusion
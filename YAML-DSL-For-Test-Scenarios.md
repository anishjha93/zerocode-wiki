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
In the below test scenario, please have a look at the 2nd step's `verifications` block where various JSON Paths are used to pick/reuse the desired fields rather than hard-coding.
```yaml
---
scenarioName: As simple GET request response Multi STep
steps:
- name: find_match
  url: "/api/v1/search/persons"
  operation: GET
  request:
    queryParams:
      lang: Amazing
      city: Lon
  assertions:
    status: 200
    body:
      exactMatches: true
      name: Mr Bean
      lang: Amazing
      city: Lon

- name: find_match2
  url: "/api/v1/search/persons"
  operation: GET
  request:
    queryParams:
      lang: Amazing
      city: Lon
  verifications:
    status: "$EQ.${$.find_match.response.status}"
    body:
      exactMatches: true
      name: "$CONTAINS.STRING:Bean"
      lang: "${$.find_match.response.body.lang}"
      city: "${$.find_match2.request.queryParams.city}"
```

## Using Array in YAML
e.g. the API responds with a `person` payload with array of `addresses`.

```yaml
---
scenarioName: "A simple GET API Scenario" #comments allowed
steps:
- name: "find_match"
  url: "/api/v1/persons/p001"
  operation: "GET"
  request:
    headers:
      x-api-key: "Ama-zing-key"
      x-api-secret: "Sec-ret-stuff"
  verifications:
    status: 200 #comment - a http status code as int value
    body:
      exactMatches: true
      name: "Mr Bean"
      addresses:
      - type: "office"
        line1: "10 Random St"
      - type: "home"
        line1: "300 Random St"
```

Here `addresses` is a collection of individual address. The equivalent JSON is as follows.
```json
{
        ...
	"exactMatches": true,
	"name": "Mr Bean",
	"addresses": [{
			"type": "office",
			"line1": "10 Random St"
		},
		{
			"type": "home",
			"line1": "300 Random St"
		}
	]
}
```

## Conclusion
In an YAML file if the line starts with a `-` mark, then the containing element is an `array`.
### Send and test `"Content-Type": "application/x-www-form-urlencoded"` with KeyValue params

[Zerocode](https://github.com/authorjapps/zerocode) makes it easy to send this content-type in the header and assert the response.

When you use this header, then you just need to put the `Key-Value` or `Name-Value` content under request `body` or request `queryParams` section. That's it.

e.g.
```javaScript
         "request": {
            "headers": {
               "Content-Type": "application/x-www-form-urlencoded"
            },
            "body": {
               "unit-no": "12-07",
               "block-number": 33,
               "state/region": "Singapore North",
               "country": "Singapore",
               "pin": "87654321",
            }
         }
```

### What happens if my Key contains a `space` or front slash `/` etc?
This is automatically taken care by Apache Http Client. That means it gets converted to the equivalent encoded char which is understood by the server(e.g. Spring boot or Jersey or Tomcat etc ).
e.g. 
The above name-value pair behind the scene is sent as below:
> unit-no=12-07&country=Singapore&block-number=33&pin=87654321&state%2Fregion=Singapore+North

### How does the server receives this?
The server received them as MultiValue map. E.g. If your server implementation is as below, the paramMap gets populated with Key-Value pairs.
```java
    @PostMapping(value = "/api/v1/issues/customer", consumes = {"application/x-www-form-urlencoded"})
    public ResponseEntity handleRequestCustomer( @RequestParam MultiValueMap paramMap ) {
```

### How does a full test case look like?
You can frame many variations of a test situation depending on your use-case. The simplest one could be like below:
```javaScript
{
   "scenarioName": "Post Name Value pairs with x-www-form-urlencoded header @@arunvelusamyd",
   "steps": [
      {
         "name": "post_www_form_header",
         "url": "/api/v1/issues/customer",
         "operation": "POST",
         "request": {
            "headers": {
               "Content-Type": "application/x-www-form-urlencoded"
            },
            "queryParams": {
               "unit-no": "12-07",
               "block-number": "33",
               "state/region": "singapore north",
               "country": "singapore",
               "pincode": "87654321"
            }
         },
         "assertions": {
            "status": 201
         }
      },
      {
         "name": "check_json_header",
         "url": "/api/v1/issues/customer",
         "operation": "POST",
         "request": {
            "headers": {
               "Content-Type": "application/json"
            }
         },
         "assertions": {
            "status": 415,
            "body": {
               "error": "Unsupported Media Type",
               "message": "Content type 'application/json' not supported"
            }
         }
      }
   ]
}
```
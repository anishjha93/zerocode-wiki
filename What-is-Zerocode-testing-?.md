
[Zerocode](https://github.com/authorjapps/zerocode) is an open source lib/framework enables API testing via simple declarative JSON steps - REST, SOAP, KAFKA and DB services

Zerocode brings the simplicity in testing and validating APIs by eliminating repetitive code for test assertions, http calls and payload parsing. See an example [how](https://github.com/authorjapps/zerocode/wiki/User-journey:-Create,-Update-and-GET-Employee-Details). It's powerful JSON comparison and assertions make the testing cycle a lot easy and clean.

It also helps in mocking/stubbing interfacing APIs during the testing cycle. Its approach to IDE based performance testing to generate load/stress on the target application is quite simple, flexible and efficient - It goes a step further enabling you to simply reuse the test(s) from your regression pack.

[![License](https://img.shields.io/hexpm/l/plug.svg)](https://github.com/authorjapps/zerocode/blob/master/LICENSE) 
[![Code Coverage](https://img.shields.io/badge/coverage-80%25-brightgreen.svg)](https://github.com/authorjapps/zerocode/blob/master/img/code_coverage/code_coverage_granular.png)
[![zerocode REST API Automation](https://img.shields.io/badge/REST%20API-automation-green.svg)](https://github.com/authorjapps/zerocode-hello-world) 
[![zerocode SOAP Testing Automation API Automation](https://img.shields.io/badge/SOAP%20testing-automation-blue.svg)](https://github.com/authorjapps/zerocode/issues/28) 
[![Gitter](https://img.shields.io/gitter/room/nwjs/nw.js.svg)](https://gitter.im/zerocode-testing/help-and-usage)
[![Performance Testing](https://img.shields.io/badge/performance-testing-ff69b4.svg)](https://github.com/authorjapps/zerocode/wiki/Load-or-Performance-Testing-(IDE-based))

>Testing was _never_ so easy before.

e.g. Your below User-Journey or ACs(Acceptance Criterias) or a scenario,
```java
AC1:
GIVEN- the POST api end point '/api/v1/users' to create an user,     
WHEN- I invoke the API,     
THEN- I will receive the 201 status with the a user ID and headers 
AND- I will validate the response

AC2:
GIVEN- the REST api GET end point '/api/v1/users/${created-User-Id}',     
WHEN- I invoke the API,     
THEN- I will receive the 200(Ok) status with body(user details) and headers
AND- I will assert the response
```
translates to the below executable JSON in `Zerocode` - Simple and clean ! <br/>
_(See here [a full blown CRUD operation scenario](https://github.com/authorjapps/zerocode/wiki/User-journey:-Create,-Update-and-GET-Employee-Details) with POST, PUT, GET, DELETE example.)_ <br/>

<img width="624" alt="post_get_user" src="https://user-images.githubusercontent.com/12598420/47145467-bc089400-d2c1-11e8-8707-8e2d2e8c3127.png">

Keep in mind: It's simple JSON. <br/>
~~_No feature files, no extra plugins, no assertThat(...), no statements or grammar syntax overhead._~~ 

And it is **declarative** JSON DSL, with the `request/response` fields available for the next steps via the `JSON Path`.

See the [Table Of Contents](https://github.com/authorjapps/zerocode#table-of-contents--) for usages and examples.
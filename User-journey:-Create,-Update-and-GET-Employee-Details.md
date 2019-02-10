<br/>

> _Visit here for a quick introduction to [What is Declarative Testing And Zerocode](https://github.com/authorjapps/zerocode/wiki/What-is-Zerocode-testing)_

::: _**Note**_ :::

In _Declarative Testing_, the framework here does the job for us behind the scene, i.e. 
+ Making Http calls to the target end-point, with our request payload
+ Receiving the server reseponse into the test case
+ Doing the JSON comparison of the **actual** vs **expected** response for our "_assertions_". 
  + _Here we can choose to skip the fields  we do not need to assert_
  + _We keep the payload as JSON with its structure intact_

> _It saves us from the hassles of writing any code to do the above repititive tasks._

<br/>

Let's see in an user journey, how it is applied.

<br/>

** **USER JOURNEY - Acceptance Criteria(AC)** **

+ AC1
```
GIVEN- The Create API POST:"/api/v1/persons"
WHEN I invoke the POST operation with a "person" payload
THEN I will create a new employee 
AND assert the 201(created) status 
and newly created employee ID.
```
+ AC2
```
GIVEN- The Update API PUT:"/api/v1/persons/{personId}"
WHEN I invoke the PUT operation by the Id 
with some "person" details
THEN I will update the existing employee 
AND assert the 200(OK) status and updated fields.
```
+ AC3
```
GIVEN- The Get API GET:"/api/v1/persons/{personId}"
WHEN I invoke the GET operation
THEN I will fetch the employee details 
AND assert the status 200(OK) along with 
updated as well as non-updated fields 
```

To write a test-case for the above CRUD operation scenario is quite easy using [Zerocode](https://github.com/authorjapps/zerocode/blob/master/README.md#hello-world), just your IDE's **JSON editor is enough** to hook these steps. Example of `POST` and `GET` step would look like below(simple and clean)

<img width="624" alt="post_get_user" src="https://user-images.githubusercontent.com/12598420/47145467-bc089400-d2c1-11e8-8707-8e2d2e8c3127.png">

And at the same time you **don't have to search** for or think hard of any **syntaxes** to do the job. That means, you are ready with a BDD scenario test in couple of minutes with simple JSON steps(see below). Advantage here is the tests are instantly readable to anyone because it simple JSON payloads as it is.

<img width="566" alt="expanded-simple" src="https://user-images.githubusercontent.com/12598420/45925725-fe34f480-bf12-11e8-941c-cb3ec8da6c3e.png"> <br />

That's it, done. We are ready to run.

***
Then we stick the above json file to a JUnit runner and run. We can point to any `host` and `port` in the `Runner`. See the sample below.
```java
@TargetEnv("application_host.properties")
@RunWith(ZeroCodeUnitRunner.class)
public class JustHelloWorldTest {

    @Test
    @JsonTestCase("helloworld/user_crud_journey_test.json")
    public void testGet() throws Exception {
       // See, No code was needed here. What?
    }
}
```

the `application_host.properties` looks as below:
```
web.application.endpoint.host=https://hbc.banking.co.local.uk
web.application.endpoint.port=443
web.application.endpoint.context=
```
***

Let's put into the context n deep dive a bit.

We needed 3 steps here for the Happy case in the above journey-
+ POST - To create the new employee (e.g. created employee ID will be `1001`)
+ PUT - To update the same employee
+ GET - To verify that UPDATE has gone fine

This is how somewhat we imagined to perform the steps-
![collapse-1v2](https://user-images.githubusercontent.com/12598420/45925386-fde52b00-bf0b-11e8-8162-ff478c9c037e.png)
Note- _You can use any JSON editor to do the job for you -as simple as that_

Next we get our API end points details from the spec or api-doc(e.g. swagger) and fit into the steps(it should look like below)
<img width="772"  height="525" alt="Collapsed steps - bit extended" src="https://user-images.githubusercontent.com/12598420/46082518-2df42e80-c197-11e8-8007-adc9ce452123.png">

Next let's **Copy-Paste the payload and assertions** section which we might get it from the `spec` or api-doc(swagger). See below the **full-blown** steps(That's it - _we are ready to run._) How simple was that !
<img width="555"  height="726" alt="Full Blown steps" src="https://user-images.githubusercontent.com/12598420/45925567-ef007780-bf0f-11e8-8daf-12e7c8a12b82.png">


To complete the `D` part the CRUD operation(if your application has implemented this operation), you can simply add one more step or 2 more steps as below to verify it works perfectly ok.

<img width="504"  height="272" alt="Delete steps" src="https://user-images.githubusercontent.com/12598420/45928093-f2a6f500-bf35-11e8-8d4c-202849917c06.png">



> 
Done. Happy days !

***


_If you have little more time to read below, see what all hassles you escaped and how much time you saved !_

+ No need to write pojos and builder for the domain objects(e.g. Employee here)
+ No need of any serialization/deserialization
+ No need of http client calls and read the response
+ No need to `assertThat(expected, is(actual))` etc multiple times
+ No need of any feature files and syntax searchings
+ No need of English statements and grammars

See below what we did not have to do(luckily?) :
===
JOURNEY1 :

+ Step 1

~~Employee emp =~~
    ~~EmployeeBuilder.aNewInstance();~~
    ~~.name("Larry P")~~
    ~~.job("Full Time")~~
    ~~.build()~~

> Make the POST call

~~ObjectMapper objectMapper = ObjectMapperProvider.getInjectedObjectMapper();~~

~~HttpResponse<Object> postResponse =~~

~~aHttpClient.post("http://host:port/api/v1/persons")~~

  ~~.header("accept", "application/json")~~

  ~~.body(objectMapper.writeValueAsString(emp))~~

  ~~.execute();~~

> Assert the response

~~assertThat(postResponse.getStatusCode(), is(201))~~

~~assertThat(postResponse.getEntity().getId(), is(1001))~~


+ Step 2

> Create an employee with updated payload

~~Employee empForUpdate = EmployeeBuilder.aNewInstance()~~
    ~~.name("Larry Page")~~
    ~~.job("Co-Founder")~~
    ~~.build();~~

> Make a PUT call

~~HttpResponse<Employee> putResponse =~~

~~aHttpClient.put("http://host:port/api/v1/persons/" + postResponse.getEntity().getId())~~

  ~~.header("accept", "application/json")~~

  ~~.body(objectMapper.writeValueAsString(empForUpdate))~~

  ~~.execute();~~

~~Employee empUpdated = response.getUser();~~

> Assert the response

~~assertThat(putResponse.getStatusCode(), is(200))~~

~~assertThat(empUpdated.getName(), is(empForUpdate.getName()))~~

~~assertThat(empUpdated.getJob(), is(empForUpdate.getJob()))~~


+ Step 3

> Make the GET call

~~HttpResponse<Employee> response =~~

~~aHttpClient.get("http://host:port/api/v1/persons/" + postResponse.getEntity().getId())~~

  ~~.header("accept", "application/json")~~

  ~~.execute();~~

~~Employee empFetched = response.getEmployee();~~

> Assert the response

~~assertThat(response.getStatusCode(), is(200))~~

~~assertThat(empFetched.getName(), is(empForUpdate.getName()))~~

~~assertThat(empFetched.getJob(), is(empForUpdate.getJob()))~~


<br/>
<br/>

Also, you escaped the **hard** way of doing things with special attention to English statements and grammars. See below:

***

This approach might take different `shapes and forms` for developers/testers with spending too much time agreeing on the semantics than spending time in writing actual executable tests.

**e.g.** <br/>
~~GIVEN- the REST api POST end point,~~ <br/>
~~WHEN- I invoke the API with a payload,~~ <br/>
~~THEN- I will receive 201(Created) status with a newly created ID and assert the response~~ <br/>

or

~~GIVEN- the REST url and the method POST,~~ <br/>
~~WHEN- I invoke the API with a body,~~ <br/>
~~THEN- I will receive 201(Created) status with newly created ID~~ <br/>
~~AND assert the response~~ <br/>

or

~~GIVEN- the REST url /api/v1/persons/ ~~ <br/>
~~AND the http method POST ~~ <br/>
~~WHEN- I invoke the API using a HTTP client and send the body,~~ <br/>
~~THEN- I will receive 200(OK) status with body~~ <br/>
~~AND assert the response~~ <br/>

> and so on...

**Note**- Too much is going on the above around an `user journey`, in terms of writing correct sentences or **nearly** correct sentences/grammars, too many `assertThat`s to come up with a test scenario. 
> And imagine the situation you will be when you have more number of steps in an user journey !

<br/>

:::Note:::

It makes sense when the **BAs**(Business Analysts) or **managers** or non-technology folks while creating the stories and defining the entry and exit criteria of the tickets for a business scenario or User-Journey. But technology folks simply picking these statements and trying hard syntactically to fit these into executable tests seems like bit too much of an overhead. 
<br/>
<br/>
But we should choose the `tools`, `technologies` and `solutions` which best fits to your project and situation and helps us solving the testing challenges.

See this in action(HelloWorld):
===
The simplified HelloWorld projects are in GitHub repo to clone and run locally

- Simple HelloWorld repo : https://github.com/authorjapps/zerocode-hello-world

- (More examples and usages : https://github.com/authorjapps/zerocode/blob/master/README.md#hello-world )


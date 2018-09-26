USER JOURNEY1
+ AC1
```
GIVEN- The Create-API details
WHEN I invoke the POST operation with a employee payload
THEN I will create a new employee 
AND assert the 201(created) status and newly created employee ID.
```
+ AC2
```
GIVEN- The Update-API 
WHEN I invoke the PUT operation to update the employee by the ID 
THEN I will update the existing employee 
AND assert the 200(OK) status and updated fields.
```
+ AC3
```
GIVEN- The Get-API
WHEN I invoke the GET operation
THEN I will fetch the employee details 
AND assert the status 200(OK) along with updated as well as non-updated fields 
```

To write a test-case for the above CRUD operation scenario is quite easy, just your IDE's **JSON editor is enough**. And at the same time you **don't have to search** for or think hard of any **syntaxes** to do the job. That means, you are ready with a BDD scenario test in couple of minutes with simple JSON steps(see below).

<img width="566" alt="expanded-simple" src="https://user-images.githubusercontent.com/12598420/45925725-fe34f480-bf12-11e8-941c-cb3ec8da6c3e.png"> <br />

That's it, done.

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
+ No need to `aseretThat(expected, is(actual))` etc multiple times
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

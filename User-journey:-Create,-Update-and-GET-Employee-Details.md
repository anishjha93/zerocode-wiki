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

To write a test-case for the above CRUD operation scenario is quite easy, and at the same time you don't have to search for or think hard of any syntaxes to make it. That means, you are ready with a BDD scenario test in couple of minutes with simple JSON steps(see below).

Just your IDE's JSON editor is enough. Let's put into the context.

You need 3 steps here for the Happy case-
+ POST - To create the new employee (e.g. created employee ID will be `1001`)
+ PUT - To update the same employee
+ GET - To verify that UPDATE has gone fine

This is how somewhat you imagined to perform the steps-
![collapse-1v2](https://user-images.githubusercontent.com/12598420/45925386-fde52b00-bf0b-11e8-8162-ff478c9c037e.png)

Note- _You can use any JSON editor to do the job for you -as simple as that_

Next you get your API end points from the spec or api-doc(e.g. swagger) and fit into the steps(it should look like below)
![collapse-2](https://user-images.githubusercontent.com/12598420/45925470-bcee1600-bf0d-11e8-81ec-86a05d907ad5.png)

Next you **Copy-Paste your payload and assertions** section which you might get from the `spec` or api-doc(swagger). See below the **full-blown** steps(That's it - _you are ready to run._) How simple was that !
![expanded v1](https://user-images.githubusercontent.com/12598420/45925567-ef007780-bf0f-11e8-8daf-12e7c8a12b82.png)

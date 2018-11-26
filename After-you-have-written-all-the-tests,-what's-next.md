#### After you have finished writing all your tests, what all things to take care next?
These are general things to take care, nothing specific to `Zerocode`, but `Zerocode` makes your life very easy to achieve all these things.

Organization
===

+ Please check the organization of the tests.
  + Check you have organized the test cases by the API features?
  + Check you have organized the test cases by API methods?
  + Check the sub-organization by `Positive` or `Negative` flows
     + Sometimes they are called `Happy` and `Sad` flows
     + Sometimes they are called `Sunny` and `Rainy` cenarios
  + If they are `Consumer` or `Boundary` contract tests
     + Check you have organized them by the `consumer` names or `boundary` names.
     + Bring up a single Suite runner pointing to the root of the tests(JSON test files). [See here how](https://github.com/authorjapps/zerocode/wiki/Suite-Runner-Vs-Package-runner)

Test Suite
===
+ Create a `package` of tests aka `suite` of tests
  + Sometime this may not need any additional work too
  + i.e. just identify the root of the tests for which you want to create a suite runner, that's it.
+ Create a Suite runner or a Package runner.
  + It's good to bring up a Package runner or Suite runner for all your tests or subset of your tests. [See here how](https://github.com/authorjapps/zerocode/wiki/Suite-Runner-Vs-Package-runner)

CI Build
===

+ Create a Jenkin Build Pipe line for your project.
  + This depends on how you have organized your tests
  + If you have multi-module maven project(POM or Gradle based), then you might need a pipe line
  + If you have only one `maven module` or only one type of `suite` or one regression `pack`, then you just need one Jenkin Job, not a Jenkins Pipe Line

Running from IDE
===
@TargetEnv("app_host.properties")  <--- Point this to any `properties file` to run the tests against that env

e.g.
app_host.properties  <-- against localhost/or dev or default type env.
app_host_ci.properties  <--- against ci
app_host_dit.properties <--- against dit
app_host_sit.properties <--- against sst

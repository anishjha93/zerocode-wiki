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
     + Have you organized them by the aconsumera names or `boundary` names?

Test Suite
===
+ Create a `package` of tests aka `suite` of tests
  + Sometime this may not need any additional work too
  + i.e. just identify the root of the tests for which you want to create a suite runner, that's it.
+ Create a Suite runner or a Package runner.
  + It's good to bring up a Package runner or Suite runner for all your tests or subset of your tests.

 


CI Build
===

+ Create a Jenkin Build Pipe line for your project.
  + This depends on how you have organized your tests
  + If you have multi-module maven project(POM or Gradle based)

Running from IDE
===


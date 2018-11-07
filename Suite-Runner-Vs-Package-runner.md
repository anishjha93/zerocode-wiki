When to use JUnit Suite runner Vs Zerocode Package runner
===
+ Principally both do the same thing
  + i.e. Run all the tests from the single runner
+ When to use JUnit Suite runner ?
  + Use it - when you want to control which `Test` class to run and which not to run
  + The one you don't want to be part of the `Test Suite`, then just don't add them to the annotation
  + Env switching goes into the individual classes

+ When to use Zerocode Package runner(which is a JUnit custom runner) ?
  + Points to the JSON test cases root of the package
  + It picks all tests from the folder and sub folders and runs them
  + You can add env switching at single place(i.e. just annotate this class with env details)

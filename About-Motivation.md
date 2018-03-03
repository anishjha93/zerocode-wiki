Motivation
===
Motivation for inception of `Zerocode` has roots in one of the country's `Digital Transformation Project` which posed tough challenges to testing approach due to 

* Large number of micro services being used to achieve various `workflows`
* Large number of `data pipe lines` to ingest various legacy system's data into project’s `Big Data` store.
* `Micro Services` to be tested in `isolation` and `integrated`

Over several brain storming sessions, automation testers and developers came to a common conclusion to write tests

* That will allow anyone to change and maintain the tests easily
* Avoid writing boiler plate sticky code.
* Large numbers of tests can be well organized.
* Configurable for multiple environments (SIT, UAT, PRE-PROD, PROD etc)

Outcome of the sessions was to consider a `steps based` scenario build-up approach where the underlying test and test data is picked from a referenced `JSON file`. 

JSON is well recognized widely supported by `all IDEs` and hence could prove to be a good approach.

In fact many folks were already practicing this kind of approach in the similar manner in their respective Govt, Media, Banking and Retail projects, but was never standardized so that the approach could be reused to benefit more and more testers and developers across the industry.

After implementation of agreed approach we found that we were successfully able to achieve the following :- 

Repetitive tasks became part of the framework
* Tests were simple, `human readable JSON` files
* Tests were completely `independent` and `decoupled` from code.
* `Jenkins Pipeline` integration was seamless
* `Test reports` were apt and to the point
* Test output was also simple, `human readable JSON` structure.
* Failure assertions were `to the point` precisely describing the scenario step.
* Enabled `overriding framework behavior` for performing `project/test specific` tasks

It helped the program in a big way, and in the recent years it has added many more features into it.

We sincerely hope it helps you too.

Happy testing !
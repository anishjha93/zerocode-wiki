Motivation
===
One of the motivations behind the Zerocode was the Govt's Digital Transformation Project where a lot number of micro services were used to achieve specific workflows. Along with this, there were number of data pipe lines to ingest various legacy system's data into Hadoop with help of Kafka/Samza streaming with support of smartly written in-house NoSql framework to interact with HBase/HDFS. 

In a spike to demonstrate best testing approach, the automation testers and developers did come to a common understanding to write tests in such a way that will allow anyone to change and maintain tests easily; certainly avoiding boiler plate grammar code and unnecessary wrappers which perticularly fail to fit into different IDEs and readability of the tests are lost while changing context between test steps. 

As many folks were using IDEs like IntelliJ and Eclipse, these wrappers needed external plugins which became unpleasant hurdles to set it up in the first place as they never work as one expects, then, when the test cases grow to massive numbers, these issues along with, each tests are hidden behind wrappers, become hard to change, making delivery slow and inefficient. Also dealing with different environments like `local Laptop, CI1/CI1/DIT1/DIT2, SIT1/SIT2/SIT-SMall/SIT-Large, UAT1/UAT2, Pre-Prod1/Pre-Prod2, Preprod-Performance` was cumbersome.

Then the Automation Testers and Developers came up with the idea of `step based scenario build up` approach using JSON structure due to simplicity of JSON which is already fundamental IDEs, mainly IntelliJ and Eclipse. This helped the test team to go faster as well as to design better and more test cases efficiently.

This enabled testing of data ingestion into Hadoop and testing of `integrated Micro Services` and `Micro Services in isolation` an easy and quick thing. Migration between environments was seamless. IDE support was already inherent to IDEs as the tests were simple JSONs.

How did it help us? <br>
What problem did it solve?  <br>
What was achieved?
- Repetitive tasks became part of the framework
- Tests were simple JSON files
- Tests were independent
- Tests were readable
- Jenkins Pipeline integration was seamless
- Test reports were apt and to the point
- Test output was human readable as input/output was also JSONs
- Failure assertions were to the point precisely describing the scenario step.
- Enables overriding framework behaviour for performing project/test specific tasks

We sincerely hope it helps you too. <br>
Happy testing !

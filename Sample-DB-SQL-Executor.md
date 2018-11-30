Sample DB SQL Executor
===
This is particularly useful where as part of your testing you are not satisfied only with the REST responses and you want to verify the DB changes has gone well or not. It's very easy to and sometimes it's a good practice to test this DB verification bit too.

How the tests will look
===
The below are sample only, but you can extend this or devise your own execution method which makes your life easy.
Let's see below how we can achieve this:
+ Sample Test steps
+ Config properties (useful for your env switching)
+ Executor code (You can even more customize this for your project specific)
+ Test Logs(collected from console logs or target logs)

#### Sample Test steps:
```
{
    "scenarioName": "Postgres DB SQL Executor - Simple and generic one, you can extend to ",
    "steps": [
        {
            "name": "fetch_all",
            "url": "com.xp.springboot.dbutils.PostGresSqlExecutor",
            "operation": "executeSimpleSql",
            "request": "select * from employees;",
            "assertions": {
                "rows.SIZE": 2,
                "rows": [
                    {
                        "id": 1,
                        "name": "Jack"
                    },
                    {
                        "name": "Pulsar",
                        "id": 2
                    }
                ]
            }
        },
        {
            "name": "fetch_with_where",
            "url": "com.xp.springboot.dbutils.PostGresSqlExecutor",
            "operation": "executeSimpleSql",
            "request": "select id, name from employees where name='${$.fetch_all.response.rows[1].name}';",
            "assertions": {
                "rows.SIZE": 1,
                "rows": [
                    {
                        "id": 2,
                        "name": "${$.fetch_all.response.rows[1].name}"
                    }
                ]
            }
        }
    ]
}
```

#### Config properties
This is where you DB host, user, password details goes along with REST/SOAP/Kafka application host.
```
# Web Server host and port
web.application.endpoint.host=http://localhost
web.application.endpoint.port=8080
web.application.endpoint.context=

## ---------------------------
##  DB Host configs - Postgres
## ---------------------------
db_host_url=jdbc:postgresql://172.16.123.1:31435/postgres
db_username=replicaowner
db_password=password

## ---------------------------
##   DB Host configs - MySql
## ---------------------------
#db_host_url=jdbc:mysql://localhost:3306/empdb
#db_username=admin
#db_password=secret00

## ---------------------------
##   DB Host configs - Oracle
## ---------------------------
#db_host_url=jdbc:oracle://128.3.3.9:2102/empdb
#db_username=root
#db_password=pass00rd

```

#### Executor code
Here the config properties are automatically injected, hence env switching does not affect this code.
```java
public class PostGresSqlExecutor {
    private static final Logger LOGGER = LoggerFactory.getLogger(PostGresSqlExecutor.class);
    Map<String, List<Map<String, Object>>> dbRecordsMap = new HashMap<>();
    public static final String RESULTS_KEY = "rows";

    @Inject
    @Named("db_host_url")
    private String dbHostUrl;

    @Inject
    @Named("db_username")
    private String dbUserName;

    @Inject
    @Named("db_password")
    private String dbPassword;

    public Map<String, List<Map<String, Object>>> executeSimpleSql(String simpleSql) {

        LOGGER.info("DB - Executing SQL query: {}", simpleSql);

        List<Map<String, Object>> recordsList = fetchDbRecords(simpleSql);

        // -------------------------------------------------------
        // Put all the fetched rows into nice JSON key and return.
        // -- This make it better to assert SIZE etc in the steps.
        // -- You can choose any key.
        // -------------------------------------------------------
        dbRecordsMap.put(RESULTS_KEY, recordsList);

        return dbRecordsMap;
    }
```

#### Test Logs
See the sample request/response after you have executed the test.

```java
2018-11-30 15:50:07,869 [main] INFO com.xp.springboot.dbutils.PostGresSqlExecutor - DB - Executing SQL query: select * from employees;

2018-11-30 15:50:07,830 [main] INFO org.jsmart.zerocode.core.runner.ZeroCodeMultiStepsScenarioRunnerImpl - 
----- BDD: Scenario:Postgres DB SQL Executor - Simple and generic one  -------

--------- TEST-STEP-CORRELATION-ID: 09857cc4-b13b-48aa-aa52-10a21107a8db ---------
*requestTimeStamp:2018-11-30T15:50:07.857
step:fetch_all
url:com.xp.springboot.dbutils.PostGresSqlExecutor
method:executeSimpleSql
request:
"select * from employees;" 
--------- TEST-STEP-CORRELATION-ID: 09857cc4-b13b-48aa-aa52-10a21107a8db ---------
Response:
{
  "rows" : [ {
    "name" : "Jack",
    "id" : 1
  }, {
    "name" : "Pulsar",
    "id" : 2
  } ]
}
*responseTimeStamp:2018-11-30T15:50:07.958 
*Response delay:101.0 milli-secs 
---------> Assertion: <----------
{
  "rows.SIZE" : 2,
  "rows" : [ {
    "id" : 1,
    "name" : "Jack"
  }, {
    "name" : "Pulsar",
    "id" : 2
  } ]
} 
-done-

2018-11-30 15:50:07,992 [main] INFO com.xp.springboot.dbutils.PostGresSqlExecutor - DB - Executing SQL query: select id, name from employees where name='Pulsar';

--------- TEST-STEP-CORRELATION-ID: 174d132d-07a9-46c0-a8a2-4fd3e38de960 ---------
*requestTimeStamp:2018-11-30T15:50:07.992
step:fetch_with_where
url:com.xp.springboot.dbutils.PostGresSqlExecutor
method:executeSimpleSql
request:
"select id, name from employees where name='Pulsar';" 
--------- TEST-STEP-CORRELATION-ID: 174d132d-07a9-46c0-a8a2-4fd3e38de960 ---------
Response:
{
  "rows" : [ {
    "name" : "Pulsar",
    "id" : 2
  } ]
}
*responseTimeStamp:2018-11-30T15:50:08.002 
*Response delay:10.0 milli-secs 
---------> Assertion: <----------
{
  "rows.SIZE" : 1,
  "rows" : [ {
    "id" : 2,
    "name" : "Pulsar"
  } ]
} 
-done-
```

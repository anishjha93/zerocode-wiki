Yes, just keep them under "headers" section as below(you can choose the fields to keep/skip, order doesn't matter).

e.g.
```javaScript
            "assertions": {
                "status": 200,
                "headers" : {
                    "X-Server-Token": 190215, //<--- e.g. If this is random or indeterministic, then use "$NOT.NULL"
                    "Server" : [ "hsbcbank.co.uk" ],
                    "DateTime" : "$NOT.NULL" //<--- Not null due to indeterministic for every response 
                },
                "body": {
                    "login" : "octocat",
                    "id" : 583231
                }
            }
```

In case you want to use a custom header `token` for your **next step**, then just point your `JSON path` to that header. 
 e.g.
 > `${$.create_emp.response.headers.X-Server-Token}`  //<--- This will resolve to `190215`

>                                  Original Author Name: @kristin-smith

Background
===
_A great time saver!_

This archetype helps a developer or a Dev-In-Test automation-engineer to set up a working maven project quickly. Also, we can think of this archetype might help us to avoid any errors which could otherwise occur during setting up a project manually.

Commands
===
To install the `archetype` locally in your laptop:

1. Navigate to `zerocode-maven-archetype` on your machine. 
1. Run `mvn install` from this directory
    
To generate anew archetype-based project:
1. Navigate to the directory that will house the project. 
> _e.g. a brand new folder or a new git repo._

1. Run 
```
    "mvn archetype:generate 
    -DarchetypeGroupId=com.myproject 
    -DarchetypeArtifactId=zerocodeArchetype 
    -DarchetypeVersion=1.0-SNAPSHOT 
    -DgroupId=com.myproject 
    -DartifactId=zerocodeArchetypeTest"
```
    
3. The generic command format is:
```
    "mvn archetype:generate -DarchetypeGroupId=<custom-archetype group id e.g.>
    -DarchetypeArtifactId=<custom-archetype artifactid>
    -DarchetypeVersion=<custom-archetype version>
    -DgroupId=<new project Group Id>
    -DartifactId=<new project artifact Id>"
```

Tried and Tested CLI
===
```java
$ mvn archetype:generate -DarchetypeGroupId=com.myproject -DarchetypeArtifactId=zerocodeArchetype -DarchetypeVersion=1.0-SNAPSHOT -DgroupId=com.xbox -DartifactId=game-app
```

<img width="916" alt="Green Test" src="https://user-images.githubusercontent.com/12598420/67926647-6a6e3700-fbae-11e9-8d65-755e9820fb57.png">



Optional step
===
This may not be needed for a real or live project. The purpose of the above archetype is to generate a ready-made maven project to make it easy for a developer to start with automation.
    
Add personal GitHub token to test files:
+    In both `post_api_200.json` and `put_api_200.json`, substitute your own GitHub token for the placeholder.
+    In `put_api_200.json`, also update the name of the owner in the URL to your GitHub username
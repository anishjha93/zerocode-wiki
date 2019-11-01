>                                  Original Author Name: @kristin-smith

Background
===
_A great time saver!_

This archetype helps a developer or a Dev-In-Test automation-engineer to set up a working maven project quickly. Also, we can think of this archetype might help us to avoid any errors which could otherwise occur during setting up a project manually.

Sample CLI
===
```java

$ mvn archetype:generate -DarchetypeGroupId=zerocode.archetype -DarchetypeArtifactId=zerocodeArchetype -DarchetypeVersion=1.0-SNAPSHOT -DgroupId=com.xbox -DartifactId=game-app
```

<img width="916" alt="Green Test" src="https://user-images.githubusercontent.com/12598420/67926647-6a6e3700-fbae-11e9-8d65-755e9820fb57.png">

Commands
===
To install the `archetype` locally in your laptop:
### Step 1)
1. Navigate to `zerocode-maven-archetype` on your machine. 
1. Run `mvn install` from this directory

This generates `zerocodeArchetype-1.0-SNAPSHOT.jar`, which is then used for generating the new ready-made project.
![image](https://user-images.githubusercontent.com/12598420/68037188-199a3380-fcbf-11e9-9af5-d7c150b84ddc.png)

### Step 2)    
To generate a new archetype-based project:
1. Navigate to the directory that will house the project. 
> _e.g. a brand new folder or a new git repo._

1. Run 
```
    "mvn archetype:generate 
    -DarchetypeGroupId=zerocode.archetype
    -DarchetypeArtifactId=zerocodeArchetype 
    -DarchetypeVersion=1.0-SNAPSHOT 
    -DgroupId=com.myproject 
    -DartifactId=zerocodeArchetypeTest"
```
    
2. The generic command format is:
```
    "mvn archetype:generate -DarchetypeGroupId=<custom-archetype group id e.g. zerocode.archetype>
    -DarchetypeArtifactId=<custom-archetype artifactid e.g. zerocodeArchetype>
    -DarchetypeVersion=<custom-archetype version e.g. 1.0-SNAPSHOT>
    -DgroupId=<new project Group Id>
    -DartifactId=<new project artifact Id>"
```

The final command should look like below:
> $ mvn archetype:generate -DarchetypeGroupId=zerocode.archetype -DarchetypeArtifactId=zerocodeArchetype -DarchetypeVersion=1.0-SNAPSHOT -DgroupId=com.xbox -DartifactId=game-app


Optional step
===
This may not be needed for a real or live project. The purpose of the above archetype is to generate a ready-made maven project to make it easy for a developer to start with automation.
    
Add personal GitHub token to test files:
+    In both `post_api_200.json` and `put_api_200.json`, substitute your own GitHub token for the placeholder.
+    In `put_api_200.json`, also update the name of the owner in the URL to your GitHub username
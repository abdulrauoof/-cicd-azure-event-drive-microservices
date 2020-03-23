# Azure Function App CI-CD pipeline project

## generate the maven azure functions archetype project
On the terminal:
```
mvn archetype:generate -DarchetypeGroupId=com.microsoft.azure -darchetypeArtificatId=azure-functions-archetype
```

You will be prompted to select your groupId, in this case com.yourname
You will be prompted to enter your artifactId, in this case ci-cd-demo

You can hit enter the next 2 times, and then type "y" to confirm.

# Azure Function App CI-CD pipeline project

## Generate project
On the terminal:
```
mvn archetype:generate -DarchetypeGroupId=com.microsoft.azure -darchetypeArtificatId=azure-functions-archetype
```

You will be prompted to select your groupId, in this case ```com.yourname```

You will be prompted to enter your artifactId, in this case ```ci-cd-demo```

You can hit enter the next 2 times, and then type "y" to confirm.

## References
https://azure.microsoft.com/en-us/resources/videos/azure-friday-java-in-azure-functions/
https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-azure-function-azure-cli?tabs=bash%2Cbrowser&pivots=programming-language-csharp

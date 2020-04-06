# Azure Functions CI/CD Pipeline

## About
The goal of this project will be to create an serverless function in the cloud using Azure Functions, and to create a CI/CD process for the application. We will
be using a HTTP trigger function, which is invoked via HTTP request.

## Environment Setup
Before jumping in you should download the Azure CLI and Azure Functions Core Tools.

https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest
https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local?tabs=windows%2Ccsharp%2Cbash

## Generate Project using Maven
On the terminal:
```
mvn archetype:generate -DarchetypeGroupId=com.microsoft.azure -darchetypeArtificatId=azure-functions-archetype
```

You will be prompted to select your groupId, in this case ```com.yourname```

You will be prompted to enter your artifactId, in this case ```ci-cd-demo```

You can hit enter the next 2 times, and then type "y" to confirm.

This maven archetype will generate an Azure HTTP Trigger function boilerplate code.

## Test Locally
After installing the Azure CLI and Azure Functions Core Tools from above, you can test your function locally.

## References
https://azure.microsoft.com/en-us/resources/videos/azure-friday-java-in-azure-functions/

https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-azure-function-azure-cli?tabs=bash%2Cbrowser&pivots=programming-language-csharp

https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest
# Azure Functions CI/CD Pipeline

## About
The goal of this project will be to create an serverless function in the cloud using Azure Functions, and to create a CI/CD process for the application. We will
be using a HTTP trigger function, which is invoked via HTTP request.

## Environment Setup
Before jumping in you should download the Azure CLI and Azure Functions Core Tools. You will also need to install Node.js, which includes npm, prior to installing Core Tools.

Azure CLI:
https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest

Node.js:
https://docs.npmjs.com/downloading-and-installing-node-js-and-npm

Azure Functions Core Tools:
https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local?tabs=windows%2Ccsharp%2Cbash

## Generate Project using Maven
I will be usung IntelliJ IDEA for this project.

On the terminal:
```
mvn archetype:generate -DarchetypeGroupId=com.microsoft.azure -darchetypeArtificatId=azure-functions-archetype
```

You will be prompted to select your groupId, in this case ```com.yourname```

You will be prompted to enter your artifactId, in this case ```ci-cd-demo```

You can hit enter the next 2 times, and then type "y" to confirm.

This maven archetype will generate an Azure HTTP Trigger function boilerplate code. You can view the typical Maven project directories, that is,
your src/main and src/test directories. src/main will include your Java source code, in the package matching the groupId you specified above. You will
see a **Function** class here, that contains the source code for HTTP Trigger function. The src/test directory will contain your Unit/Integration tests 
that have the same package/namespace matching the source code they are testing i.e Because we have one Unit Test here in the src/test/java/groupId directory,
the name of the file by convention should match what it is testing, that is the **Function** class, thus **FunctionTest**. By convention, the namespace or packagename,
in this *com.groupId* should match the source code file it's testing. Anyway, that's enough about that.


## Test Locally
After installing the Azure CLI and Azure Functions Core Tools from above, you can test your function locally.

We can compile/build our project by running the command below in the command prompt/terminal inside your IDE:

```mvn clean package```

Package is part of the Maven buildlifecycle. It includes compilation and packaging your code into a .jar. You can read more about Maven and its default build lifecycle here:
https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html

To start up or run our function, we use:
```mvn azure-functions:run```

We will now see the local server boot up, and we can test that it is functional by making a sample CURL request to the endpoint (the endpoint will be displayed
as it boots up).

Thus:

```curl http://localhost:7071/api/HttpExample/ -d "Linus Torvald"```

You will see a response like:
```Hello, Linus Torvald```

If you inspect the **Function** source code in src/main/java/yourGroupId, it will make sense as the parameter "name" is passed to the API endpoint,
which is then parsed out. If it is not *null*, then an Http status of *200* (OK) is returned with the value of the name that triggered the API concatenated with *"Hello, "*
Very neat.

## Deploy to the Cloud (Azure)
Now that we generated, compiled/built, and tested our Azure Function locally, we can now deploy it to the cloud (Azure) directly.




## References
https://azure.microsoft.com/en-us/resources/videos/azure-friday-java-in-azure-functions/

https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-azure-function-azure-cli?tabs=bash%2Cbrowser&pivots=programming-language-csharp

https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest
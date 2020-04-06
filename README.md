# Azure Functions CI/CD Pipeline

## About
The goal of this project will be to create an serverless function in the cloud using Azure Functions, and to create a CI/CD process for the application. We will
be using a HTTP trigger function, which is invoked via HTTP request. Furthermore, a CI/CD process will be created, such that the source code of 
the Azure function can be uploaded to Azure DevOps and a CI (Continous Integration) pipeline can be created via *yaml* code, which automates the build process (especially useful with multiple developers)
and then can feed artifacts into the CD pipeline for creating releases and deploying to production for use by customers. It basically streamlines the entire, once arduous process.

Continuous Integreation (CI) means new code changes to an app are regularly built, tested, and merged to a shared repository. 
It’s a solution to the problem of having too many branches of an app in development at once that might conflict with each other.

Continuous deployment (CD) can refer to automatically releasing a developer’s changes from the repository to production, 
where it is usable by customers. It addresses the problem of overloading operations teams with manual processes that slow down app delivery. It builds on the benefits of continuous delivery by automating the next stage in the pipeline.

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

You will need an Azure Subscription. You can get one for free:
https://azure.microsoft.com/en-us/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio

1. After creating the subscription, you will need to log into Azure. Open up command prompt/terminal:
```az login```

2. You will need to create a Resource group
```az group create --name MyTestResourceGroup --location centralus

3. You will need to create a **globally** unique Storage Account name (3-24 lowercase letters only). Replace ```<STORAGE_NAME>``` with your unique name:
```az storage account create --name <STORAGE_NAME> --location centralus --resource-group MyTestResourceGroup --sku Standard_LRS```

4. Create the function app on Azure. Replace ```<APP_NAME>``` with a globally unique name you would like, and ```<STORAGE_NAME>``` with the storage name you used in the previous step:
```az functionapp create --resource-group MyTestResourceGroup --consumption-plan-location centralus --runtime dotnet --name <APP_NAME> --storage-account <STORAGE_NAME>```

Now that your resource group, storage account, and function app are created on Azure cloud, the only thing left to do is publish your local code to the function app you just created:
```func azure functionapp publish <APP_NAME>```


## Azure Portal


## Azure DevOps


## References
https://azure.microsoft.com/en-us/resources/videos/azure-friday-java-in-azure-functions/

https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-azure-function-azure-cli?tabs=bash%2Cbrowser&pivots=programming-language-csharp

https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest
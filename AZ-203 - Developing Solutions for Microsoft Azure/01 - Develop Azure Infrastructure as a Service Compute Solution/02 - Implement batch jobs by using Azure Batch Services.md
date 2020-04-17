# Implement batch jobs by using Azure Batch Services

## Manage batch jobs by using Batch Service API

### Concept

- [**Run parallel workloads**](https://docs.microsoft.com/en-us/azure/batch/batch-technical-overview#run-parallel-workloads) - Batch works well with intrinsically parallel (also known as "embarrassingly parallel") workloads.

- [**Azure Batch Service**](https://docs.microsoft.com/en-us/azure/batch/batch-technical-overview) [**REST API**](https://docs.microsoft.com/en-us/rest/api/batchservice/) - The REST APIs for the Azure Batch service offer developers a means to schedule large-scale parallel and HPC applications in the cloud.

- [**Azure Batch service resources**](https://docs.microsoft.com/en-us/azure/batch/batch-api-basics)
    - [**Account**](https://docs.microsoft.com/en-us/azure/batch/batch-api-basics#account) - A Batch account is a uniquely identified entity within the Batch service.
    - [**Azure Storage account**](https://docs.microsoft.com/en-us/azure/batch/batch-api-basics#azure-storage-account) - Most Batch solutions are Azure Storage for storing resource files and output files.
    - [**Compute node**](https://docs.microsoft.com/en-us/azure/batch/batch-api-basics#compute-node) - A compute node is an Azure virtual machine (VM) or cloud service VM that is dedicated to processing a portion of your application's workload.
    - [**Pool**](https://docs.microsoft.com/en-us/azure/batch/batch-api-basics#pool) - A pool is a collection of nodes that your application runs on.
    - [**Compute node type and target number of nodes**](https://docs.microsoft.com/en-us/azure/batch/batch-api-basics#pool)
        - **Dedicated compute nodes** are reserved for your workloads. They are more expensive than low-priority nodes, but they are guaranteed to never be preempted.
        - **Low-priority nodes** take advantage of surplus capacity in Azure to run your Batch workloads.
    - [**Job**](https://docs.microsoft.com/en-us/azure/batch/batch-api-basics#job) - A job is a collection of tasks.
    - [**Application packages**](https://docs.microsoft.com/en-us/azure/batch/batch-api-basics#application-packages-1) - The application packages feature provides easy management and deployment of applications to the compute nodes in your pools.

- [**Azure Batch service quotas and limits**](https://docs.microsoft.com/en-us/azure/batch/batch-quota-limit)
    - [**Resource quotas**](https://docs.microsoft.com/en-us/azure/batch/batch-quota-limit#resource-quotas) - A quota is a credit limit, not a capacity guarantee.
    - [**Pool size limits**](https://docs.microsoft.com/en-us/azure/batch/batch-quota-limit#pool-size-limits) - Pool size limits are set by the Batch service.

- [**Authorize with Shared Key**](https://docs.microsoft.com/en-us/rest/api/storageservices/authorize-with-shared-key)
    - [**Specifying the Date header**](https://docs.microsoft.com/en-us/rest/api/storageservices/authorize-with-shared-key#specifying-the-date-header) - All authorized requests must include the Coordinated Universal Time (UTC) timestamp for the request.
    - [**Specifying the Authorization header**](https://docs.microsoft.com/en-us/rest/api/storageservices/authorize-with-shared-key#specifying-the-authorization-header) - An authorized request must include the ```Authorization``` header.
        - [**Constructing the signature string**](https://docs.microsoft.com/en-us/rest/api/storageservices/authorize-with-shared-key#constructing-the-signature-string)
        - [**Constructing the canonicalized headers string**](https://docs.microsoft.com/en-us/rest/api/storageservices/authorize-with-shared-key#constructing-the-canonicalized-headers-string)
        - [**Constructing the canonicalized resource string**](https://docs.microsoft.com/en-us/rest/api/storageservices/authorize-with-shared-key#constructing-the-canonicalized-resource-string)
        - [**Encoding the signature**](https://docs.microsoft.com/en-us/rest/api/storageservices/authorize-with-shared-key#encoding-the-signature)

- [**Batch Status and Error Codes**](https://docs.microsoft.com/en-us/rest/api/batchservice/batch-status-and-error-codes) - REST API operations for the Batch service return standard HTTP status codes, as defined in the [HTTP/1.1 Status Code Definitions](https://go.microsoft.com/fwlink/?linkid=133333).

- [**Common parameters and headers**](https://docs.microsoft.com/en-us/rest/api/batchservice/common-parameters-and-headers)
    - [**Representation of Date/Time Values**](https://docs.microsoft.com/en-us/rest/api/batchservice/common-parameters-and-headers#BKMK_DateTime)
        - [**Specifying Date/Time values in HTTP headers**](https://docs.microsoft.com/en-us/rest/api/batchservice/common-parameters-and-headers#specifying-datetime-values-in-http-headers)
        - [**Specifying Date/Time values in URI Parameters and Request/Response Body**](https://docs.microsoft.com/en-us/rest/api/batchservice/common-parameters-and-headers#specifying-datetime-values-in-uri-parameters-and-requestresponse-body)

- [**Specifying conditional headers**](https://docs.microsoft.com/en-us/rest/api/batchservice/specifying-conditional-headers)
    - [**HTTP Response Codes for Operations Supporting Conditional Headers**](https://docs.microsoft.com/en-us/rest/api/batchservice/specifying-conditional-headers#http-response-codes-for-operations-supporting-conditional-headers)
        - [**Read Operations**](https://docs.microsoft.com/en-us/rest/api/batchservice/specifying-conditional-headers#read-operations)
        - [**Write Operations**](https://docs.microsoft.com/en-us/rest/api/batchservice/specifying-conditional-headers#write-operations)

----

## Run a batch job by using Azure CLI, Azure portal, and other tools

### Resource

- [Quickstart: Run your first Batch job with the Azure CLI](https://docs.microsoft.com/en-us/azure/batch/quick-create-cli)
- [Quickstart: Run your first Batch job in the Azure portal](https://docs.microsoft.com/en-us/azure/batch/quick-create-portal)
- [Quickstart: Run your first Azure Batch job with the .NET API](https://docs.microsoft.com/en-us/azure/batch/quick-run-dotnet)
- [Quickstart: Use Python API to run an Azure Batch job](https://docs.microsoft.com/en-us/azure/batch/quick-run-python)

----

## Write code to run an Azure Batch Services batch job

### Concept

- [**Batch Management client library**](https://docs.microsoft.com/en-us/azure/batch/batch-management-dotnet)
    - [**Create and delete Batch accounts**](https://docs.microsoft.com/en-us/azure/batch/batch-management-dotnet#create-and-delete-batch-accounts) within any region.
    - [**Retrieve and regenerate account keys**](https://docs.microsoft.com/en-us/azure/batch/batch-management-dotnet#retrieve-and-regenerate-account-keys) programmatically for any of your Batch accounts.
    - [**Check account quotas**](https://docs.microsoft.com/en-us/azure/batch/batch-management-dotnet#check-azure-subscription-and-batch-account-quotas) and take the trial-and-error guesswork out of determining which Batch accounts have what limits.
    - **Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, Azure Active Directory, and the Azure Resource Manager together in the same application.

### Resource

- [Create a Batch account with the Azure portal](https://docs.microsoft.com/en-us/azure/batch/batch-account-create-portal)
- [AccountManagement sample project](https://github.com/Azure-Samples/azure-batch-samples/tree/master/CSharp/AccountManagement)
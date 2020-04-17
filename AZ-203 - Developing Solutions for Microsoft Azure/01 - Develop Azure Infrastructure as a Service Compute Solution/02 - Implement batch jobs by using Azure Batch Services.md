# Implement batch jobs by using Azure Batch Services

## Azure Batch overview

- Batch works well with [**intrinsically parallel (also known as "embarrassingly parallel") workloads**](https://docs.microsoft.com/en-us/azure/batch/batch-technical-overview#run-parallel-workloads).

- The [**REST APIs**](https://docs.microsoft.com/en-us/rest/api/batchservice/) for the [**Azure Batch service**](https://docs.microsoft.com/en-us/azure/batch/batch-technical-overview) offer developers a means to schedule large-scale parallel and HPC applications in the cloud.

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

## Manage batch jobs by using Batch Service API

### Resource

- [Authorize with Shared Key](https://docs.microsoft.com/en-us/rest/api/storageservices/authorize-with-shared-key)
- [Batch Status and Error Codes](https://docs.microsoft.com/en-us/rest/api/batchservice/batch-status-and-error-codes)
- [Common parameters and headers](https://docs.microsoft.com/en-us/rest/api/batchservice/common-parameters-and-headers)
- [Specifying conditional headers](https://docs.microsoft.com/en-us/rest/api/batchservice/specifying-conditional-headers)
- [Batch Service REST API Versioning](https://docs.microsoft.com/en-us/rest/api/batchservice/batch-service-rest-api-versioning)

----

## Run a batch job by using Azure CLI, Azure portal, and other tools

### Resource

- [Quickstart: Run your first Batch job with the Azure CLI](https://docs.microsoft.com/en-us/azure/batch/quick-create-cli)
- [Quickstart: Run your first Batch job in the Azure portal](https://docs.microsoft.com/en-us/azure/batch/quick-create-portal)
- [Quickstart: Run your first Azure Batch job with the .NET API](https://docs.microsoft.com/en-us/azure/batch/quick-run-dotnet)
- [Quickstart: Use Python API to run an Azure Batch job](https://docs.microsoft.com/en-us/azure/batch/quick-run-python)

----

## Write code to run an Azure Batch Services batch job

### Resource

- [Manage Batch accounts and quotas with the Batch Management client library for .NET](https://docs.microsoft.com/en-us/azure/batch/batch-management-dotnet)
- [Create a Batch account with the Azure portal](https://docs.microsoft.com/en-us/azure/batch/batch-account-create-portal)
- [AccountManagement sample project](https://github.com/Azure-Samples/azure-batch-samples/tree/master/CSharp/AccountManagement)

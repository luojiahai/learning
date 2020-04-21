# Develop solutions that use blob storage

## Azure Blob storage overview

- [**Azure Blob storage**](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blobs-overview) is Microsoft's object storage solution for the cloud. Blob storage is optimized for storing massive amounts of unstructured data. Unstructured data is data that doesn't adhere to a particular data model or definition, such as text or binary data.

- Blob storage is designed for:
    - Serving images or documents directly to a browser.
    - Storing files for distributed access.
    - Streaming video and audio.
    - Writing to log files.
    - Storing data for backup and restore, disaster recovery, and archiving.
    - Storing data for analysis by an on-premises or Azure-hosted service.

- Azure storage offers different [**access tiers**](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-storage-tiers), which allow you to store blob object data in the most cost-effective manner. The available access tiers include:
    - **Hot** - Optimized for storing data that is accessed frequently.
    - **Cool** - Optimized for storing data that is infrequently accessed and stored for at least 30 days.
    - **Archive** - Optimized for storing data that is rarely accessed and stored for at least 180 days with flexible latency requirements (on the order of hours).
    
- The storage service offers three [**types of blobs**](https://docs.microsoft.com/en-us/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs), *block blobs*, *append blobs*, and *page blobs*.

- [**Azure Storage events**](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-event-overview) allow applications to react to events, such as the creation and deletion of blobs. It does so without the need for complicated code or expensive and inefficient polling services.

----

## Move items in Blob storage between storage accounts or containers

### Resource

- [storage-blob-dotnet-getting-started/BlobStorage/Advanced.cs](https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs)

----

## Set and retrieve properties and metadata

### Resource

- [Setting and retrieving properties and metadata for Blob service resources](https://docs.microsoft.com/en-us/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources)
- [Manage container properties and metadata with .NET](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-container-properties-metadata)

----

## Implement blob leasing

### Resource

- [az storage blob lease](https://docs.microsoft.com/en-us/cli/azure/storage/blob/lease?view=azure-cli-latest)

----

## Implement data archiving and retention

### Concept

- The [**archive access tier**](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-storage-tiers#archive-access-tier) has the lowest storage cost. But it has higher data retrieval costs compared to the hot and cool tiers. Data in the archive tier can take several hours to retrieve. Data must remain in the archive tier for at least 180 days or be subject to an early deletion charge.

----

## Implement Geo Zone Redundant Storage

### Concept

- Azure Storage always stores multiple copies of your data so that it is protected from planned and unplanned events, including transient hardware failures, network or power outages, and massive natural disasters. [**Redundancy**](https://docs.microsoft.com/en-us/azure/storage/common/storage-redundancy) ensures that your storage account meets the Service-Level Agreement (SLA) for Azure Storage even in the face of failures.

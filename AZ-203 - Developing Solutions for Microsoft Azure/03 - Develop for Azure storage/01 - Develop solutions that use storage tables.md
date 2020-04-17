# Develop solutions that use storage tables

## Design and implement policies for tables

### Concept

- [**Azure Table storage**](https://docs.microsoft.com/en-us/azure/cosmos-db/table-storage-overview) is a service that stores structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.

- [**Azure Table storage**](https://docs.microsoft.com/en-us/azure/cosmos-db/table-storage-overview#what-is-table-storage) stores large amounts of structured data. The service is a NoSQL datastore which accepts authenticated calls from inside and outside the Azure cloud. Azure tables are ideal for storing structured, non-relational data. Common uses of Table storage include:
    - Storing TBs of structured data capable of serving web scale applications
    - Storing datasets that don't require complex joins, foreign keys, or stored procedures and can be denormalized for fast access
    - Quickly querying data using a clustered index
    - Accessing data using the OData protocol and LINQ queries with WCF Data Service .NET Libraries

- Table storage contains the following components:
    - **URL format** - Azure Table Storage accounts use this format: ```http://<storage account>.table.core.windows.net/<table>```
    - **Accounts** - All access to Azure Storage is done through a storage account.
    - **Table** - A table is a collection of entities.
    - **Entity** - An entity is a set of properties, similar to a database row.
    - **Properties** - A property is a name-value pair.
    
- [**Introduction to Azure Cosmos DB: Table API**](https://docs.microsoft.com/en-us/azure/cosmos-db/table-introduction)
    
- [**Guidelines for table design**](https://docs.microsoft.com/en-us/azure/storage/tables/table-storage-design-guidelines)

- [**Design scalable and performant tables**](https://docs.microsoft.com/en-us/azure/storage/tables/table-storage-design)

- [**Design for querying**](https://docs.microsoft.com/en-us/azure/storage/tables/table-storage-design-for-query)

### Resource

- [Authorize with Shared Key](https://docs.microsoft.com/en-us/rest/api/storageservices/authorize-with-shared-key)
- [Define a stored access policy](https://docs.microsoft.com/en-us/rest/api/storageservices/define-stored-access-policy)
- [Configure Cross-Origin Resource Sharing (CORS)](https://docs.microsoft.com/en-us/azure/cosmos-db/how-to-configure-cross-origin-resource-sharing)
    
---- 

## Query table storage by using code

### Resource

- [Addressing Table Service Resources](https://docs.microsoft.com/en-us/rest/api/storageservices/addressing-table-service-resources)
- [Query timeout and pagination](https://docs.microsoft.com/en-us/rest/api/storageservices/query-timeout-and-pagination)
- [Querying tables and entities](https://docs.microsoft.com/en-us/rest/api/storageservices/querying-tables-and-entities)
- [Inserting and updating entities](https://docs.microsoft.com/en-us/rest/api/storageservices/inserting-and-updating-entities)

----

## Implement partitioning schemes

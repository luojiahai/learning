## Develop for Azure storage (15-20%)

### Develop solutions that use storage tables
#### design and implement policies for tables
- [Security recommendations for Blob storage](https://docs.microsoft.com/en-us/azure/storage/blobs/security-recommendations)
#### query table storage by using code
- [Get started with Azure Cosmos DB Table API and Azure Table storage using the .NET SDK](https://docs.microsoft.com/en-us/azure/cosmos-db/tutorial-develop-table-dotnet)
    ```csharp
    // Retrieve storage account information from connection string.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConnectionString);

    // Create a table client for interacting with the table service
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient(new TableClientConfiguration());

    // Create a table from the table client
    CloudTable table = tableClient.GetTableReference(tableName);

    // Create the InsertOrReplace table operation
    TableOperation insertOrMergeOperation = TableOperation.InsertOrMerge(entity);

    // Execute the operation.
    TableResult result = await table.ExecuteAsync(insertOrMergeOperation);
    CustomerEntity insertedCustomer = result.Result as CustomerEntity;

    // Get an entity from a partition
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>(partitionKey, rowKey);
    TableResult result = await table.ExecuteAsync(retrieveOperation);
    CustomerEntity customer = result.Result as CustomerEntity;

    // Delete an entity
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
    TableResult result = await table.ExecuteAsync(deleteOperation);
    ```
#### implement partitioning schemes
- [Partitioning Azure blob storage](https://docs.microsoft.com/en-us/azure/architecture/best-practices/data-partitioning-strategies#partitioning-azure-blob-storage)
- [Horizontal, vertical, and functional data partitioning](https://docs.microsoft.com/en-us/azure/architecture/best-practices/data-partitioning)

### Develop solutions that use Cosmos DB storage
#### create, read, update, and delete data by using appropriate APIs
- [Azure Cosmos DB documentation](https://docs.microsoft.com/en-us/azure/cosmos-db/)
#### implement partitioning schemes
- [Partitioning Cosmos DB](https://docs.microsoft.com/en-us/azure/architecture/best-practices/data-partitioning-strategies#partitioning-cosmos-db)
#### set the appropriate consistency level for operations
- [Choose the right consistency level](https://docs.microsoft.com/en-us/azure/cosmos-db/consistency-levels-choosing)

### Develop solutions that use a relational database
#### provision and configure relational databases
- [Create an Azure SQL Database single database](https://docs.microsoft.com/en-us/azure/azure-sql/database/single-database-create-quickstart)
    - Azure PowerShell
        ```azurepowershell-interactive
        # Creates a resource group in which all resources are stored.
        New-AzResourceGroup

        # Creates a server that hosts databases and elastic pools.
        New-AzSqlServer

        # Creates a server-level firewall rule for a server.
        New-AzSqlServerFirewallRule

        #Creates a database.
        New-AzSqlDatabase
        ```
    - Azure CLI
        ```azurecli
        # Sets a subscription to be the current active subscription.
        az account set

        # Creates a resource group in which all resources are stored.
        az group create

        # Creates a server that hosts databases and elastic pools.
        az sql server create

        # Creates a server-level firewall rule.
        az sql server firewall-rule create

        # Creates a database.
        az sql db create
        ```
#### configure elastic pools for Azure SQL Database
- [Manage elastic pools in Azure SQL Database](https://docs.microsoft.com/en-us/azure/azure-sql/database/elastic-pool-manage)
    - Azure PowerShell
        ```azurepowershell-interactive
        # Creates an elastic pool.
        New-AzSqlElasticPool

        # Gets elastic pools and their property values.
        Get-AzSqlElasticPool

        # Modifies properties of an elastic pool For example, use the StorageMB property to modify the max storage of an elastic pool.
        Set-AzSqlElasticPool

        # Deletes an elastic pool.
        Remove-AzSqlElasticPool

        # Gets the status of operations on an elastic pool
        Get-AzSqlElasticPoolActivity

        # Creates a new database in an existing pool or as a single database.
        New-AzSqlDatabase

        # Gets one or more databases.
        Get-AzSqlDatabase

        # Sets properties for a database, or moves an existing database into, out of, or between elastic pools.
        Set-AzSqlDatabase

        # Removes a database.
        Remove-AzSqlDatabase
        ```
    - Azure CLI
        ```azurecli
        # Creates an elastic pool.
        az sql elastic-pool create

        # Returns a list of elastic pools in a server.
        az sql elastic-pool list

        # Returns a list of databases in an elastic pool.
        az sql elastic-pool list-dbs

        # Also includes available pool DTU settings, storage limits, and per database settings. In order to reduce verbosity, additional storage limits and per database settings are hidden by default.
        az sql elastic-pool list-editions

        # Updates an elastic pool.
        az sql elastic-pool update

        # Deletes the elastic pool.
        az sql elastic-pool delete
        ```
#### create, read, update, and delete data tables by using code
- [Query the database](https://docs.microsoft.com/en-us/azure/azure-sql/database/single-database-create-quickstart#query-the-database)
#### provision and configure Azure SQL Database serverless instances
- [Azure SQL Database serverless](https://docs.microsoft.com/en-us/azure/azure-sql/database/serverless-tier-overview)
#### provision and configure Azure SQL and Azure PostgreSQL Hyperscale instances
- [Hyperscale service tier](https://docs.microsoft.com/en-us/azure/azure-sql/database/service-tier-hyperscale)

### Develop solutions that use blob storage
#### move items in Blob storage between storage accounts or containers
- [storage-blob-dotnet-getting-started/BlobStorage/Advanced.cs](https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs)
#### set and retrieve properties and metadata
- [Manage container properties and metadata with .NET](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-container-properties-metadata)
    ```csharp
    // Fetch some container properties and write out their values.
    var properties = await container.GetPropertiesAsync();

    // Add some metadata to the container.
    metadata.Add("docType", "textDocuments");
    metadata.Add("category", "guidance");

    // Set the container's metadata.
    await container.SetMetadataAsync(metadata);

    // Enumerate the container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in properties.Value.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
    ```
#### implement blob leasing
- [az storage blob lease](https://docs.microsoft.com/en-us/cli/azure/storage/blob/lease)
    ```
    # Requests a new lease.
    az storage blob lease acquire

    # Breaks the lease, if the blob has an active lease.
    az storage blob lease break

    # Changes the lease ID of an active lease.
    az storage blob lease change

    # Releases the lease.
    az storage blob lease release

    # Renews the lease.
    az storage blob lease renew	
    ```
#### implement data archiving and retention
- [Azure Blob storage: hot, cool, and archive access tiers](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-storage-tiers)
    ```azurepowershell-interactive
    --- HOT
    # Change the storage account tier to hot
    Set-AzStorageAccount -ResourceGroupName $rgName -Name $accountName -AccessTier Hot

    --- ARCHIVE
    # Select the storage account and get the context
    $storageAccount = Get-AzStorageAccount -ResourceGroupName $rgName -Name $accountName
    $ctx = $storageAccount.Context

    # Select the blob from a container
    $blob = Get-AzStorageBlob -Container $containerName -Blob $blobName -Context $ctx

    # Change the blob’s access tier to archive
    $blob.ICloudBlob.SetStandardBlobTier("Archive")
    ```
#### implement Geo Zone Redundant Storage
- [Azure Storage redundancy](https://docs.microsoft.com/en-us/azure/storage/common/storage-redundancy)
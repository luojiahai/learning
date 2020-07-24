## Connect to and consume Azure services and third####party services (20-25%)

### Develop an App Service Logic App
#### create a Logic App
- [Create logic app workflows from prebuilt templates](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-create-logic-apps-from-templates#create-logic-apps-from-templates)
#### create a custom connector for Logic Apps
- [Custom connectors in Logic Apps](https://docs.microsoft.com/en-us/azure/logic-apps/custom-connector-overview)
#### create a custom template for Logic Apps
- [Automate deployment for Azure Logic Apps by using Azure Resource Manager templates](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-azure-resource-manager-templates-overview)

### Integrate Azure Search within solutions
#### create an Azure Search index, import searchable data, query the Azure Search index, implement cognitive search
- [Create a search index in .NET](https://docs.microsoft.com/en-us/azure/search/search-get-started-dotnet)
- [Create an Azure Cognitive Search index in PowerShell using REST APIs](https://docs.microsoft.com/en-us/azure/search/search-get-started-powershell)
- [Create an Azure Cognitive Search index in the Azure portal](https://docs.microsoft.com/en-us/azure/search/search-get-started-portal)

### Implement API management
#### establish API Gateways

#### create an APIM instance
- [Create a new Azure API Management service instance by using PowerShell](https://docs.microsoft.com/en-us/azure/api-management/powershell-create-service-instance)
#### configure authentication for APIs
- [How to secure APIs using client certificate authentication in API Management](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates-for-clients)
#### define policies for APIs
- [API Management policies](https://docs.microsoft.com/en-us/azure/api-management/api-management-policies)

### Develop event-based solutions
#### implement solutions that use Azure Event Grid
- [Azure Event Grid documentation](https://docs.microsoft.com/en-us/azure/event-grid/)
#### implement solutions that use Azure Notification Hubs
- [Azure Notification Hubs documentation](https://docs.microsoft.com/en-us/azure/notification-hubs/)
#### implement solutions that use Azure Event Hub
- [Azure Event Hubs documentation](https://docs.microsoft.com/en-us/azure/event-hubs/)

### Develop message-based solutions
#### implement solutions that use Azure Service Bus
- [Azure Service Bus Messaging documentation](https://docs.microsoft.com/en-us/azure/service-bus-messaging/)
#### implement solutions that use Azure Queue Storage queues
- [Get started with Azure Queue storage using .NET](https://docs.microsoft.com/en-us/azure/storage/queues/storage-dotnet-how-to-use-queues)
    ```csharp
    # Add using directives
    using System; // Namespace for Console output
    using System.Configuration; // Namespace for ConfigurationManager
    using System.Threading.Tasks; // Namespace for Task
    using Azure.Storage.Queues; // Namespace for Queue storage types
    using Azure.Storage.Queues.Models; // Namespace for PeekedMessage

    # Create the Queue service client
    // Get the connection string from app settings
    string connectionString = ConfigurationManager.AppSettings["storageConnectionString"];

    // Instantiate a QueueClient which will be used to create and manipulate the queue
    QueueClient queueClient = new QueueClient(connectionString, "myqueue");

    # Create a queue
    // Get the connection string from app settings
    string connectionString = ConfigurationManager.AppSettings["storageConnectionString"];

    // Instantiate a QueueClient which will be used to create and manipulate the queue
    QueueClient queueClient = new QueueClient(connectionString, "myqueue");

    // Create the queue
    queueClient.CreateIfNotExists();

    # Insert a message into a queue
    // Create the text message to add to the queue
    string message = "First Message to azure Queue";

    // Send a message to the queue
    queueClient.SendMessage(message);

    # Peek at the next message
    // Peek at the next message
    PeekedMessage[] peekedMessage = queueClient.PeekMessages();

    // Display the message
    Console.WriteLine($"Peeked message: '{peekedMessage[0].MessageText}'");
    
    # Change the contents of a queued message
    // Get the message from the queue
    QueueMessage[] message = queueClient.ReceiveMessages();

    // Update the message contents
    queueClient.UpdateMessage(message[0].MessageId, 
            message[0].PopReceipt, 
            "Updated contents",
            TimeSpan.FromSeconds(60.0)  // Make it invisible for another 60 seconds
        );

    # De-queue the next message
    // Get the next message
    QueueMessage[] retrievedMessage = queueClient.ReceiveMessages();

    // Process (i.e. print) the message in less than 30 seconds
    Console.WriteLine($"De-queued message: '{retrievedMessage[0].MessageText}'");

    // Delete the message
    queueClient.DeleteMessage(retrievedMessage[0].MessageId, retrievedMessage[0].PopReceipt);

    # Use Async-Await pattern with common Queue storage APIs
    // Async enqueue the message
    await queueClient.SendMessageAsync("Hello, World");
    Console.WriteLine($"Message added");

    // Async receive the message
    QueueMessage[] retrievedMessage = await queueClient.ReceiveMessagesAsync();
    Console.WriteLine($"Retrieved message with content '{retrievedMessage[0].MessageText}'");

    // Async delete the message
    await queueClient.DeleteMessageAsync(retrievedMessage[0].MessageId, retrievedMessage[0].PopReceipt);
    Console.WriteLine($"Deleted message: '{retrievedMessage[0].MessageText}'");

    // Async delete the queue
    await queueClient.DeleteAsync();
    Console.WriteLine($"Deleted queue: '{queueClient.Name}'");

    # Leverage additional options for de-queuing messages
    // Receive and process 20 messages
    QueueMessage[] receivedMessages = queueClient.ReceiveMessages(20, TimeSpan.FromMinutes(5));

    foreach (QueueMessage message in receivedMessages)
    {
        // Process (i.e. print) the messages in less than 5 minutes
        Console.WriteLine($"De-queued message: '{message.MessageText}'");

        // Delete the message
        queueClient.DeleteMessage(message.MessageId, message.PopReceipt);
    }

    # Get the queue length
    QueueProperties properties = queueClient.GetProperties();

    // Retrieve the cached approximate message count.
    int cachedMessagesCount = properties.ApproximateMessagesCount;

    # Delete a queue
    // Delete the queue
    queueClient.Delete();
    ```
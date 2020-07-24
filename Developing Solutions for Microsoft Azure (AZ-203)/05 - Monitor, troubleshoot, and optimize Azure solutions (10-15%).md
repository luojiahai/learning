## Monitor, troubleshoot, and optimize Azure solutions (10-15%)

### Develop code to support scalability of apps and services
#### implement autoscaling rules and patterns (schedule, operational/system metrics, singleton applications)
- [Autoscaling](https://docs.microsoft.com/en-us/azure/architecture/best-practices/auto-scaling)
#### implement code that handles transient faults
- [Transient fault handling](https://docs.microsoft.com/en-us/azure/architecture/best-practices/transient-faults)
#### implement AKS scaling strategies
- [Automatically scale a cluster to meet application demands on Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/cluster-autoscaler)

### Integrate caching and content delivery within solutions
#### store and retrieve data in Azure Redis cache
- [Use Azure Cache for Redis with a .NET Framework application](https://docs.microsoft.com/en-us/azure/azure-cache-for-redis/cache-dotnet-how-to-use-azure-redis-cache)
    ```csharp
    # Connect to the cache
    using StackExchange.Redis;
    using System.Configuration;

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

    # Executing cache commands
    cache.Execute(cacheCommand);

    # Get and put of integral data types into the cache
    cache.StringGet("Message");
    cache.StringSet("Message", <MESSAGE>);

    # Work with .NET objects in the cache
    using Newtonsoft.Json;

    Employee e007 = new Employee("007", "Davide Columbo", 100);
    cache.StringSet("e007", JsonConvert.SerializeObject(e007));
    ```
#### develop code to implement CDN’s in solutions
- [Getting started on managing CDN in C#](https://docs.microsoft.com/en-us/samples/azure-samples/cdn-dotnet-manage-cdn/getting-started-on-managing-cdn-in-c/)
#### invalidate cache content (CDN or Redis)
-[Purge an Azure CDN endpoint](https://docs.microsoft.com/en-us/azure/cdn/cdn-purge-endpoint)

### Instrument solutions to support monitoring and logging
#### configure instrumentation in an app or service by using Application Insights
- [Set up Application Insights for your ASP.NET website](https://docs.microsoft.com/en-us/azure/azure-monitor/app/asp-net)
#### analyze and troubleshoot solutions by using Azure Monitor
- [Get started with Log Analytics queries](https://docs.microsoft.com/en-us/azure/azure-monitor/log-query/get-started-portal)
#### implement Application Insights Web Test and Alerts
- [Creating an Application Insights Web Test and Alert Programmatically](https://azure.microsoft.com/en-us/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
# Developing Solutions for Microsoft Azure (AZ-203)

## Develop Azure Infrastructure as a Service Compute Solution (10-15%)

### Implement solutions that use virtual machines (VM)
- provision VMs
    - [Azure PowerShell](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-powershell)
        ```
        # Create a resource group
        New-AzResourceGroup -Name "myResourceGroup" -Location "EastUS"

        # Create virtual network resources
        New-AzNetworkInterface `
        -Name "myNic" `
        -ResourceGroupName "myResourceGroup" `
        -Location "EastUS" `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

        # Create a virtual machine
        New-AzVM `
        -ResourceGroupName "myResourceGroup" `
        -Location eastus -VM $vmConfig

        # Get public IP address
        Get-AzPublicIpAddress -ResourceGroupName "myResourceGroup" | Select "IpAddress"

        # Clean up resources
        Remove-AzResourceGroup -Name "myResourceGroup"
        ```
    - [Azure CLI](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-cli)
        ```
        # Create a resource group
        az group create --name myResourceGroup --location eastus

        # Create a virtual machine
        az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys

        # Open port 80 for web traffic
        az vm open-port --port 80 --resource-group myResourceGroup --name myVM

        # Clean up resources
        az group delete --name myResourceGroup
        ```
- create ARM templates
    - [Azure PowerShell](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/quickstart-create-templates-use-visual-studio-code?tabs=PowerShell)
        ```
        # Deploy the template
        New-AzResourceGroup -Name arm-vscode -Location eastus
        New-AzResourceGroupDeployment -ResourceGroupName arm-vscode -TemplateFile ./azuredeploy.json -TemplateParameterFile ./azuredeploy.parameters.json

        # Clean up resources
        Remove-AzResourceGroup -Name arm-vscode
        ```
    - [Azure CLI](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/quickstart-create-templates-use-visual-studio-code?tabs=CLI)
        ```
        # Deploy the template
        az group create --name arm-vscode --location eastus
        az deployment group create --resource-group arm-vscode --template-file azuredeploy.json --parameters azuredeploy.parameters.json

        # Clean up resources
        az group delete --name arm-vscode
        ```
- configure Azure Disk Encryption for VMs
    - [Azure PowerShell](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/disk-encryption-powershell-quickstart)
        ```
        # Create a resource group
        New-AzResourceGroup -Name "myResourceGroup" -Location "EastUS"

        # Create a virtual machine
        $cred = Get-Credential
        New-AzVM -Name MyVm -Credential $cred -ResourceGroupName MyResourceGroup -Image Canonical:UbuntuServer:18.04-LTS:latest -Size Standard_D2S_V3

        # Create a Key Vault configured for encryption keys
        New-AzKeyvault -name "<your-unique-keyvault-name>" -ResourceGroupName "myResourceGroup" -Location EastUS -EnabledForDiskEncryption

        # Encrypt the virtual machine
        $KeyVault = Get-AzKeyVault -VaultName "<your-unique-keyvault-name>" -ResourceGroupName "MyResourceGroup"
        Set-AzVMDiskEncryptionExtension -ResourceGroupName MyResourceGroup -VMName "MyVM" -DiskEncryptionKeyVaultUrl $KeyVault.VaultUri -DiskEncryptionKeyVaultId $KeyVault.ResourceId -SkipVmBackup -VolumeType All

        # Verify the encryption process
        Get-AzVmDiskEncryptionStatus -VMName MyVM -ResourceGroupName MyResourceGroup
        ```
    - [Azure CLI](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/disk-encryption-cli-quickstart)
        ```
        # Create a resource group
        az group create --name "myResourceGroup" --location "eastus"

        # Create a virtual machine
        az vm create \
        --resource-group "myResourceGroup" \
        --name "myVM" \
        --image "Canonical:UbuntuServer:16.04-LTS:latest" \
        --size "Standard_D2S_V3"\
        --generate-ssh-keys

        # Create a Key Vault configured for encryption keys
        az keyvault create --name "<your-unique-keyvault-name>" --resource-group "myResourceGroup" --location "eastus" --enabled-for-disk-encryption

        # Encrypt the virtual machine
        az vm encryption enable -g "MyResourceGroup" --name "myVM" --disk-encryption-keyvault "<your-unique-keyvault-name>"

        # Verify the encryption process
        az vm show --name "myVM" -g "MyResourceGroup"
        ```

### Implement batch jobs by using Azure Batch Services
- manage batch jobs by using Batch Service API
- run a batch job by using Azure CLI, Azure portal, and other tools
- write code to run an Azure Batch Services batch job

### Create containerized solutions
- create an Azure Managed Kubernetes Service (AKS) cluster
- create container images for solutions
- publish an image to the Azure Container Registry
- run containers by using Azure Container Instance or AKS

## Develop Azure Platform as a Service Compute Solution (20-25%)

### Create Azure App Service Web Apps
- create an Azure App Service Web App
- create an Azure App Service background task by using WebJobs
- enable diagnostics logging
- create an Azure Web App for Containers
- monitor service health by using Azure Monitor

### Create Azure App Service mobile apps
- add push notifications for mobile apps
- enable offline sync for mobile app
- implement a remote instrumentation strategy for mobile devices

### Create Azure App Service API apps
- create an Azure App Service API app
- create documentation for the API by using open source and other tools

### Implement Azure functions
- implement input and output bindings for a function
- implement function triggers by using data operations, timers, and webhooks
- implement Azure Durable Functions
- create Azure Function apps by using Visual Studio
- implement Python Azure Functions

## Develop for Azure storage (15-20%)
Develop solutions that use storage tables
- design and implement policies for tables
- query table storage by using code
- implement partitioning schemes

### Develop solutions that use Cosmos DB storage
- create, read, update, and delete data by using appropriate APIs
- implement partitioning schemes
- set the appropriate consistency level for operations

### Develop solutions that use a relational database
- provision and configure relational databases
- configure elastic pools for Azure SQL Database
- create, read, update, and delete data tables by using code
- provision and configure Azure SQL Database serverless instances
- provision and configure Azure SQL and Azure PostgreSQL Hyperscale instances

### Develop solutions that use blob storage
- move items in Blob storage between storage accounts or containers
- set and retrieve properties and metadata
- implement blob leasing
- implement data archiving and retention
- implement Geo Zone Redundant Storage

## Implement Azure security (10-15%)

### Implement authentication
- implement authentication by using certificates, forms-based authentication, or tokens
- implement multi-factor or Windows authentication by using Azure AD
- implement OAuth2 authentication
- implement Managed identities/Service Principal authentication
- implement Microsoft identity platform

### Implement access control
- implement CBAC (Claims-Based Access Control) authorization
- implement RBAC (Role-Based Access Control) authorization
- create shared access signatures

### Implement secure data solutions
- encrypt and decrypt data at rest and in transit
- create, read, update, and delete keys, secrets, and certificates by using the KeyVault API

## Monitor, troubleshoot, and optimize Azure solutions (10-15%)

### Develop code to support scalability of apps and services
- implement autoscaling rules and patterns (schedule, operational/system metrics, singleton applications)
- implement code that handles transient faults
- implement AKS scaling strategies

### Integrate caching and content delivery within solutions
- store and retrieve data in Azure Redis cache
- develop code to implement CDN’s in solutions
- invalidate cache content (CDN or Redis)

### Instrument solutions to support monitoring and logging
- configure instrumentation in an app or service by using Application Insights
- analyze and troubleshoot solutions by using Azure Monitor
- implement Application Insights Web Test and Alerts

## Connect to and consume Azure services and third-party services (20-25%)

### Develop an App Service Logic App
- create a Logic App
- create a custom connector for Logic Apps
- create a custom template for Logic Apps

### Integrate Azure Search within solutions
- create an Azure Search index
- import searchable data
- query the Azure Search index
- implement cognitive search

### Implement API management
- establish API Gateways
- create an APIM instance
- configure authentication for APIs
- define policies for APIs

### Develop event-based solutions
- implement solutions that use Azure Event Grid
- implement solutions that use Azure Notification Hubs
- implement solutions that use Azure Event Hub
Develop message-based solutions
- implement solutions that use Azure Service Bus
- implement solutions that use Azure Queue Storage queues
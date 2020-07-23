# Developing Solutions for Microsoft Azure (AZ-203)

## Develop Azure Infrastructure as a Service Compute Solution (10-15%)

### Implement solutions that use virtual machines (VM)
- provision VMs
    - [Azure PowerShell](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-powershell)
        ```azurepowershell-interactive
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
        ```azurecli
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
        ```azurepowershell-interactive
        # Deploy the template
        New-AzResourceGroup -Name arm-vscode -Location eastus
        New-AzResourceGroupDeployment -ResourceGroupName arm-vscode -TemplateFile ./azuredeploy.json -TemplateParameterFile ./azuredeploy.parameters.json

        # Clean up resources
        Remove-AzResourceGroup -Name arm-vscode
        ```
    - [Azure CLI](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/quickstart-create-templates-use-visual-studio-code?tabs=CLI)
        ```azurecli
        # Deploy the template
        az group create --name arm-vscode --location eastus
        az deployment group create --resource-group arm-vscode --template-file azuredeploy.json --parameters azuredeploy.parameters.json

        # Clean up resources
        az group delete --name arm-vscode
        ```
- configure Azure Disk Encryption for VMs
    - [Azure PowerShell](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/disk-encryption-powershell-quickstart)
        ```azurepowershell-interactive
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

        # Clean up resources
        Remove-AzResourceGroup -Name "myResourceGroup"
        ```
    - [Azure CLI](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/disk-encryption-cli-quickstart)
        ```azurecli
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

        # Clean up resources
        az group delete --name "myResourceGroup"
        ```

### Implement batch jobs by using Azure Batch Services
- manage batch jobs by using Batch Service API
    - [Azure Batch Service REST API Reference](https://docs.microsoft.com/en-us/rest/api/batchservice/)
- run a batch job by using Azure CLI, Azure portal, and other tools
    - [Azure CLI](https://docs.microsoft.com/en-us/azure/batch/quick-create-cli)
        ```azurecli
        # Create a resource group
        az group create \
        --name myResourceGroup \
        --location eastus2

        # Create a storage account
        az storage account create \
        --resource-group myResourceGroup \
        --name mystorageaccount \
        --location eastus2 \
        --sku Standard_LRS

        # Create a Batch account
        az batch account create \
        --name mybatchaccount \
        --storage-account mystorageaccount \
        --resource-group myResourceGroup \
        --location eastus2

        # Authenticate with Batch
        az batch account login \
        --name mybatchaccount \
        --resource-group myResourceGroup \
        --shared-key-auth

        # Create a pool of compute nodes
        az batch pool create \
        --id mypool --vm-size Standard_A1_v2 \
        --target-dedicated-nodes 2 \
        --image canonical:ubuntuserver:16.04-LTS \
        --node-agent-sku-id "batch.node.ubuntu 16.04" 

        # Shows all the properties of the pool
        az batch pool show --pool-id mypool \
        --query "allocationState"

        # Create a job
        az batch job create \
        --id myjob \
        --pool-id mypool

        # Create tasks
        for i in {1..4}
        do
        az batch task create \
            --task-id mytask$i \
            --job-id myjob \
            --command-line "/bin/bash -c 'printenv | grep AZ_BATCH; sleep 90s'"
        done

        # View task status
        az batch task show \
        --job-id myjob \
        --task-id mytask1

        # View task output
        az batch task file list \
        --job-id myjob \
        --task-id mytask1 \
        --output table

        # Download one of the output files
        az batch task file download \
        --job-id myjob \
        --task-id mytask1 \
        --file-path stdout.txt \
        --destination ./stdout.txt

        # Clean up resources
        az batch pool delete --pool-id mypool
        az group delete --name myResourceGroup
        ```
    - [.NET](https://docs.microsoft.com/en-us/azure/batch/quick-run-dotnet)
        ```csharp
        # Create a pool of compute nodes
        CloudPool pool = batchClient.PoolOperations.CreatePool(
            poolId: PoolId,
            targetDedicatedComputeNodes: PoolNodeCount,
            virtualMachineSize: PoolVMSize,
            virtualMachineConfiguration: vmConfiguration);

        pool.Commit();

        # Create a Batch job
        CloudJob job = batchClient.JobOperations.CreateJob();
        job.Id = JobId;
        job.PoolInformation = new PoolInformation { PoolId = PoolId };

        job.Commit();

        # Create tasks
        for (int i = 0; i < inputFiles.Count; i++)
        {
            string taskId = String.Format("Task{0}", i);
            string inputFilename = inputFiles[i].FilePath;
            string taskCommandLine = String.Format("cmd /c type {0}", inputFilename);

            CloudTask task = new CloudTask(taskId, taskCommandLine);
            task.ResourceFiles = new List<ResourceFile> { inputFiles[i] };
            tasks.Add(task);
        }

        batchClient.JobOperations.AddTask(JobId, tasks);

        # View task output
        foreach (CloudTask task in completedtasks)
        {
            string nodeId = String.Format(task.ComputeNodeInformation.ComputeNodeId);
            Console.WriteLine("Task: {0}", task.Id);
            Console.WriteLine("Node: {0}", nodeId);
            Console.WriteLine("Standard out:");
            Console.WriteLine(task.GetNodeFile(Constants.StandardOutFileName).ReadAsString());
        }
        ```
- write code to run an Azure Batch Services batch job
    - [Azure Batch Samples](https://github.com/Azure-Samples/azure-batch-samples)

### Create containerized solutions
- create an Azure Managed Kubernetes Service (AKS) cluster
    - [Azure PowerShell](https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough-powershell)
        ```azurepowershell-interactive
        # Create a resource group
        New-AzResourceGroup -Name myResourceGroup -Location eastus

        # Create AKS cluster
        New-AzAks -ResourceGroupName myResourceGroup -Name myAKSCluster -NodeCount 1

        # Connect to the cluster
        Install-AzAksKubectl
        Import-AzAksCredential -ResourceGroupName myResourceGroup -Name myAKSCluster
        .\kubectl get nodes
        
        # Run the application - with a Kubernetes manifest file
        .\kubectl apply -f azure-vote.yaml

        # Test the application
        .\kubectl get service azure-vote-front --watch

        # Delete the cluster
        Remove-AzResourceGroup -Name myResourceGroup
        ```
    - [Azure CLI](https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough)
        ```azurecli
        # Create a resource group
        az group create --name myResourceGroup --location eastus

        # Create AKS cluster
        az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 1 --enable-addons monitoring --generate-ssh-keys

        # Connect to the cluster
        az aks install-cli
        az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
        kubectl get nodes

        # Run the application - with a Kubernetes manifest file
        kubectl apply -f azure-vote.yaml

        # Test the application
        kubectl get service azure-vote-front --watch

        # Delete the cluster
        az group delete --name myResourceGroup --yes --no-wait
        ```
- create container images for solutions
    - [Azure CLI](https://docs.microsoft.com/en-us/azure/container-instances/container-instances-tutorial-prepare-app)
        ```azurecli
        # Build the container image - with a Dockerfile
        docker build ./aci-helloworld -t aci-tutorial-app

        # View the built images
        docker images

        # Run the container locally
        docker run -d -p 8080:80 aci-tutorial-app
        ```
- publish an image to the Azure Container Registry
    - [Azure CLI](https://docs.microsoft.com/en-us/azure/container-instances/container-instances-tutorial-prepare-acr)
        ```azurecli
        # Create a resource group
        az group create --name myResourceGroup --location eastus

        # Create Azure container registry
        az acr create --resource-group myResourceGroup --name <acrName> --sku Basic

        # Log in to container registry
        az acr login --name <acrName>

        # Show login server name
        az acr show --name <acrName> --query loginServer --output table

        # Tag container image
        docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1

        # Push image to Azure Container Registry
        docker push <acrLoginServer>/aci-tutorial-app:v1
        
        # List images in Azure Container Registry
        az acr repository list --name <acrName> --output table
        ```
- run containers by using Azure Container Instance or AKS
    - [Azure CLI](https://docs.microsoft.com/en-us/azure/container-instances/container-instances-tutorial-deploy-app)
        ```azurecli
        # Get registry credentials
        az acr show --name <acrName> --query loginServer

        # Deploy container
        az container create --resource-group myResourceGroup --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-login-server <acrLoginServer> --registry-username <service-principal-ID> --registry-password <service-principal-password> --dns-name-label <aciDnsLabel> --ports 80

        # Verify deployment progress
        az container show --resource-group myResourceGroup --name aci-tutorial-app --query instanceView.state

        # View the application
        az container show --resource-group myResourceGroup --name aci-tutorial-app --query ipAddress.fqdn

        # View the container logs
        az container logs --resource-group myResourceGroup --name aci-tutorial-app

        # Clean up resources
        az group delete --name myResourceGroup
        ```

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
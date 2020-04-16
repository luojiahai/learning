# Implement solutions that use virtual machines (VM)

## Provision VMs

### Concept

- [**What do I need to think about before creating a VM?**](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/overview#what-do-i-need-to-think-about-before-creating-a-vm)
    - The names of your application resources
    - The location where the resources are stored
    - The size of the VM
    - The maximum number of VMs that can be created
    - The operating system that the VM runs
    - The configuration of the VM after it starts
    - The related resources that the VM needs

- Azure Virtual Machine creation and management options
    - [**Azure portal**](https://azure.microsoft.com/en-us/features/azure-portal/)
    - [**Azure Resource Manager**](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/overview)
    - [**Azure PowerShell**](https://docs.microsoft.com/en-us/powershell/azure/)
    - [**Azure CLI** (Command Line Interface)](https://docs.microsoft.com/en-us/cli/azure/)
    - Programmactic (APIs)
        - [**Azure REST API**](https://docs.microsoft.com/en-us/rest/api/azure/)
        - [**Azure Client SDK**](https://github.com/Azure/azure-sdk)\\n    - [**Azure VM Extensions**](https://docs.microsoft.com/en-us/azure/virtual-machines/extensions/overview)
    - [**Azure Automation Services**](https://azure.microsoft.com/en-us/services/automation/)
    
- [**Availability**](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/availability) is the percentage of time a service is available for use.
    - An [**Availability Zone**](https://docs.microsoft.com/en-us/azure/availability-zones/az-overview) is a physically separate zone, within an Azure region. There are three Availability Zones per supported Azure region.
    - An [**availability set**](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/availability#availability-sets) is a logical feature used to ensure that a group of related VMs are deployed so that they aren't all subject to a single point of failure and not all upgraded at the same time during a host operating system upgrade in the datacenter.
    - A [**fault domain**](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/availability#fault-domains) is is a logical group of underlying hardware that share a common power source and network switch, similar to a rack within an on-premises datacenter.
    - An [**update domain**](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/availability#update-domains) is a logical group of underlying hardware that can undergo maintenance or be rebooted at the same time.

### Resource

- [Windows virtual machines in Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/)
- [Linux virtual machines in Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/)
- [Quickstart: Create a Linux virtual machine in the Azure portal](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal)
- [Quickstart: Create a Linux virtual machine in Azure with PowerShell](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-powershell)
- [Quickstart: Create a Linux virtual machine with the Azure CLI](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-cli)

----

## Create ARM templates

### Concept

- [**Resource Manager**](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/overview) provides a consistent management layer to perform tasks through Azure PowerShell, Azure CLI, Azure portal, REST API, and client SDKs.

- [**Terminology**](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/overview#terminology)
    - **resource** - A manageable item that is available through Azure. Virtual machines, storage accounts, web apps, databases, and virtual networks are examples of resources.
    - [**resource group**](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/overview#resource-groups) - A container that holds related resources for an Azure solution.
    - [**resource provider**](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/resource-providers-and-types) - A service that supplies Azure resources.
    - [**Resource Manager template**](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/overview) - A JavaScript Object Notation (JSON) file that defines one or more resources to deploy to a resource group or subscription.
    - [**declarative syntax**](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/overview) - Syntax that lets you state "Here is what I intend to create" without having to write the sequence of programming commands to create it.

### Resource

- [ARM template documentation](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/)
- [Quickstart: Create and deploy ARM templates by using the Azure portal](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/quickstart-create-templates-use-the-portal)
- [Quickstart: Create ARM templates by using Visual Studio Code](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/quickstart-create-templates-use-visual-studio-code)

----

## Configure Azure Disk Encryption for VMs

### Concept

- Encryption is about converting meaningful information into something that appears meaningless, such as a random sequence of letters and numbers.
    - **Symmetric encryption**
    - **Asymmetric encryption**
- Key management - In Azure, your encryption keys can be managed by Microsoft or the customer.
- The main encryption-based disk protection technologies for Azure VMs are:
    - [**Storage Service Encryption (SSE)**](https://docs.microsoft.com/en-us/azure/storage/common/storage-service-encryption)
    - **Azure Disk Encryption (ADE)** ([Linux](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/disk-encryption-overview), [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/disk-encryption-overview))

### Resource

- [Quickstart: Create and encrypt a virtual machine with the Azure portal](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/disk-encryption-portal-quickstart)
- [Quickstart: Create and encrypt a Linux VM in Azure with Azure PowerShell](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/disk-encryption-powershell-quickstart)
- [Quickstart: Create and encrypt a Linux VM with the Azure CLI](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/disk-encryption-cli-quickstart)

# Create containerized solutions

## Azure Kubernetes Service (AKS) overview

- [**Azure Kubernetes Service (AKS)**](https://docs.microsoft.com/en-us/azure/aks/intro-kubernetes) makes it simple to deploy a managed Kubernetes cluster in Azure. AKS reduces the complexity and operational overhead of managing Kubernetes by offloading much of that responsibility to Azure.

- You can create an AKS cluster in the Azure portal, with the Azure CLI, or template driven deployment options such as Resource Manager templates and Terraform.

## Create an Azure Managed Kubernetes Service (AKS) cluster

### Concept

- [**Kubernetes**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#what-is-kubernetes) is a rapidly evolving platform that manages container-based applications nad their associated networking and storage components.

- A [**Kubernetes cluster**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#kubernetes-cluster-architecture) is divided into two components:
    - [ **Control plane**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#control-plane) nodes provide the core Kubernetes services and orchestration of application workloads.
    - [**Nodes**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#nodes-and-node-pools) run your application workloads.

- [**Pods**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#pods) - Kubernetes uses *pods* to run an instance of your application. A pod represents a single instance of your application.

- [**Deployments and YAML manifests**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#deployments-and-yaml-manifests) - A *deployment* represents one or more identical pods, managed by the Kubernetes Deployment Controller.
    - [**Package management with Helm**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#package-management-with-helm)
    - [**StatefulSets and DaemonSets**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#statefulsets-and-daemonsets)
        - [**StatefulSets**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#statefulsets) - Maintain the state of applications beyond an individual pod lifecycle, such as storage.
        - [**DaemonSets**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#daemonsets) - Ensure a running instance on each node, early in the Kubernetes bootstrap process.

- [**Namespaces**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#namespaces) - Kubernetes resources, such as pods and Deployments, are logically grouped into a *namespace*.

### Resource

- [Access and identity options for Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/concepts-identity)
- [Security concepts for applications and clusters in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/concepts-security)
- [Network concepts for applications in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/concepts-network)
- [Storage options for applications in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/concepts-storage)
- [Scaling options for applications in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/concepts-scale)
- [Cluster operator and developer best practices to build and manage applications on Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/best-practices)

----

## Create container images for solutions

### Resource

- [Quickstart: Deploy an Azure Kubernetes Service cluster using the Azure CLI](https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough)
- [Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster using the Azure portal](https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough-portal)

----

## Publish an image to the Azure Container Registry

### Concept

- [**Azure Container Registry**](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-intro) is a managed, private Docker registry service based on the open-source Docker Registry 2.0. Create and maintain Azure container registries to store and manage your private Docker container images and related artifacts.

- [**Use cases**](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-intro#use-cases)
    - **Scalable orchestration systems** that manage containerized applications across clusters of hosts, including Kubernetes, DC/OS, and Docker Swarm.
    - **Azure services** that support building and running applications at scale, including Azure Kubernetes Service (AKS), App Service, Batch, Service Fabric, and others.

- **Key concepts**
    - **Registry** - Create one or more container registries in your Azure subscription.
    - **Repository** - A registry contains one or more repositories, which store groups of container images.
    - **Image** - Store in a repository, each image is a read-only snapshot of a Docker-compatible container.
    - **Container** - A container defines a software application and its dependencies wrapped in a complete filesystem including code, runtime, system tools, and libraries.

- [**Azure Container Registry Tasks (ACR Tasks)**](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-tasks-overview) is a suite of features within Azure Container Registry that provides streamlined and effient Docker container image builds in Azure.

### Resource

- [Quickstart: Create a private container registry using the Azure CLI](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-get-started-azure-cli)

----

## Run containers by using Azure Container Instance or AKS

### Concept

- Containers are becoming the preferred way to package, deploy, and manage cloud applications. [**Azure Container Instances**](https://docs.microsoft.com/en-us/azure/container-instances/container-instances-overview) offers the fastest and simplest way to run a container in Azure, without having to manage any virtual machines and without having to adopt a higher-level service.

### Resource

- [Tutorial: Create a container image for deployment to Azure Container Instances](https://docs.microsoft.com/en-us/azure/container-instances/container-instances-tutorial-prepare-app)
- [Tutorial: Deploy a container application to Azure Container Instances](https://docs.microsoft.com/en-us/azure/container-instances/container-instances-tutorial-deploy-app)

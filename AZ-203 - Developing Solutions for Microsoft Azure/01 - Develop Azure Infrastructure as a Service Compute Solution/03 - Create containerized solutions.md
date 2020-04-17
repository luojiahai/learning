# Create containerized solutions

## Create an [Azure Managed Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/) cluster

### Concept

- [**Kubernetes**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#what-is-kubernetes) is a rapidly evolving platform that manages container-based applications nad their associated networking and storage components.

- A [**Kubernetes cluster**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#kubernetes-cluster-architecture) is divided into two components:
    - **Control plane** nodes provide the core Kubernetes services and orchestration of application workloads.
    - **Nodes** run your application workloads.

- [**Control plane**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#control-plane) - When you create an AKS cluster, a control plane is automatically created and configured.
    - The control plane includes the following core Kubernetes components:
        - **kube-apiserver** - The API server is how the underlying Kubernetes APIs are exposed. This component provides the interaction for management tools, such as ```kubectl``` or the Kubernetes dashboard.
        - **etcd** - To maintain the state of your Kubernetes cluster and configuration, the highly available etcd is a key value store within Kubernetes.
        - **kube-scheuler** - When you create or scale applications, the Scheduler determines what nodes can run the workload and starts them.
        - **kube-controller-manager** - The Controller Manager oversees a number of smaller Controllers that perform actions such as replicating pods and handling node operations.

- [**Nodes and node pools**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#nodes-and-node-pools) - To run your applications and supporting services, you need a Kubernetes node. 
    - An AKS cluster has one or more nodes, which is an Azure virtual machine (VM) that runs the Kubernetes node components and container runtime:
        - The ```kubelet``` is the Kubernetes agent that processes the orchestration requests from the control plane and scheduling of running the requested containers.
        - Virtual networking is handled by the *kube-proxy* on each node. The proxy routes network traffic and manages IP addressing for services and pods.
        - The *container runtime* is the component that allows containerized applications to run and interact with additional resources such as the virtual network and storage. In AKS, Moby is used as the container runtime.
    - [**Resource reservations**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#resource-reservations) - Node resources are utilized by AKS to make the node function as part of your cluster.
    - [**Node pools**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#node-pools) - Nodes of the same configuration are grouped together into *node pools*.
    - [**Node selectors**](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#node-selectors) - In an AKS cluster that contains multiple node pools, you may need to tell the Kubernetes Scheduler which node pool to use for a given resource.

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

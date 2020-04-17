# Create Azure App Service Web Apps

## Create an Azure App Service Web App

### Concept

- [**Azure App Service**](https://docs.microsoft.com/en-us/azure/app-service/overview) is an HTTP-based service for hosting web applications, REST APIs, and mobile back ends. You can develop in your favorite language, be it .NET, .NET Core, Java, Ruby, Node.js, PHP, or Python. Applications run and scale with ease on both Windows and Linux-based environments.

- [**Why use App Service?**](https://docs.microsoft.com/en-us/azure/app-service/overview#why-use-app-service)
    - **Multiple languages and frameworks**
    - **DevOps optimization**
    - **Global scale with high availability**
    - **Connections to SaaS platforms and on-premises data**
    - **Security and compliance**
    - **Application templates**
    - **Visual Studio integration**
    - **API and mobile features**
    - **Serverless code**

- In App Service, an app runs in an [**App Service plan**](https://docs.microsoft.com/en-us/azure/app-service/overview-hosting-plans). An App Service plan defines a set of compute resources for a web app to run.
    - [**How does my app run and scale?**](https://docs.microsoft.com/en-us/azure/app-service/overview-hosting-plans#how-does-my-app-run-and-scale)
    - [**How much does my App Service plan cost?**](https://docs.microsoft.com/en-us/azure/app-service/overview-hosting-plans#how-much-does-my-app-service-plan-cost)
    - [**What if my app needs more capabilities or features?**](https://docs.microsoft.com/en-us/azure/app-service/overview-hosting-plans#what-if-my-app-needs-more-capabilities-or-features)
    - [**Should I put an app in a new plan or an existing plan?**](https://docs.microsoft.com/en-us/azure/app-service/overview-hosting-plans#should-i-put-an-app-in-a-new-plan-or-an-existing-plan)

- Azure App Service provides built-in [**authentication and authorization**](https://docs.microsoft.com/en-us/azure/app-service/overview-authentication-authorization) support, so you can sign in users and access data by writing minimal or no code in your web app, RESTful API, and mobile back end, and also [**Azure Functions**](https://docs.microsoft.com/en-us/azure/azure-functions/functions-overview).
    - [**How it works**](https://docs.microsoft.com/en-us/azure/app-service/overview-authentication-authorization#how-it-works)
    - [**Identity providers**](https://docs.microsoft.com/en-us/azure/app-service/overview-authentication-authorization#identity-providers)
    - [**Authentication flow**](https://docs.microsoft.com/en-us/azure/app-service/overview-authentication-authorization#authentication-flow)
    - [**Authorization behavior**](https://docs.microsoft.com/en-us/azure/app-service/overview-authentication-authorization#authorization-behavior)

- [**OS and runtime patching in Azure App Service**](https://docs.microsoft.com/en-us/azure/app-service/overview-patch-os-runtime) - App Service is a Platform-as-a-Service, which means that the OS and application stack are managed for you by Azure; you only manage your application and its data.
    - [**How and when are OS updates applied?**](https://docs.microsoft.com/en-us/azure/app-service/overview-patch-os-runtime#how-and-when-are-os-updates-applied)
    - [**How is App Service patched against significant vulnerabilities (such as zero-day)?**](https://docs.microsoft.com/en-us/azure/app-service/overview-patch-os-runtime#how-does-azure-deal-with-significant-vulnerabilities)
    - [**Which OS and runtime versions are running your apps?**](https://docs.microsoft.com/en-us/azure/app-service/overview-patch-os-runtime#when-are-supported-language-runtimes-updated-added-or-deprecated)

- [**Inbound and outbound IP addresses in Azure App Service**](https://docs.microsoft.com/en-us/azure/app-service/overview-inbound-outbound-ips) - Azure App Service is a multi-tenant service, except for App Service Environments. Apps that are not in an App Service environment (not in the Isolated tier) share network infrastructure with other apps. As a result, the inbound and outbound IP addresses of an app can be different, and can even change in certain situations.

- [**Hybrid Connections**](https://docs.microsoft.com/en-us/azure/app-service/app-service-hybrid-connections) is both a service in Azure and a feature in Azure App Service. As a service, it has uses and capabilities beyond those that are used in App Service.
    - [**How it works**](https://docs.microsoft.com/en-us/azure/app-service/app-service-hybrid-connections#how-it-works)

- [**Controlling Azure App Service traffic with Azure Traffic Manager**](https://docs.microsoft.com/en-us/azure/app-service/web-sites-traffic-manager) - You can use Azure Traffic Manager to control how requests from web clients are distributed to apps in Azure App Service.
    - [**Routing methods**](https://docs.microsoft.com/en-us/azure/app-service/web-sites-traffic-manager#routing-methods)
        - **Priority**
        - **Weighted**
        - **Performance**
        - **Geographic**
    - [**App Service and Traffic Manager Profiles**](https://docs.microsoft.com/en-us/azure/app-service/web-sites-traffic-manager#app-service-and-traffic-manager-profiles)

- [**Azure App Service Local Cache**](https://docs.microsoft.com/en-us/azure/app-service/overview-local-cache)
    - [**How the local cache changes the behavior of App Service**](https://docs.microsoft.com/en-us/azure/app-service/overview-local-cache#how-the-local-cache-changes-the-behavior-of-app-service)

- The [**Azure App Service Environment**](https://docs.microsoft.com/en-us/azure/app-service/environment/intro) is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.

### Resource

- [CLI samples for Azure App Service](https://docs.microsoft.com/en-us/azure/app-service/samples-cli)
- [PowerShell samples for Azure App Service](https://docs.microsoft.com/en-us/azure/app-service/samples-powershell)

----

## Create an Azure App Service background task by using WebJobs

### Concept

- [**WebJobs**](https://docs.microsoft.com/en-us/azure/app-service/webjobs-create#overview) is a feature of Azure App Service that enables you to run a program or script in the same context as a web app, API app, or mobile app.
    - [**WebJob types**](https://docs.microsoft.com/en-us/azure/app-service/webjobs-create#webjob-types): 
        - continuous
        - triggered
    - [**Supported file types for scripts or programs**](https://docs.microsoft.com/en-us/azure/app-service/webjobs-create#acceptablefiles)
        - .cmd, .bat, .exe (using Windows cmd)
        - .ps1 (using PowerShell)
        - .sh (using Bash)
        - .php (using PHP)
        - .py (using Python)
        - .js (using Node.js)
        - .jar (using Java)

### Resource

- [Create a continuous WebJob](https://docs.microsoft.com/en-us/azure/app-service/webjobs-create#CreateContinuous)
- [Create a manually triggered WebJob](https://docs.microsoft.com/en-us/azure/app-service/webjobs-create#CreateOnDemand)

----

## Enable diagnostics logging

### Concept

- [**Enable diagnostics logging for apps in Azure App Service**](https://docs.microsoft.com/en-us/azure/app-service/troubleshoot-diagnostic-logs) - Azure provides built-in diagnostics to assist with debugging an App Service app.

### Resource

- [Enable application logging (Windows)](https://docs.microsoft.com/en-us/azure/app-service/troubleshoot-diagnostic-logs#enable-application-logging-windows)
- [Enable application logging (Linux/Container)](https://docs.microsoft.com/en-us/azure/app-service/troubleshoot-diagnostic-logs#enable-application-logging-linuxcontainer)

----

## Create an Azure Web App for Containers

### Resource

- [Deploy a custom Linux container to Azure App Service](https://docs.microsoft.com/en-us/azure/app-service/containers/quickstart-docker)

----

## Monitor service health by using Azure Monitor

### Concept

- [**Azure Monitor**](https://docs.microsoft.com/en-us/azure/azure-monitor/overview) maximizes the availability and performance of your applications and services by delivering a comprehensive solution for collecting, analyzing, and acting on telemetry from your cloud and on-premises environments.

### Resource

- [Monitor Azure App Service performance](https://docs.microsoft.com/en-us/azure/azure-monitor/app/azure-web-apps)

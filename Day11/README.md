# Day 11/16 - Azure DevOps CICD Pipeline on Azure Kubernetes Services 🛳️ 🐳

Azure Kubernetes Service (AKS) offers the quickest way to start developing and deploying cloud-native apps in Azure, datacenters, or at the edge, with built-in code-to-cloud pipelines and guardrails. Azure handles critical tasks like health monitoring and maintenance as a hosted Kubernetes service.

## Kubernetes Architecture

The Kubernetes Architecture has mainly 2 components – the master node and the worker node.

<img width="1046" alt="K8s architecture ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/357c58c9-ccca-4522-b9a6-0671e0971892">

The master node machine components include the Kubernetes API server, Kubernetes scheduler, Kubernetes controller manager, etcd. Kubernetes worker node components include a container runtime engine or docker, a Kubelet service, and a Kubernetes proxy service.


## Kubernetes components

𝗠𝗮𝘀𝘁𝗲𝗿 𝗖𝗼𝗺𝗽𝗼𝗻𝗲𝗻𝘁𝘀:
1️⃣ API Server - Exposes the Kubernetes API.
2️⃣ Controller - Helps in maintaining the desired state of your cluster.
3️⃣ Scheduler - Schedules pods onto nodes.
4️⃣ etcd - Persistent storage which stores all cluster data.

𝗪𝗼𝗿𝗸𝗲𝗿 𝗖𝗼𝗺𝗽𝗼𝗻𝗲𝗻𝘁𝘀:
1️⃣ Kubelet - An agent that runs on each node in the cluster.
2️⃣ Kube Proxy - Takes care of Kubernetes networking.
3️⃣ Container Runtime - Responsible for running containers.

## Pre-requisites

### Infrastructure provisioning

**Using the below script, you can provision infra for this demo**

The following resources will be provisioned:

* Resource Group
* AKS Kubernetes Cluster
* Image container registry
* SQL Server
* SQL Database

``` bash

#!/bin/bash
REGION="westus"
RGP="day11-demo-rg"
CLUSTER_NAME="day11-demo-cluster"
ACR_NAME="day11demoacr"
SQLSERVER="day11-demo-sqlserver"
DB="mhcdb"


 #Create Resource group
 az group create --name $RGP --location $REGION

#Deploy AKS
az aks create --resource-group $RGP --name $CLUSTER_NAME --enable-addons monitoring --generate-ssh-keys --location $REGION

#Deploy ACR
az acr create --resource-group $RGP --name $ACR_NAME --sku Standard --location $REGION

#Authenticate with ACR to AKS
az aks update -n $CLUSTER_NAME -g $RGP --attach-acr $ACR_NAME

#Create SQL Server and DB
az sql server create -l $REGION -g $RGP -n $SQLSERVER -u sqladmin -p P2ssw0rd1234

az sql db create -g $RGP -s $SQLSERVER -n $DB --service-objective S0

```

## Change the Firewall settings of the SQL server

If you have the Allow Azure Services and resources to access this server setting enabled, this counts as a single firewall rule for the server. You can configure server-level IP firewall rules by using the Azure portal.

<img width="921" alt="Firewall setting ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/2fa9fda1-f4de-40aa-99c1-cc84fff73dbd">

## Setup Azure DevOps Project

### Pre-requisites

Make sure the below Azure DevOps extensions are installed and enabled in your organization
- Replace Token
- Kubernetes extension

Replace Tokens is an extension that can be used in Azure DevOps to replace tokens in the code files with variable values (which can be configured in the Pipelines Library) during the execution of the CI/CD process.

Quarkus can automatically generate Kubernetes resources based on sane defaults and user-supplied configuration using dekorate. It currently supports generating resources for vanilla Kubernetes, OpenShift, and Knative.

Once the infra is ready, go to dev.azure.com --> Project --> repos 
and import the below git repo, which has the source code and pipeline code

https://github.com/Ibrahimsi/MyHealthClinic-AKS.git

### Build and Release Pipeline

- You can create your pipeline by following along with the editing of the existing pipeline. The below details need to be updated in the pipeline:
   - Azure Service connection
   - Token pattern
   - Pipeline variables
   - The Kubectl version should be the latest in the release pipeline
   - Secrets should be updated in the deployment step
   - ACR details in the pipeline should be updated
 
 **Azure Pipeline Code**

 ```
# Starter pipeline
# Start with a minimal pipeline that you can customize to build and deploy your code.
# Add steps that build, run tests, deploy, and more:
# https://aka.ms/yaml

trigger:
- main

pool:
  vmImage: ubuntu-latest

steps:
- task: replacetokens@4
  displayName: 'Replace tokens in appsettings.json'
  inputs:
    rootDirectory: '$(build.sourcesdirectory)/src/MyHealth.Web'
    targetFiles: 'appsettings.json'
    encoding: 'auto'
    tokenPattern: 'rm'
    writeBOM: true
    escapeType: 'none'
    actionOnMissing: 'warn'
    keepToken: false
    actionOnNoFiles: 'continue'
    enableTransforms: false
    enableRecursion: false
    useLegacyPattern: false
    enableTelemetry: true

- task: replacetokens@3
  displayName: 'Replace tokens in mhc-aks.yaml'
  inputs:
    targetFiles: 'mhc-aks.yaml'
    escapeType: none
    tokenPrefix: '__'
    tokenSuffix: '__'

- task: DockerCompose@0
  displayName: 'Run services'
  inputs:
    containerregistrytype: 'Azure Container Registry'
    azureSubscription: 'Pay-As-You-Go(1)(f30deb63-a417-4fa4-afc1-813a7d3920bb)'
    azureContainerRegistry: '{"loginServer":"day11demoacrs.azurecr.io", "id" : "/subscriptions/f30deb63-a417-4fa4-afc1-813a7d3920bb/resourceGroups/day11-demo-rg/providers/Microsoft.ContainerRegistry/registries/day11demoacrs"}'
    dockerComposeFile: 'docker-compose.ci.build.yml'
    action: 'Run services'
    detached: false

- task: DockerCompose@0
  displayName: 'Build services'
  inputs:
    containerregistrytype: 'Azure Container Registry'
    azureSubscription: 'Pay-As-You-Go(2)(f30deb63-a417-4fa4-afc1-813a7d3920bb)'
    azureContainerRegistry: '{"loginServer":"day11demoacrs.azurecr.io", "id" : "/subscriptions/f30deb63-a417-4fa4-afc1-813a7d3920bb/resourceGroups/day11-demo-rg/providers/Microsoft.ContainerRegistry/registries/day11demoacrs"}'
    dockerComposeFile: 'docker-compose.yml'
    dockerComposeFileArgs: 'DOCKER_BUILD_SOURCE='
    action: 'Build services'
    additionalImageTags: '$(Build.BuildId)'

- task: DockerCompose@0
  displayName: 'Push services'
  inputs:
    containerregistrytype: 'Azure Container Registry'
    azureSubscription: 'Pay-As-You-Go(1)(f30deb63-a417-4fa4-afc1-813a7d3920bb)'
    azureContainerRegistry: '{"loginServer":"day11demoacrs.azurecr.io", "id" : "/subscriptions/f30deb63-a417-4fa4-afc1-813a7d3920bb/resourceGroups/day11-demo-rg/providers/Microsoft.ContainerRegistry/registries/day11demoacrs"}'
    dockerComposeFile: 'docker-compose.yml'
    dockerComposeFileArgs: 'DOCKER_BUILD_SOURCE='
    action: 'Push services'
    additionalImageTags: '$(Build.BuildId)'

- task: DockerCompose@0
  displayName: 'Lock services'
  inputs:
    containerregistrytype: 'Azure Container Registry'
    azureSubscription: 'Pay-As-You-Go(1)(f30deb63-a417-4fa4-afc1-813a7d3920bb)'
    azureContainerRegistry: '{"loginServer":"day11demoacrs.azurecr.io", "id" : "/subscriptions/f30deb63-a417-4fa4-afc1-813a7d3920bb/resourceGroups/day11-demo-rg/providers/Microsoft.ContainerRegistry/registries/day11demoacrs"}'
    dockerComposeFile: 'docker-compose.yml'
    dockerComposeFileArgs: 'DOCKER_BUILD_SOURCE='
    action: 'Lock services'
    outputDockerComposeFile: '$(Build.StagingDirectory)/docker-compose.yml'

- task: CopyFiles@2
  displayName: 'Copy Files'
  inputs:
    Contents: |
     **/mhc-aks.yaml
     **/*.dacpac
     
    TargetFolder: '$(Build.ArtifactStagingDirectory)'

- task: PublishBuildArtifacts@1
  displayName: 'Publish Artifact'
  inputs:
    ArtifactName: deploy
```
 
#### Steps in the pipeline

<img width="805" alt="Steps pipeline ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/62893f0e-4cd2-4c57-bd11-d04b949b9589">

Azure DevOps provides integration with popular open-source and third-party tools and services—across the entire DevOps workflow.

 **https://azuredevopslabs.com/labs/vstsextend/kubernetes/**

## Destroy the resources 

```
#!/bin/bash


# Set environment variables
REGION="westus"
RGP="day11-demo-rg"
CLUSTER_NAME="day11-demo-cluster"
ACR_NAME="day11demoacr"
SQLSERVER="day11-demo-sqlserver"
DB="mhcdb"

# Function to handle errors
handle_error() {
    echo "Error: $1"
    exit 1
}

# Function to check if the resource exists
resource_exists() {
    az resource show --ids $1 &> /dev/null
}

# Delete Azure Kubernetes Service (AKS)
if resource_exists $(az aks show --resource-group $RGP --name $CLUSTER_NAME --query id --output tsv); then
    az aks delete --resource-group $RGP --name $CLUSTER_NAME || handle_error "Failed to delete AKS."
else
    echo "AKS not found. Skipping deletion."
fi

# Delete Azure Container Registry (ACR)
if resource_exists $(az acr show --name $ACR_NAME --resource-group $RGP --query id --output tsv); then
    az acr delete --name $ACR_NAME --resource-group $RGP || handle_error "Failed to delete ACR."
else
    echo "ACR not found. Skipping deletion."
fi

# Delete SQL Database
if resource_exists $(az sql db show --resource-group $RGP --server $SQLSERVER --name $DB --query id --output tsv); then
    az sql db delete --resource-group $RGP --server $SQLSERVER --name $DB || handle_error "Failed to delete SQL Database."
else
    echo "SQL Database not found. Skipping deletion."
fi

# Delete SQL Server
if resource_exists $(az sql server show --resource-group $RGP --name $SQLSERVER --query id --output tsv); then
    az sql server delete --resource-group $RGP --name $SQLSERVER || handle_error "Failed to delete SQL Server."
else
    echo "SQL Server not found. Skipping deletion."
fi

# Delete Resource Group
if resource_exists $(az group show --name $RGP --query id --output tsv); then
    az group delete --name $RGP || handle_error "Failed to delete Resource Group."
else
    echo "Resource Group not found. Skipping deletion."
fi

echo "Resources successfully deleted."

```

## Hands-On 🗂️ - Day-11 (Three Tier Architecture CI CD On Kubernetes — Azure DevOps)  ✅

👉 https://medium.com/@ibrahims/three-tier-architecture-ci-cd-on-kubernetes-azure-devops-bf558c16ea07 👈

<img width="921" alt="Health clinic ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/3b7a1d61-4ac4-4196-9297-48583393d873">

If you are doing a project on Hands-on follow the above blog it would be more helpful.

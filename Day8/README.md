# Day 8/16 - Azure DevOps with Terraform 🏗

Terraform is built into Azure Cloud Shell and authenticated to your subscription, so it's integrated and ready to go.

Terraform is an IAC tool, used primarily by DevOps teams to automate various infrastructure tasks. The provisioning of cloud resources, for instance, is one of the main use cases of Terraform. It's a cloud-agnostic, open-source provisioning tool written in the Go language and created by HashiCorp.

Why Terraform?

1) Free of cost
2) The manual tasks are error-prone and inconsistent
3) Multiple platform support
4) Easy to write (JSON based)
5) Easy integration with configuration management tool (Ansible).

## How Terraform works

Terraform is the IAAS(Infrastructure as the service) tool. It is used to automate the infra provision on the various cloud providers (more than 75). It has become the industry standard for IAAC.

![Azure terraform how it works ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/4961519b-9a4f-4ccf-a30f-52f6be92716b)

Terraform can be thought of as consisting of two main parts: **Terraform Core** and **Plugins**. A core is responsible for the life cycle management of infrastructure. It is the open-source binary that you download and use from the command line. 

Terraform Plugins provide a mechanism for Terraform Core to communicate with your infrastructure host or SaaS providers. Terraform Providers and Provisioners are examples of plugins as mentioned above. Terraform Core communicates with the plugins via Remote Procedure Call (RPC).


## Initialize the Terraform repo

Terraform init" again to reinitialize your working directory. Terraform Cloud has been successfully initialized! You may now begin working with Terraform Cloud.

**terraform init**

<img width="675" alt="tf init ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/469312c2-05a6-424f-9915-70fa2430860d">


## Run Terraform plan

**terraform plan**

The Terraform plan command creates an execution plan, which lets you preview the changes that Terraform plans to make to your infrastructure.

When Terraform creates a plan it → Reads the current state of any already-existing remote objects to make sure that the Terraform state is up-to-date.

<img width="923" alt="tf paln ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/c383363a-b238-4b63-8536-d93c616e9402">


## Run Terraform apply

**terraform apply**

<img width="923" alt="tf apply ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/0daa2693-051b-4751-9588-2a2988dbd72b">

The terraform apply command executes the actions proposed in a terraform plan. It is used to deploy your infrastructure. Typically apply should be run after terraform init and terraform plan.

### Import the below repository into Azure DevOps for Terraform configuration

https://github.com/Ibrahimsi/Terraform-AzureDevOps-Sample.git

## Let's implement this using Azure DevOps

![Implement tf ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/c7f1c6cd-3b7b-4143-947f-d4e861d3e49c)

Terraform is a tool for building, changing, and versioning infrastructure safely and efficiently. Terraform can manage existing and popular cloud service providers as well as custom in-house solutions.

Configuration files describe to Terraform the components needed to run a single application or your entire data center. 

Terraform generates an execution plan describing what it will do to reach the desired state and then executes it to build the described infrastructure. As the configuration changes, Terraform is able to determine what changed and create incremental execution plans that can be applied.

### You can use the below Azure CLI commands to set the terraform remote backend, or you can do it via the portal

``` shell
#!/bin/bash
## The Storage account name must be unique, and the values below should match your backend.tf
RESOURCE_GROUP_NAME=demo-rg
STORAGE_ACCOUNT_NAME=ibrahimsi
CONTAINER_NAME=prod-tfstate

# Create resource group
az group create --name $RESOURCE_GROUP_NAME --location West Europe

# Create storage account
az storage account create --resource-group $RESOURCE_GROUP_NAME --name $STORAGE_ACCOUNT_NAME --sku Standard_LRS --encryption-services blob

# Create blob container
az storage container create --name $CONTAINER_NAME --account-name $STORAGE_ACCOUNT_NAME
```

## Azure DevOps CICD Pipeline

Azure CI/CD refers to the practice of Continuous Integration and Continuous Deployment, which are key components of the software development lifecycle. 

CI/CD helps automate and streamline the process of building, testing, and deploying applications, resulting in faster and more reliable software releases.

<img width="1143" alt="CI:CD Pipeline ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/af7ee52c-309e-454b-b17c-2c50000cb73f">

## YAML Code for Build Pipeline

``` YAML
trigger: 
- main

stages:
- stage: Build
  jobs:
  - job: Build
    pool:
      vmImage: 'ubuntu-latest'
    steps:
    - task: TerraformTaskV4@4
      displayName: Tf init
      inputs:
        provider: 'azurerm'
        command: 'init'
        backendServiceArm: 'Pay-As-You-Go(f30deb63-a417-4fa4-afc1-813a7d3920bb)'
        backendAzureRmResourceGroupName: 'demo-resources'
        backendAzureRmStorageAccountName: 'ibrahimsi'
        backendAzureRmContainerName: 'prod-tfstate'
        backendAzureRmKey: 'prod.terraform.tfstate'
    - task: TerraformTaskV4@4
      displayName: Tf validate
      inputs:
        provider: 'azurerm'
        command: 'validate'
    - task: TerraformTaskV4@4
      displayName: Tf fmt
      inputs:
        provider: 'azurerm'
        command: 'custom'
        customCommand: 'fmt'
        outputTo: 'console'
        environmentServiceNameAzureRM: 'Pay-As-You-Go(f30deb63-a417-4fa4-afc1-813a7d3920bb)'
      
    - task: TerraformTaskV4@4
      displayName: Tf plan
      inputs:
        provider: 'azurerm'
        command: 'plan'
        commandOptions: '-out $(Build.SourcesDirectory)/tfplanfile'
        environmentServiceNameAzureRM: 'Pay-As-You-Go(f30deb63-a417-4fa4-afc1-813a7d3920bb)'
      
    - task: ArchiveFiles@2
      displayName: Archive files
      inputs:
        rootFolderOrFile: '$(Build.SourcesDirectory)/'
        includeRootFolder: false
        archiveType: 'zip'
        archiveFile: '$(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip'
        replaceExistingArchive: true
    - task: PublishBuildArtifacts@1
      inputs:
        PathtoPublish: '$(Build.ArtifactStagingDirectory)'
        ArtifactName: '$(Build.BuildId)-build'
        publishLocation: 'Container'
```

## Release Pipeline

A Release Pipeline consumes the Artifacts and conducts follow-up actions within a multi-staging system.

<img width="913" alt="Release pipeline new ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/f442b661-f8fb-4b47-b39b-6c759772461a">

Variables give you a convenient way to get key bits of data into various parts of the pipeline. The most common use of variables is to define a value that you can then use in your pipeline. All variables are strings and are mutable.

![Variable ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/f8832bd3-6453-491a-9c08-88d29961c562)

### Deployment stage

The deployment phase is the final phase of the software development life cycle (SDLC) and puts the product into production. After the project team tests the product and the product passes each testing phase, the product is ready to go live.

![Deployment stage ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/be2f00ac-316f-444a-ae8a-5de55c784a58)

1) Pre-deploy
2) Deploy
3) Post-deploy

During the Pre-Deploy testing phase, both the development team and the QA engineer should be tasked with the following items --> Ask developers to make Production and Stage environment backups.

### Destroy stage

The destroy stage of the data life cycle might involve which of the following actions? The removal of all copies of a data item from an organization is known as data destruction or purging. Usually, it is carried out from a storage facility for archives.

![Destroy ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/e8238949-efc3-4907-9b30-ab5f5fc5ccb1)

Destroy → Removal of every copy of a data item from an organization.

<img width="898" alt="Destroy 1 ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/de447c9d-e5d2-43b3-b560-d43bfbd01b19">

### Hands-On 🗂️ - Day-8 (Azure Terraform Pipeline — DevOps)  ✅

👉 https://medium.com/@ibrahims/azure-terraform-pipeline-devops-b57005a37936 👈

<img width="913" alt="LAst add ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/095aa4da-089b-4283-96f7-8113ad4544e9">

If you are doing a project on Hands-on follow the above blog it would be more helpful.


# Day 13/16 - Azure Functions CI CD With Azure DevOps | What is Azure Function 🚀

Azure Functions is an event-driven, serverless computing platform that helps you develop more efficiently using the programming language of your choice. 

## To publish the Azure function from your CLI to Azure, follow the instructions given in the below repo:

```bash
https://github.com/rishabkumar7/azure-qr-code
```

## Azure DevOps CI/CD Process diagram:

![Day 13 ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/70288380-ef53-4e3b-ac1d-866e449c19bc)

Azure subscription is a logical container used to provision related business or technical resources in Azure. It holds the details of all your resources like virtual machines (VMs), databases, and more. When you create an Azure resource like a VM, you identify the subscription it belongs to.

Azure Pipelines automatically builds and tests code projects. It supports all major languages and project types and combines continuous integration, continuous delivery, and continuous testing to build, test, and deliver your code to any destination.

Azure Artifacts enables developers to efficiently manage all their dependencies from one place. With Azure Artifacts, developers can publish packages to their feeds and share them within their team, across organizations, and even publicly across the internet.

## Prerequisites
1. Node.js (or) brew install node
2. Azure Functions Core Tools
3. Azure CLI
4. An Azure account and an Azure Blob Storage account.

## Azure DevOps pipeline code:

```YAML
# # Node.js Function App to Linux on Azure
# Build a Node.js function app and deploy it to Azure as a Linux function app.
# Add steps that analyze code, save build artifacts, deploy, and more:
# https://docs.microsoft.com/azure/devops/pipelines/languages/javascript

trigger:
- iac-implementation

variables:

  # Azure Resource Manager connection created during pipeline creation
  azureSubscription: '37035b62-6584-46fa-83fe-a8b418991be4'

  # Function app name
  functionAppName: 'ibrahims'

  # Environment name
  environmentName: 'ibrahims'
  system.debug: true

  # Agent VM image name
  vmImageName: 'ubuntu-latest'

stages:
- stage: Build
  displayName: Build stage
  jobs:
  - job: Build
    displayName: Build
    pool:
      vmImage: $(vmImageName)

    steps:
    - task: NodeTool@0
      inputs:
        versionSpec: '18.x'
      displayName: 'Install Node.js'

    - script: |
        cd qrCodeGenerator
        npm install
        npm run build --if-present
        npm run test --if-present
      displayName: 'Prepare binaries'

    - task: CopyFiles@2
      inputs:
        SourceFolder: '$(System.DefaultWorkingDirectory)/qrCodeGenerator/GenerateQRCode/'
        Contents: '**'
        TargetFolder: '$(System.DefaultWorkingDirectory)/qrCodeGenerator/'
    - task: ArchiveFiles@2
      displayName: 'Archive files'
      inputs:
        rootFolderOrFile: '$(System.DefaultWorkingDirectory)/qrCodeGenerator/'
        includeRootFolder: false
        archiveType: zip
        archiveFile: $(Build.ArtifactStagingDirectory)/qrCodeGenerator/$(Build.BuildId).zip
        replaceExistingArchive: true

    - upload: $(Build.ArtifactStagingDirectory)/qrCodeGenerator/$(Build.BuildId).zip
      artifact: drop

- stage: Deploy
  displayName: Deploy stage
  dependsOn: Build
  condition: succeeded()
  jobs:
  - deployment: Deploy
    displayName: Deploy
    environment: $(environmentName)
    pool:
      vmImage: $(vmImageName)
    strategy:
      runOnce:
        deploy:
          steps:
          - task: AzureFunctionApp@2
            inputs:
              connectedServiceNameARM: 'Pay-As-You-Go (f30deb63-a417-4fa4-afc1-813a7d3920bb)'
              appType: 'functionApp'
              appName: 'ibrahims'
              package: '$(Pipeline.Workspace)/drop/$(Build.BuildID).zip'
              deploymentMethod: 'zipDeploy'
```

## Hands-On 🗂️ - Day-13 (Azure Functions CI CD — DevOps)  ✅

👉 https://medium.com/@ibrahims/azure-functions-ci-cd-devops-b6770ec8417f 👈

<img width="921" alt="QR code ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/60cf4050-70b6-4737-b4ff-04c686d33a95">

If you are doing a project on Hands-on follow the above blog it would be more helpful.

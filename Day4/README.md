
# 🚀 Azure DevOps Build Pipeline - Build and Deploy a YouTube Clone 

Azure Pipelines automatically builds and tests code projects. It supports all major languages and project types and combines continuous integration, continuous delivery, and continuous testing to build, test, and deliver your code to any destination.

## Steps 
- Login to VSCode (or) any other IDE of your choice (https://vscode.dev)
- Run the below commands to download the application code
  ```
  mkdir day4_youtube_clone; cd day4_youtube_clone
  git init
  git clone https://github.com/Ibrahimsi/Youtube_clone.git
  ```
- Create a project in Azure DevOps for Day4 and push the code by running the below commands on VSCode:
  ```
  git remote add origin $YOURAZUREREPO
  git push -u origin all
  ```
  **Note:** Make sure to update your Azure repo in the above command

- Go to the Azure Portal and Create the Azure App Service

Azure App Service enables you to build and host web apps, mobile backends, and RESTful APIs in the programming language of your choice without managing infrastructure.  

- Implement the build pipeline using the classic editor

The classic editor is a WordPress content editor that was previously used to create, edit, and format posts and pages.

- Understand the use of service connection and service 

Service Connection” is a configuration that securely stores information required to connect and authenticate to external services or resources, such as cloud providers, container registries, version control systems, and more.

![Service connection ibbus 4](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/1698713d-d512-4a75-8263-2276b19ee637)

**Note: You must set the app settings WEBSITE_DYNAMIC_CACHE=0 and WEBSITE_LOCAL_CACHE_OPTION=Never to disable all file caching**


## Structure of Azure DevOps build Pipeline

The DevOps pipeline typically has eight stages. In the Development phase, they are: 
Plan, Code, Build, and Test.

Operations phase, the stages are: Release, Deploy, Operate, and Monitor.

<img width="586" alt="Structure of devops pipeline ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/666d7f8d-bfc2-4058-974f-2fcbbe2fadce">

*  A trigger tells a Pipeline to run. It could be CI or Scheduled, manual(if not specified), or after another build finishes.
*  A pipeline is made up of one or more stages. A pipeline can deploy to one or more environments.
*  A stage organizes jobs in a pipeline, and each stage can have one or more jobs.
*  Each job runs on one agent, such as Ubuntu, Windows, macOS, etc. A job can also be agentless.
*  Each agent runs a job that contains one or more steps.
*  A step can be a task or script and is the smallest building block of a pipeline.
*  A task is a pre-packaged script that acts, such as invoking a REST API or publishing a build artifact.
*  An artifact is a collection of files or packages published by a run.

![Azure pipeline ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/84a2d632-2abe-44aa-946b-c89249d53dde)

## Pipeline code used in the demo

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
    - task: Npm@1
      inputs:
        command: 'install'
    - task: Npm@1
      inputs:
        command: 'custom'
        customCommand: 'run build'

    
    - task: PublishBuildArtifacts@1
      inputs:
        PathtoPublish: 'build'
        ArtifactName: 'drop'
        publishLocation: 'Container'

- stage: Deploy 
  jobs:
  - job: Deploy
    pool:
      vmImage: 'ubuntu-latest'
    steps:
    - task: DownloadBuildArtifacts@1
      inputs:
        buildType: 'current'
        downloadType: 'single'
        artifactName: 'drop'
        downloadPath: '$(System.ArtifactsDirectory)'
    - task: AzureRmWebAppDeployment@4
      inputs:
        ConnectionType: 'AzureRM'
        azureSubscription: 'f2d858b2-0b52-4d8e-a750-adae9358c49a'
        appType: 'webAppLinux'
        WebAppName: 'ibrahimsi'
        packageForLinux: '$(System.ArtifactsDirectory)/drop'
        RuntimeStack: 'STATICSITE|1.0'
```
## Hands-On 🗂️ - Day-4 (Azure Pipeline — DevOps)  ✅

👉 https://medium.com/@ibrahims/azure-pipeline-devops-b6fe8d8505ba 👈

<img width="919" alt="youtube final ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/67730b91-b809-4ec2-a522-723f8f6c8930">

If you are doing a project on Hands-on follow the above blog it would be more helpful.


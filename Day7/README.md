# Day 7 - Azure Artifacts 👨‍💻

Azure Artifacts is an extension for Azure DevOps that can host NuGet and npm packages and organize them in feeds.

## Setup your Azure repos with the same application code

Import the below repository to clone the Nike landing page sample website code to your Azure Repos:

https://github.com/Ibrahimsi/nike_landing_page.git

**Note:** You must set the app settings as below to disable all file caching:

Caching is the process of storing copies of files in a cache, or temporary storage location so that they can be accessed more quickly.

*  WEBSITE_DYNAMIC_CACHE=0
*  WEBSITE_LOCAL_CACHE_OPTION=Never

These settings are about your Azure Web App files. They decide where the files are written and read from your web apps.

<img width="913" alt="Cache ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/52eccdc0-c18b-439f-9ff4-ecf6249f2089">

## Architectural diagram 

A build pipeline contains the stages that define the build process for successfully compiling, testing, and running software applications before deployment. 

A Release Pipeline consumes the Artifacts and conducts follow-up actions within a multi-staging system.

Azure Artifacts enables developers to efficiently manage all their dependencies from one place. With Azure Artifacts, developers can publish packages to their feeds and share them within their team, across organizations, and even publicly across the internet.

Triggers are events on which you can start your pipeline run automatically. You can enable triggers on your pipeline by subscribing to both internal and external events.

![ibbus Day 7](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/8d67a8be-90dc-45f7-8a43-9b72f21a5151)

Azure App Service enables you to build and host web apps, mobile backends, and RESTful APIs in the programming language of your choice without managing infrastructure.

## NPM Pipeline YAML code:

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
        command: 'custom'
        customCommand: 'install -D tailwindcss postcss autoprefixer'
    - task: Npm@1
      inputs:
        command: 'custom'
        customCommand: 'run build'
    - task: Npm@1
      inputs:
        command: 'publish'
        workingDir: './dist'
        publishRegistry: 'useFeed'
        publishFeed: '515a2edb-27f5-416f-88c0-0c50138edec1/336630b1-903f-4ae3-88c6-69149d01550e'
```



### Post-deployment inline script in the Release pipeline

A script runs code as a step in your pipeline using command line.

```
cp -rf /home/site/wwwroot/package/* /home/site/wwwroot/
```

## Hands-On 🗂️ - Day-7 (Azure Artifacts- DevOps)  ✅

👉 https://medium.com/@ibrahims/azure-artifacts-devops-6298adae0ce5 👈

<img width="920" alt="Nike ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/baf5a0d7-92cc-4a58-939c-a5288a06b3ef">

If you are doing a project on Hands-on follow the above blog it would be more helpful.

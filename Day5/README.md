# 🚀 Azure DevOps Release Pipeline - Continous Delivery of a YouTube Clone Website

Azure Pipelines provide a highly configurable and manageable pipeline for releases to multiple stages such as development, staging, QA, and production.

<img width="912" alt="ibbus 1 clone" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/61eeeebb-7f48-4287-876b-69770b7ee5e6">

## Blue Green Deployments

- 𝐁𝐥𝐮𝐞-𝐆𝐫𝐞𝐞𝐧 - In this deployment method, two identical production environments work in parallel.
- One is the currently running production environment. It receives all user traffic (𝐁𝐥𝐮𝐞).
- The other environment is a clone of it, but idle (𝐆𝐫𝐞𝐞𝐧). Both use the app configuration.

✔ The new version of the application is deployed in the 𝐠𝐫𝐞𝐞𝐧 environment and tested for functionality and performance. Once the testing results are successful, application traffic is routed from 𝐛𝐥𝐮𝐞 to 𝐠𝐫𝐞𝐞𝐧. Then 𝐆𝐫𝐞𝐞𝐧 becomes the new production.

✔ Blue-Green deployment means to have two identical environments at a given time, one of which is active (blue), and the other idle (green). 

✔ The updates are pushed to an idle environment and are tested. Then traffic is switched to an idle environment (green). 

✔ Hence idle (green then) becomes active(blue now) now and the previously active (blue then) becomes idle (green now).

✔ If things go wrong (even after thorough testing!) then traffic is switched back to the previously active environment.

![Blue green deployment ibbus 1](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/fcc56ec0-9ec1-480d-a02b-83453433a938)

## End-to-End CICD Pipeline using Azure DevOps Build and Release Pipeline

A Build Pipeline is used to generate Artifacts out of Source Code. A Release Pipeline consumes the Artifacts and conducts follow-up actions within a multi-staging system.

![CI?CD NPM ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/f9a67033-3990-441e-bcf4-5739c318617e)

## Pipeline code used in the demo

```
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
```
## Hands-On 🗂️ - Day-5 (Azure Release Pipelines-DevOps)  ✅

👉 https://medium.com/@ibrahims/azure-release-pipelines-devops-c23bd4c43066 👈

<img width="919" alt="Youtube final ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/ad78b0eb-522a-479f-9e89-52f5df503e1f">

If you are doing a project on Hands-on follow the above blog it would be more helpful.

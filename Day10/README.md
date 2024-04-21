# Day 10/16 - Azure DevOps CICD Pipeline on Azure Container Instances 🐳

Azure Container Instances (ACI) is a service that enables a developer to deploy containers on the Microsoft Azure public cloud without having to provision or manage any underlying infrastructure. 

## Understanding Virtual machine V/s Containers.

Containers virtualize the operating system, allowing multiple isolated user-space instances to run on a single OS kernel. Containers package an application and its dependencies into a single unit that can be easily deployed across different environments.

Virtual Machines virtualize the hardware layer, allowing multiple operating systems to run on a single physical machine. Each VM includes a complete OS, along with the application and its dependencies.

![Container differ ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/a0db526a-a1d6-4e75-bad3-477ef17b2a02)

## Challenges with the non-containerized applications

1) Complexity
2) Security
3) Persistent Storage
4) Networking
5) Monitoring and Debugging

## Docker Architecture

The Docker architecture defines all the components, such as the docker daemon, the docker client, (or) the docker registries, and their interconnections upon which Docker is built. Scrolling down you will learn how it actually looks and works inside Docker and the different components that make use of it.

![Docker Architecture ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/9553f09e-9222-4551-a88e-559cf5627a03)

## Containerize a sample To-Do list web app written in React JS.

To-do lists help you organize your work and keep track of tasks. A good digital to-do list makes it easier to get work done—and makes it harder to miss deadlines.

**GitHub repo for the App:**
https://github.com/Ibrahimsi/todoapp-docker.git

**DockerFile**

A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image.

```
FROM node:18-alpine AS installer
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
FROM nginx:latest AS deployer
COPY --from=installer /app/build /usr/share/nginx/html
```

## Benefits of a multi-stage docker file

Multi-stage build means the resulting container will be more secure because your final image includes only what it needs to run the application. Faster deployment. 

<img width="913" alt="Multi stage ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/4358bb6b-5d62-42b3-9c26-ab6db964280d">

Smaller images mean less time to transfer or quicker CI/CD builds, faster deployment time, and improved performance.

**Efficient Use of Layers:**
Docker layers play a pivotal role in image-building efficiency. By strategically placing instructions in your Dockerfile and optimizing your image creation process you can reduce build times and enhance resource utilization.

**Security:**
Docker containers are, by default, quite secure; especially if you run your processes as non-privileged users inside the container. You can add an extra layer of safety.

Container security is knowing that a container image you run in your environment includes only the libraries, base image, and any custom bits you declare in your Dockerfile,  and not malware or known vulnerabilities. 

**Build Isolation and Clarity:**
Isolation provides an additional layer of security to prevent malicious workloads running in containers from compromising the Docker Desktop or the host.

**Faster Builds:**
Docker builds is by using the power of Docker layer caching. It is a feature that allows you to cache intermediate build layers, reducing the need to rebuild them from scratch every time you make changes to your code.

**Optimized for Production:**
Consolidate Dockerfile instructions to reduce layer count. Trim any unnecessary files or packages from your image. Utilize Docker's built-in build cache.

**Docker Scout:**
Docker Scout gives you the list of discovered vulnerabilities in your container images and offers guidance for remediation in an iterative small-improvement style. 

You can compare your scores from one deployment to the next and show improvement to create a sense of accomplishment for your teams, not an overwhelming bombardment of vulnerabilities and risks that seem insurmountable.

## What are Azure container instances(ACI)

Azure Container Instances is a solution for any scenario that can operate in isolated containers, without orchestration. Run event-driven applications, quickly deploy from your container development pipelines, and run data processing and build jobs.

![Azure container instances ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/22405602-9e46-482e-a159-d5e671db3135)

## Azure DevOps CICD Pipeline to deploy to ACI

**Pipeline Code**:

``` YAML
# Docker
# Build and push an image to Azure Container Registry
# https://docs.microsoft.com/azure/devops/pipelines/languages/docker

trigger:
- main

resources:
- repo: self

variables:
  # Container registry service connection established during pipeline creation
  dockerRegistryServiceConnection: 'ce86373d-4d75-4b34-b778-d5b8eb8dd4b0'
  imageRepository: 'todoapp'
  containerRegistry: 'ibrahims.azurecr.io'
  dockerfilePath: '$(Build.SourcesDirectory)/Dockerfile'
  tag: '$(Build.BuildId)'

  # Agent VM image name
  vmImageName: 'ubuntu-latest'

stages:
- stage: Build
  displayName: Build and push stage
  jobs:
  - job: Build
    displayName: Build
    pool:
      vmImage: $(vmImageName)
    steps:
    - task: AzureCLI@2
      inputs:
        azureSubscription: 'Pay-As-You-Go(f30deb63-a417-4fa4-afc1-813a7d3920bb)'
        scriptType: 'bash'
        scriptLocation: 'inlineScript'
        inlineScript: 'az acr login --name=$(containerRegistry)'
    
    - task: Docker@2
      displayName: Build and push an image to container registry
      inputs:
        command: buildAndPush
        repository: $(imageRepository)
        dockerfile: $(dockerfilePath)
        containerRegistry: $(dockerRegistryServiceConnection)
        tags: |
          $(tag)
    - task: AzureCLI@2
      inputs:
        azureSubscription: 'Pay-As-You-Go(f30deb63-a417-4fa4-afc1-813a7d3920bb)'
        scriptType: 'bash'
        scriptLocation: 'inlineScript'
        inlineScript: |
          az container create \
                --name ibrahims \
                -g ibbus-container-RG \
                --image $(containerRegistry)/$(imageRepository):$(tag) \
                --registry-login-server $(containerRegistry) \
                --registry-username ibrahims  \
                --registry-password lxkaWa1MtCG3Li0M8ZPDaVJmFzsj9Kwf79B5UaLwGh+ACRBJQQS9 \
                --dns-name-label aci-demo-ibrahimsi
```

## Hands-On 🗂️ - Day-10 (Azure Docker Container — DevOps)  ✅

👉 https://medium.com/@ibrahims/azure-docker-container-devops-4b487c4a1903 👈

<img width="913" alt="Last add ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/d01ca61d-c1eb-4191-a426-e0eb7965a404">

If you are doing a project on Hands-on follow the above blog it would be more helpful.

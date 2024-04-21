# Day 9/16 - Azure DevOps Self-hosted agents on Virtual Machine Scale Sets 🏗

Self-hosted agents give you more control to install dependent software needed for your builds and deployments. Also, machine-level caches and configuration persist from run to run, which can boost speed.

Create and manage a group of load-balanced VMs. The number of VM instances can automatically increase or decrease in response to demand or a defined schedule. Scale sets provide the following key benefits: Easy to create and manage multiple VMs

## Microsoft-hosted vs. self-hosted agents

Microsoft-hosted agents are run in individual VMs, which are re-imaged after each run. Each agent is dedicated to a single organization, and each VM hosts only a single agent. 

An agent that you set up and manage on your own to run jobs is a self-hosted agent. You can use self-hosted agents in Azure Pipelines or Azure DevOps Server, formerly named Team Foundation Server (TFS). Self-hosted agents give you more control to install dependent software needed for your builds and deployments.

![self host agent difference ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/67b3870a-06fe-40ec-834d-bdfed262516b)

## Use case of self-hosted agents

![Self hosted use ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/6414b5d5-ddae-432d-a32f-7f71b6755352)

### Ways to setup self-hosted agents: 
- Azure Virtual Machine
- Azure Virtual Machine Scale Sets (VMSS)
- Containers etc.
  
### What is a Virtual machine scale set
- A group of one or more identical Virtual machines that can be scaled out and scaled in based on the demand/schedule and manual actions.
- This ensures high availability and fault tolerance so that if one VM crashes, another gets provisioned using the template.
- This is similar to AWS AutoScaling Groups or GCP Managed Instance Groups.

## Hands-On 🗂️ - Day-9 (Azure Virtual Machine Scale Set Agents | VMSS — DevOps)  ✅

👉 https://medium.com/@ibrahims/azure-virtual-machine-scale-set-agents-vmss-devops-45f8fa40523d 👈

<img width="913" alt="VMSS ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/e152a169-7995-4636-8bce-458190637b81">

If you are doing a project on Hands-on follow the above blog it would be more helpful.
  


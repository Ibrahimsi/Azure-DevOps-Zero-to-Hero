# Day 14/16 - Azure DevOps Wiki | Azure DevOps Zero to Hero Full Course

Azure DevOps Wiki is a documentation solution within the Azure DevOps Suite. It can help developers address their documentation needs at various stages of their product development, such as creating specifications, writing meeting reports, or any general information that they would like to share with the team.

There are two types of Wiki, 
1) Project wiki (Provisioned)
2) Code wiki

Refer Official documentation **https://learn.microsoft.com/en-us/azure/devops/project/wiki/provisioned-vs-published-wiki?view=azure-devops**

## Project wiki (Provisioned)

- Creation limit →Only one per project
- Edit → Only editable from the Wiki page
- Revert to the previous version → Revert page by page from the Wiki page
- Version-by-version wiki → uncreatable
- Reference → Stakeholders are also available
- Location → Not conscious. Internally, a location called {ProjectName} .wiki is automatically created and managed there.

## Code wiki (as a code)

- Creation limit → Multiple creations can be made in the project
- Edit → Editable with Git Push to Wiki page or Repos page or Repos
- Revert to the previous version → Revert with Repos page (or) Git Push. Same procedure as Git Revert
- Version-by-version wiki → Can be created using Repos’ Git branch
- Reference → Stakeholder cannot be referenced
- Location → Repos Git. Select the location of the Folder on Git and create it. It is also possible to set multiple settings for one Git.

## Access Level

1. Stakeholder → Reference to the project wiki only.
2. Basic (or) Visual Studio Subscription → Same as Permission.

## Hands-On 🗂️ - Day-14 (Azure Wiki — DevOps)  ✅

👉 https://medium.com/@ibrahims/azure-wiki-devops-f14132e47d62 👈

<img width="921" alt="Wiki ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/8212c9b6-6649-411f-914d-447aac689e3a">

If you are doing a project on Hands-on follow the above blog it would be more helpful.




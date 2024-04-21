# Day3 - Azure Repos

## What is Azure repos?

Azure Repos is a set of **version control tools** that you can use to manage your code. Whether your software project is large or small, using version control as soon as possible is a good idea. Version control systems are software that helps you track changes you make in your code over time.

![Repo 1 ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/64f045de-682e-4807-b08e-3cbde8d83af6)

Version control, also known as source control, is the practice of tracking and managing changes to software code. It's software tools that help software teams manage changes to source code over time.

Even if you are working on a personal project, version control helps you stay organized as you fix bugs and develop new features. Version control keeps your development history so you can quickly review and even roll back to any code version.

- Helps you track changes in the codebase
- Maintains the history of your codebase, who made the changes, what changes were made, why the changes were made, etc
- Helps you stay organized
- Gives you the ability to rollback the changes as needed


## Git vs. TFVC

Azure Repos supports two types of version control
- Git
- Team Foundation Version Control (TFVC)

**CheetSheet**

<img width="1046" alt="GIT   TFVC ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/fba1fb41-94bb-43f6-a251-847e69791611">

### Git
Git is a DevOps tool used for source code management. It is a free and open-source version control system used to handle small to very large projects efficiently. Git is used to tracking changes in the source code, enabling multiple developers to work together on non-linear development.

### TFVC
Team Foundation Version Control (TFVC) is a centralized version control system. Typically, team members have only one version of each file on their dev machines. Historical data is maintained only on the server. Branches are path-based and created on the server. You can host TFVC on hosting services such as Perforce, SVC, Azure Repos, etc.


## Working with branches

![Git branches 3 ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/b351cc0b-aa09-4326-863e-351659c0d22d)

𝗕𝗿𝗮𝗻𝗰𝗵𝗶𝗻𝗴, 𝗶𝗻 𝗮𝗻𝘆 𝘃𝗲𝗿𝘀𝗶𝗼𝗻 𝗰𝗼𝗻𝘁𝗿𝗼𝗹 𝘀𝘆𝘀𝘁𝗲𝗺, 𝗶𝘀 𝗯𝗮𝘀𝗶𝗰𝗮𝗹𝗹𝘆 𝗹𝗶𝗸𝗲 𝗰𝗼𝗽𝘆𝗶𝗻𝗴 𝗼𝗻 𝘀𝘁𝗲𝗿𝗼𝗶𝗱𝘀. 𝗜𝘁 𝗮𝗹𝗹𝗼𝘄𝘀 𝘆𝗼𝘂 𝘁𝗼 𝘄𝗼𝗿𝗸 𝗼𝗻 𝗺𝘂𝗹𝘁𝗶𝗽𝗹𝗲 𝘃𝗲𝗿𝘀𝗶𝗼𝗻𝘀 𝗶𝗻 𝗽𝗮𝗿𝗮𝗹𝗹𝗲𝗹 𝘄𝗵𝗶𝗹𝗲 𝗸𝗲𝗲𝗽𝗶𝗻𝗴 𝗹𝗶𝗻𝗸𝘀 𝗯𝗲𝘁𝘄𝗲𝗲𝗻 𝘁𝗵𝗲𝗺 𝘀𝗼 𝘁𝗵𝗮𝘁 𝘁𝗵𝗲𝘆 𝗰𝗮𝗻 𝗯𝗲 𝗺𝗲𝗿𝗴𝗲𝗱 𝗯𝗮𝗰𝗸 𝘁𝗼𝗴𝗲𝘁𝗵𝗲𝗿.

Some common branching patterns used in Git include:

𝗠𝗮𝘀𝘁𝗲𝗿: The "master" branch is usually the main branch that contains the production-ready code. It is usually the default branch in a Git repository.

𝗗𝗲𝘃𝗲𝗹𝗼𝗽: The "develop" branch is used for ongoing development work. It contains the latest version of the code, which is updated regularly as new features are added or changes are made.

𝗙𝗲𝗮𝘁𝘂𝗿𝗲 𝗯𝗿𝗮𝗻𝗰𝗵𝗲𝘀: "Feature" branches are used to isolate development work on specific features or changes. They are created from the "develop" branch and are typically merged back into "develop" when the work is complete.

𝗥𝗲𝗹𝗲𝗮𝘀𝗲 𝗯𝗿𝗮𝗻𝗰𝗵𝗲𝘀: "Release" branches are used to prepare for a release. They are created from the "develop" branch and are used to stabilize and test the code before it is released to production.

𝗛𝗼𝘁𝗳𝗶𝘅 𝗯𝗿𝗮𝗻𝗰𝗵𝗲𝘀: "Hotfix" branches are used to address urgent issues that need to be fixed immediately. They are created from the "master" branch and are used to make quick fixes that can be merged back into "master" and "develop."

## Hands-On 🗂️ - Day-3 (Azure Repos — DevOps)  ✅

👉 https://medium.com/@ibrahims/azure-repos-devops-59242c7ab529 👈

<img width="926" alt="Azure repo final" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/e8360c16-0a9c-4229-b024-4144fdec3e78">

If you are doing a project on Hands-on follow the above blog it would be more helpful.


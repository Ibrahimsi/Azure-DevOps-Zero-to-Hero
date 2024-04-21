# Day2 Azure Boards and Agile Project Management <img width="39" alt="Azure boards ibbus 1" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/47621011-2819-400d-8cab-1a191bf51f76">

## Azure DevOps Demo Generator
The Azure DevOps Services Demo Generator is a service that helps you provision projects in your organization with pre-populated sample content that includes source code, work items, iterations, service connections, and build and release pipelines based on a template you choose.

1. Navigate to **https://azuredevopsdemogenerator.azurewebsites.net**. This utility site will automate the creation of a new Azure DevOps project within your account that is prepopulated with content (work items, repos, etc.) required for the lab. 

2. Sign in using the Microsoft account associated with your Azure DevOps subscription.

<img width="1406" alt="Azure devops generator 2 ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/9519f15a-9251-4b0f-976c-4c6efb1ad140">

3. Accept the permission requests for accessing your subscription.

4. Select the PartsUnlimited template and click Select Template.
   
<img width="1435" alt="parts unlimited 3 ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/c57e2e9f-2a44-4001-88c0-bc0bd7d8d84b">

6. Click Create Project and wait for the process to complete.

<img width="1435" alt="parts unlimited project 4 ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/0748c34d-cef6-47bf-b621-1fa9ee89a9e3">

## Azure Boards Overview 
Azure Boards is a web-based service that enables teams to plan, track, and discuss work across the entire development process, while it supports agile methodologies.

## Defining Teams and Work Items

A team is defined as a group of people who perform interdependent tasks to work toward accomplishing a common mission or specific objective.

A work item is the primary unit of work completion in an application, and the primary collection of data that a flow operates on. Work items to plan and manage your project.

### What is a Work Item

Work items are also used to represent the Product Backlog. A list of Epics, Features, User Stories and Bugs in a certain order.

The "Board" provides an alternative view of the product backlog by state, often referred to as a Kanban Board. On each card, you can also visualize tasks.

The Sprint Backlog breaks down the work on the Product Backlog into tasks that can be picked up in an Iteration/Sprint. This view represents what used to be called the "Scrum board" in old revisions of the Scrum Guide.

*  Task to do
*  A bug to fix
*  An issue
  
![work item types 5 ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/fa916e9d-5d8d-47d5-b205-a6085a861df1)

## Kanban Board 📃

A kanban board is an agile project management tool designed to help visualize work, limit work-in-progress, and maximize efficiency (or flow). It can help both agile and DevOps teams establish order in their daily work. It can be divided into multiple stages such as

1) To Do
2) Doing
3) Done

<img width="1440" alt="Kanban board 6 ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/a9f5abf2-6e27-4c97-94a8-1da85e66b306">

## Azure Boards Processes

Azure DevOps has three processes out of the box 

1) Basic
2) Agile
3) Scrum
4) CMMI

Each of these processes adheres to a particular methodology. Agile is the most universal and widely used.

**Choose Basic when your team wants the simplest model that uses Issues, Tasks, and Epics to track work.**

The basic process contains three work item types:

<img width="205" alt="Basic azure boards epics 7 ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/b9c2cb89-9a57-40f6-8770-4282c38c9df2">

- Epics: Epics are used to group work under larger scenarios (or) Epics are large bodies of work that can be broken down into many smaller tasks (called stories).
- Issues: General problems (or) concerns in the product or project.
- Task: Tasks are the smallest amount of work that can be assigned to someone, act as a pipeline, and packaged scripts (or) procedures that are abstracted with a set of inputs.


<h1>Basic Azure Board</h1>

Azure board is an interface that lets you track tasks, features, and even bugs that may be associated with your project. Here you are aided by three work item types

```
Epics Issues Tasks
```
<img width="205" alt="Basic azure boards epics 7 ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/ae4fe14b-95f2-4827-a943-1233172c692e">

Work gets completed the status gets updated stage by stage from

```
To Do Doing Done
```

<img width="205" alt="To do ibbus 8" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/f79042e3-4429-4366-bef7-526bd939e68b">

Each time we create (or) add an issue, task (or) an epic, it means we are creating a work item. Every work item we create would represent an object. This object is stored in the work item data store. Every item here will have an identifier, assigned to it. **These IDs are unique** to a particular project.

## Features Of Azure 

1) Kanban Implementation
2) Collaborate using Azure Boards
3) Flexibility to work in sprints and to implement Scrum
4) Integrate with GitHub

## Scrum process
Scrum is an agile project management framework that helps teams structure and manage their work through a set of values, principles, and practices.

**A scrum-based process typically involves below work items:**

![work item types 5 ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/36718531-48ea-4456-a18d-ddb1abe7d4d9)

1. **User Stories:**
   - A user story is the smallest unit of work in an agile framework.

2. **Tasks:**
   - A task is a piece of work that needs to be done. The process is a series of actions that are done for a particular purpose.

3. **Bugs:**
   - Specific issue related to a defect (or) flaw in the software code.

4. **Epics:**
   - Epics are used to group work under larger scenarios. An epic may be broken down into smaller, more manageable pieces, known as user stories or features. 

5. **Features:**
   - More detail on how a product should be built, while user stories provide further detail on what needs to be done by each team member.

6. **Product Backlog:**
   - Your project plan, which shows what your team intends to deliver. It contains user stories, backlog items, and (or) requirements that you add to it.

8. **Sprint Backlog:**
   - Subset of the product backlog that the Development Team commits to completing during a specific sprint. All the Sprint To-dos. list of work items your team plans to complete during a project sprint. 

9. **Impediments:**
   -  Track items that may block work from getting done.

10. **Test Cases:**
   - Develop test cases to define the things that you must validate to ensure that the system is working correctly and is built with a high level of quality.


## Defining Sprints 📅

A sprint is a time-boxed effort to complete a set of predetermined work.
A Sprint (also known as Iteration in Azure DevOps) is the amount of time we have to complete our tasks. Sprints help keep us focused. 
At the end, we can have a short retrospective meeting to share what we've accomplished. 

After that, we can plan the next one.

![Sprint what is ibbus](https://github.com/Ibrahimsi/Test-Azure/assets/41462796/8b0570d0-f40f-462e-a425-ab48ba7a7982)

Sprints are time-boxed periods of one week to one month, during which a product owner, scrum master, and scrum team work to complete a specific product addition.

**Sprints should last anywhere from 1 to 4 weeks**.

### Acceptance Criteria

**Acceptance criteria** Conditions a software product must meet to be accepted by a user, a customer, or other systems. They are unique for each user story and define the feature behavior from the end-user's perspective.

## Important member of Agile/Scrum 🕵️‍♂️

Scrum was the creation of Done Increments each Sprint. All the other good stuff that Scrum brings to product development starts and builds from this core concept.

1) Product owner
2) Scrum master
3) Development team members

**Product Owner:** Plan the feature set to deliver, set priorities, and track the status of work, code defects, and customer issues. Product Owner is the person that is responsible for maximizing the results of the development team. 

**Scrum Master:** Servant leader for the rest of the team to help them through the project and remove obstacles out of the way so they can achieve the desired results. 
  - What went well
  - What could be improved
  - Planning adjustments for the next sprint

**Development Team:** Developers and IT operations working collaboratively throughout the product lifecycle, in order to increase the speed and quality of software deployment. The team self-organizes and collaborates to achieve the sprint goals.

**Stakeholders:** Are users with free but limited access to Azure DevOps features and functions. They provide input feedback and may attend sprint reviews and demos to assess progress. Stakeholders could include customers, end-users, managers, (or) other teams.

**Scrum Team:** A scrum team is a small and nimble team dedicated to delivering committed product increments. A scrum team's size is typically small, at around 10 people, but it's large enough to complete a substantial amount of work within a sprint.

**Customers/Users:** Users can include human users, service accounts, and service principals.

**Management:** Refers to the tasks and processes required to maintain your business applications and the resources that support them.

**External Vendors/Partners:** External users are individuals who are not part of your organization such as customers, partners, suppliers, vendors, clients, (or) other third parties.

## Hands-On 🗂️ - Day-2 (Azure Boards — DevOps)  ✅

👉 https://medium.com/@ibrahims/azure-boards-devops-05413ae466c8 👈

<img width="1427" alt="Azure Board ibbus" src="https://github.com/Ibrahimsi/Test-Azure/assets/41462796/553089cc-496a-4c97-8063-5736e6f8fed2">

If you are doing a project on Hands-on follow the above blog it would be more helpful.


---
layout: single

permalink: /chatbot-process
title: "Chatbot and Processes"
excerpt: "Chatbot and Processes"
last_modified_at: 2021-06-14
toc: true
sidebar:
  nav: "docs"
---

## Chatbot & Workflow Engine Integration

In this article, we will talk about Process-Aware Conversational Agents and walk you through the steps involved in building a GUI with Vue.js for hosting such agents.

Business processes can be helpful in multiple scenarios, and this tool will help guide the user throughout a process execution with a certain amount of flexibility.

Our team has already developed a [Process-Aware Conversational Agent Generation Guide](http://www.repositorio.poli.ufrj.br/monografias/projpoli10033716.pdf) — a step-by-step tutorial for integrating Rasa, a chatbot framework, with Camunda Engine, a Workflow Management System. All processes covered in this article and in the [video](https://www.youtube.com/watch?v=E_CFhojGWSw) have been created according to that guide.

Just like the PACA Generation Guide, running the GUI will also require the installation of three tools in these specific versions: Rasa 1.8.2, Rasa SDK 1.8.0, and Camunda Modeler 3.4.1. That is because this project has four different components. They are:
1. A front end built with Vue.js;
2. Camunda Engine, for coordinating the process execution;
3. Rasa API, which needs to be accessed by our front end and will take care of receiving messages from the user and replying accordingly;
4. Rasa Actions, a Python server that runs custom actions that the bot shall execute.

In this project, we are using a task-automation package called `concurrently`, installed with `npm`. When running `npm run serve`, this package will allow that all necessary steps occur simultaneously:
* The process model will be automatically deployed to Camunda.
* The front end will be served.
* The two Rasa components (both API and Actions) will be started.

## The Idealized Solution
This article will examine the integration of two different processes -- **Trip Planning** and **Wedding Planning** -- into our GUI. These two processes are modelled as follows:

**Trip Planning:**
![Trip Planning Process](/_pages/chatbot-process/assets/TripPlanningBPMN.png)

**Wedding Planning:**
![Wedding Planning Process](/_pages/chatbot-process/assets/WeddingPlanningBPMN.png)

Our finalized GUI is supposed to look like this:
![Finalized GUI](/_pages/chatbot-process/assets/FinalizedGUI.png)

When the user clicks on the `Book a trip` or the `Plan a wedding` button, it should open a chat component powered by Rasa that directly affects our process instances in Camunda.
As soon as the user asks to book a trip, it will initiate a process instance in Camunda, as it is possible to see in Camunda Cockpit.
![Initiated Process Instance in Camunda Cockpit](/_pages/chatbot-process/assets/CamundaCockpit.png)

The chatbot will constantly tell the user the next available actions and ask for information when needed.
This **Trip Planning** process has two variables, the flight date and another variable for knowing whether the user wants to book a transfer or not. Rasa will ask for these pieces of information during the conversation and then store them in Camunda.
![Rasa and Camunda Cockpit](/_pages/chatbot-process/assets/ChatbotTravelFlightCockpit.png)

Finally, when the execution is finished, Rasa informs the user, and the process instance in Camunda is terminated.
![Rasa informing Process Instance termination](/_pages/chatbot-process/assets/ChatbotTravelTour.png)

The repository containing the code for this GUI, with both the **Trip Planning** and **Wedding Planning** processes, can be accessed [here](https://github.com/luis-f-lins/process-aware-conversational-agent-gui). 
This will be the base folder for all the changes that will be listed in the next section.

## How To Implement It
Here, we will see how processes are added to our GUI. We are going to add both the **Trip Planning** and **Wedding Planning** processes.

### 1. Copying BPMN File
First, we need to copy each process’s BPMN diagram to our GUI project folder. The BPMN diagrams need to have been modeled according to our Process-Aware CA Generation Guide. Inside our project, there is a `camunda` folder, and the diagrams will go into **`camunda > configuration > resources`**. This step will allow Camunda to automatically deploy those process definitions when restarting.
![Resources folder](/_pages/chatbot-process/assets/FolderResources.png)

### 2. Copying Chatbot Folder
Then, for each process we will support, we need to copy a folder with all of its Rasa files into our GUI project folder. In this case, there needs to be two chatbot folders, `trip-planning` and `wedding-planning`, in our project's root. As previously mentioned, these chatbots need to have been built using the provided PACA Generation Guide.
![Chatbot Folder](/_pages/chatbot-process/assets/FolderChatbot.png)

We shall now start editing some code.

### 3. Editing package.json
As previously explained, in `package.json`, we use an `npm package` for task automation called "concurrently", which will be very useful to our project. Typically, we would have to run Camunda Engine and each Rasa process in different terminal windows.
However, this concurrently lib allows us to run everything with a single command. 

Using `concurrently`, the `serve` script must run a few scripts:
* One for Camunda
* One for Vue.js
* Two Rasa scripts (API and Actions) *for each supported process*

Rasa uses by default `port 5055` for the actions and `port 5005` for the API, and the trip planning process will use them, so for the wedding planning process, we need to change them to `5056` and `5006`, respectively.
![Editing package.json](/_pages/chatbot-process/assets/EditingPackageJson.png)

Since we are changing the Actions port for the wedding planning process, we need to go into its chatbot folder (`wedding-planning` in the root) and edit the `endpoints.yml` file, changing the port in the `action_endpoint` URL from `5055` (the default port) to `5056`.
![Editing endpoints.yml](/_pages/chatbot-process/assets/EditingEndpointsYml.png)

Let's now move to the Dashboard file, where we'll begin to add the new process to the GUI itself.

### 4. Editing Dashboard file
Much of the `Dashboard.vue` file will not need to be modified since it is standard for all applications. However, some of the variables and elements in this file are crucial and must be covered here because they will need to be adjusted if any of the processes are changed.

1. First, in the `data` object, there should be an `openChat` object that determines which chatbot is open. Since we are accounting for two different chatbots, we need to add them both into `openChat`.

2. In the `data` object, we also need to add a message array for each chatbot to store each conversation separately from the others. In this case, we will have two message arrays, `tripMessages` and `weddingMessages`.

3. Since we use the same chat component in the front end regardless of which chatbot we are talking to, we use a computed property called `messages` to select which message array to use based on the `openChat` object.
![Editing Dashboard](/_pages/chatbot-process/assets/EditingDashboard.png)

4. Then, we need to add the available API ports in the `addMessage` method, and the appropriate port will be chosen according to which chatbot is open. This port will determine which Rasa API the GUI will be communicating with at any given time.
![Editing openChat ports](/_pages/chatbot-process/assets/EditingOpenChatPorts.png)

5. We now add two process methods (`booktrip` and `planwedding`). Each of them
will set that process's particular key in the `openChat` object to `true` when we click on that process's button and turn all the other open chats to `false`. These process methods could easily be turned into a single method to avoid code duplication; however, they are kept separately here for clarity purposes.
![Toggling openChat between processes](/_pages/chatbot-process/assets/EditingOpenChatProcessSelection.png)

6. Finally, we must have a button for each process chatbot, and they will call the appropriate process method when clicked, opening that particular chatbot.
![Button for each process chatbot](/_pages/chatbot-process/assets/EditingOpenChatButton.png)

Hope this article has been useful!

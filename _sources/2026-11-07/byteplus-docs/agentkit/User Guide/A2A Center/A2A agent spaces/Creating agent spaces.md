---
title: "Creating agent spaces"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Creating_A2A_agent_spaces"
---

The A2A agent space is a logical space in the A2A Center used to organize and manage A2A agents. You can register A2A agents from the same business domain, team, or collaboration scenario into one space, enabling unified management, semantic search, and calling. Business applications or caller agents can discover, orchestrate, and interact with external agents through the A2A agent space.

This topic describes how to create an A2A agent space in the AgentKit console.

<span id="BYqJAxWw"></span>
## Background information

A2A agent spaces serve as a "directory and management boundary". As the number of connected A2A agents increases, if all agents are placed in the same space, callers will face high costs in retrieval, filtering, and governance. Using different spaces, you can organize agents by business domain, team, environment, or scenario, simplifying agent discovery for callers and agent maintenance for the platform.

<span id="W0k4mW5T"></span>
## Core concepts


|**Terms** |**Description** |
|---|---|
|Agent Card |The standardized capability description of the A2A agent, typically containing information such as ID, name, protocol version, communication mode, and service entry. This information serves as an important basis for callers to determine "whether this agent is available" and "how to call it". |
|Agent semantic retrieval |Returns the best\-matching agent within the current space based on natural\-language call intent. Suitable for scenarios where there are a large number of agents or the caller is unsure of the specific agent name. |


<span id="55RQu4kL"></span>
## Prerequisites

The AgentKit service has been activated. To activate AgentKit, please go to the [AgentKit console](https://console.byteplus.com/AgentKit), and follow the system prompts to complete the operations.

<span id="9uN2KjGs"></span>
## Procedure


1. Log in the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Basic Components \> A2A Center".

3. In the top menu bar, select the region and project.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After you select a project, newly created spaces can be associated only with this project. If you select "All resources", newly created spaces can be associated with any project under the current account.   </div>
   

4. In the drop\-down list, click the "Create space" button.

5. Configure the agent space parameters.

   
   |Parameter​ |Description |Screenshot |
   |---|---|---|
   |Space name |Specify a name for the agent space. The name cannot be modified after creation. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6016448fd1ffe841a446b6ac04d69017.png) </span><br><br> |
   |Agent semantic retrieval |After enabling, the caller can search for the best\-matching agent within the current space based on natural\-language call intent, and return an AgentCard. ||
   |Associated project |A project is a collection of resources. You can add the new agent space to a project and manage it centrally at the project level, which helps keep resources independent and maintain data security. For more information about projects, see [Managing projects](https://docs.byteplus.com/en/docs/agentkit/Managing_projects).<br><br><br>* By default, the project is default. Each resource can only belong to one project.<br><br>* If you select a specific project in the top menu bar when entering the creation page, the newly created space can only be associated with that project. To associate it with another project, change the project in the top menu bar to either "All resources" or the target project.<br><br>* After a project is selected, the created agent space can only be used by users who have permission for that project. After you create an agent space, you can change the project associated with the agent space based on your needs. For information about how to change a project, see [Project resource management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-project).<br><br>* If no projects are available, you can click the "Create project" button to create one. After you create a project, return to this page to select the new project. ||
   |Tag |A tag is a key\-value pair used to identify cloud resources. Tags help you categorize cloud resources based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your cloud resources.<br><br>Click the "+ Add tag" button, select an existing tag or enter a new tag, and then associate the tag with the agent space. For more information, refer to [Tag management](https://docs.byteplus.com/en/docs/agentkit/Tag_management).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can associate up to 20 tags at one time, and associate up to 50 tags with one resource.</div><br> ||
   

6. Click "Confirm" to complete the creation.


<span id="LDkyvK0j"></span>
## What to do next

After creation, you can continue to [register A2A agents](https://docs.byteplus.com/en/docs/agentkit/Registering_A2A_agents) in this space and [enable/disable semantic retrieval](https://docs.byteplus.com/en/docs/agentkit/Enabling_or_disabling_semantic_retrieval) capability based on your business needs.

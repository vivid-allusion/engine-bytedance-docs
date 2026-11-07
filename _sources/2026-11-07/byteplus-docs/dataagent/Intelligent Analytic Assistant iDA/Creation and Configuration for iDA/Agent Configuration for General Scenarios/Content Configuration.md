---
title: "Content Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Content_Configuration_"
---

Content configuration is divided into scene configuration and PC\-side configuration. This article introduces you to the configuration guidance related to content configuration when creating and configuring intelligent analysis agents.

<span id="21a99eb7"></span>
# Scene Configuration

Scene configuration function is used to orchestrate and manage the capability entry of the agent. Administrators can create groups by business direction, add specific scenarios under the groups, and configure corresponding Skills, Internet search capabilities, and recommendation questions for each scenario. At the same time, the system supports drag\-and\-drop sorting of groups and scenes to control the display priority of the client, so as to realize the structured presentation and fine operation of the agent's capabilities.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0746b93c1b8047e5a26938c97782112d~tplv-goo7wpa0wc-image.image) </span>


1. Select the corresponding agent in the agent list, and click the **agent configuration** button below the agent to enter the agent configuration page.

2. Tab page Select the scene configuration and enter the function page. Click the **Edit** button in the upper right corner to edit the scene configuration and configure the recommended scene for the agent to help you quickly focus on business goals; the scene group and scene can be adjusted by dragging and dropping.

3. Each small area is a scene group, which supports renaming and deleting scene groups in the area, and can customize the scene group capability icon. Here are the specific instructions for the relevant operation:

   
   |Scene group action item |Explain |
   |---|---|
   |Rename scene group |Modify the packet header to adjust the packet name as the business changes.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14d09a272274409b9c4aa4766ce87b79~tplv-goo7wpa0wc-image.image) </span> |
   |Replace scene group icon |Replace the visual icons before grouping to help team members quickly identify different business domains through graphics, enhancing interface visibility.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55500ef7b6b74af6bea0748faa9fac98~tplv-goo7wpa0wc-image.image) </span> |
   |Delete scene group |Remove the entire group that is no longer needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Before performing this operation, it is usually necessary to confirm whether the group contains subscenes to avoid accidentally deleting the configured content.</div><br> |
   |Add a single scene |The area supports adding scenes. Click the Add Scene button, select the corresponding scene in the pop\-up scene list, and click the Add button to add scenes to the scene group; a single scene supports editing and deleting operations.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b6ba59f799d47e494cd7710ae013134~tplv-goo7wpa0wc-image.image) </span><br><br><br>1. Edit: Click the Edit Scene button to enter the detailed configuration pop\-up window for a single scene. The currently visible configuration items mainly include:<br><br>   * Configuration Skill: Bind the underlying capability module for the current scenario to determine the capability logic actually invoked by the scenario.<br><br>   * Network search: Control whether to allow access to Internet information in this scenario, suitable for tasks that require real\-time external information.<br><br>   * Recommended Questions: Configure the guide questions that will be displayed first after you enter the scene to help you quickly initiate effective questions.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4e1392286f1486c8bfe8797c7dd2888~tplv-goo7wpa0wc-image.image) </span><br><br><br>2. Click the Delete button to delete the current scene.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Scenes cannot be restored after deletion, please proceed with caution.</div><br> |
   |Add separate scene groups and scenes |Supports adding scenes individually as independent scenes, and supports adding new scene groups. Under Scene Configuration, click the Add Analysis/Add Scene button to add new independent scene groups and scenes.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b71d5d822314789a99d6683e53452a2~tplv-goo7wpa0wc-image.image) </span> |
   

4. After the scene configuration is completed, click the Save button in the upper right corner to save the configuration. The edited scene configuration can be viewed below the agent Q & A interface.


<span id="95051878"></span>
# PC side


1. Select the corresponding agent in the agent list, and click the **agent configuration** button below the agent to enter the agent configuration page.

2. Click the left navigation bar **content configuration** , select the **PC side** on the page, configure the PC side summary title and summary copy; after entering the content, click the **summary preview** button to preview the display effect, and click the save button to save the effect after confirming.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4c012f8d5e44257bd820a41537b1823~tplv-goo7wpa0wc-image.image) </span>

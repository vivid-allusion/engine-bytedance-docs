---
title: "Operation Processes of Lark Binding and Authorization"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Operation_Processes_of_Lark_Binding_and_Authorization"
---

This function is used to access Lark interaction capabilities for iDA, and supports official, general, and vertical agents to complete Lark binding. After the binding and authorization are successful, the system will automatically generate a conversational Lark robot, allowing you to directly invoke the agent capabilities in the Lark scene. This article will explain the binding rules and the specific operation process.

<span id="78ce7a75"></span>
# Prerequisite


* You are logged in to Lark and make sure you are logged in to the [Lark open API](https://open.larkoffice.com/app). The two login accounts of Lark and Lark open API must be the same.


<span id="92f4a2ab"></span>
# **Step 1: Create a Lark app**


1. Log in to the BytePlus console, select DataAgent, and enter the corresponding project. Find the corresponding agent in the project and click to enter.

2. In the left navigation bar of the agent Q&A interface, click Connector Options to enter the connector management page.

3. Connector Click on Lark's Connect button to proceed to the authorization step.

4. Click the **Create Lark Application** button in the pop\-up window to jump to the Lark open API to create the configuration page of the Lark agent application. You can set the avatar and name for your application. Click the **Create Now** button when the configuration is complete.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca2da1ec659f444f99be1e9e5c28af10~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After clicking the Create Now button, the system will issue an operation safety prompt. You need to confirm the following information to ensure that it is correct. Click the <strong>Continue to Create</strong> button to continue the creation process.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Please confirm that you are accessing this page through a secure channel initiated by yourself, and not a QR code or link forwarded by others.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After successful creation, the channel will obtain the app ID and app secret of the app, and can operate your agent app.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fc6556bd2704a6c99960f5be7bcc45f~tplv-goo7wpa0wc-image.image) </span>

5. After the creation is successful, return to the agent page to display that the Lark application has been configured. You can click the page Created Application to open the Lark permission button to open the Lark permission.


<span id="465c40a6"></span>
# Step 2: **Lark permission is opened**


1. On the agent Lark authorization page, click the created application, go to the Lark permission opening button, and jump to the Lark open API Lark permission opening page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eec74d5c11084911a7a9c74a5e3522ee~tplv-goo7wpa0wc-image.image) </span>

2. Click the page open and authorize button, and the system will automatically open the authorized permission.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f451ad87a18849f1bd39699add15c02b~tplv-goo7wpa0wc-image.image) </span>

3. After successful activation, the page will return to the agent Lark authorization page and display that the authorization has been completed. You can talk to the iDA robot in Lark.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4351339038fd42ebb85ce37af16d6e42~tplv-goo7wpa0wc-image.image) </span>

4. If there are some permissions that need to be authorized manually, the page will prompt you to authorize manually and further add permissions.

   1. You can click on the page **copy list, to open authorization** button, the system jumps to the developer background rights management office.

   2. On the interface, click Batch Processing \- Batch Import/Export Permissions, copy the `JSON`that the agent needs to manually authorize to the code area, click Next, confirm the new permissions, and the permissions are added successfully.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The permission to import will be used as the permission for this new application, and will not affect the permission that has been applied for or opened.      </div>
      

<span id="6ecadc31"></span>
# Using iDA in Lark

iDA supports use in flying book single chat and group chat scenarios. Users can initiate data Q&A and analysis interaction by chatting with the corresponding robot alone or summoning the robot in the group. This capability supports session context inheritance and permission isolation, enabling users to directly complete data service calls within Lark, without the need to switch platforms to improve data acquisition and analysis efficiency.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Group chat dialogues do not support querying the content of datasets and knowledge bases, so as to avoid group members querying data outside the authority, and only support querying information through online search.</div>


<span id="27e234a2"></span>
## Conversation with iDA at Lark

After the Lark is successfully bound and authorized, the iDA robot will be added to the conversation list. You can directly click the robot to enter the conversation and have a conversation with the robot. It also supports uploading relevant files to ask questions to the robot.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e706c6e8641418796d8faffd400b3f0~tplv-goo7wpa0wc-image.image) </span>

<span id="f920049a"></span>
## Using iDA in group chats


1. Select a group chat to enter the conversation interface, click Settings \- Group Robot \- Add Robot \- Add in the upper right corner of the group chat, and select iDA's Lark assistant robot to add the robot to the group chat.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc4cb1f7e8244de3b8236c6ffca0284d~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8df29975b5434a69829606ae4d6f033e~tplv-goo7wpa0wc-image.image) </span>

2. After the robot is successfully added, you can @robot in the group chat to ask questions to the robot, and the robot will return corresponding results according to your questions. For example, you can enter "@robot to search for the latest information on 'Subsidy Policy for New Energy Vehicles in 2026'."

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5844e3b102de45d5a28d1b3fde263720~tplv-goo7wpa0wc-image.image) </span>


<span id="369e7f05"></span>
# Cancel authorization

If you need to cancel the authorization, click the Lark Authorization button at the top left of the agent, select Cancel Authorization, and the system will cancel the authorization of Lark. Also, you will not be able to use the Lark robot to communicate with the agent.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7898fb569c38496da8b95ea2ef9d2c1d~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e4ea0a2f884415d97b542e13522f98e~tplv-goo7wpa0wc-image.image) </span>

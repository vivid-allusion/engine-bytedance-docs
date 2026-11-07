---
title: "DingTalk Binding and Authorization"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/DingTalk_Binding_and_Authorization"
---

The DingTalk connector is used to connect the iDA to the DingTalk account. After completing the authorization, users can chat with iDA individually or in a group chat in DingTalk, and use related functions such as messages, documents, and calendars through DingTalk open capabilities. With the DingTalk Connector, iDA can provide intelligent Q&A, content processing, and collaboration assistance capabilities in DingTalk work scenarios, enabling users to efficiently complete work tasks within existing office processes.

This article will introduce the authorization process of the DingTalk connector, how to use it, and how to handle authorization exceptions.

<span id="05d8a298"></span>
# Prerequisite


* **iDA agent has been opened:**  You need to have a usable iDA agent first, and enter the conversation page of the corresponding agent;

* **Have a DingTalk account and authorization permissions:**  You need to have a DingTalk account that can be logged in and used normally, and have logged in at the mobile end to complete the connector authorization; you can [log in to the DingTalk developer platform](https://login.dingtalk.com/oauth2/challenge.htm?redirect_uri=https%3A%2F%2Fopen-dev.dingtalk.com%2Fdingtalk_sso_call_back%3Fcontinue%3Dhttps%253A%252F%252Fopen-dev.dingtalk.com%252Ffe%252Fapp%253Fhash%253D%252523%25252FcreateClawRobot%2526user_code%253D56R4-CZHJ-Q8R8%2523%252FcreateClawRobot&response_type=code&client_id=dingbakuoyxavyp5ruxw&scope=openid+corpid#/) in advance.

* At present, the connector supports iDA and general scenario agents, and the old analysis agent needs to be bound according to the corresponding steps.


<span id="dfd7f5d0"></span>
# Step 1: Enter the DingTalk connector


1. Log in to iDA and enter the target agent. Click Connectors in the left navigation bar.

2. Find **DingTalk** in the list of connectors. Click the **Connect** button to enter the authorization process.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/728e4e2868f042cc9693816028b735ee~tplv-goo7wpa0wc-image.image) </span>

<span id="3d623c31"></span>
# Step 2: Complete the DingTalk authorization


1. On the DingTalk authorization page that pops up, use the DingTalk App to scan the QR code or enter account and password, and confirm the login.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c354f8b069546a8bf1023788104424f~tplv-goo7wpa0wc-image.image) </span>

2. After successfully logging, on the Create OpenClaw DingTalk robot page, you can fill in the robot name, description, and upload the icon, and click the Create button. After creation, the system will automatically complete the required permission configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1dcc2c522abe4e6bad8a2d60ee26ab91~tplv-goo7wpa0wc-image.image) </span>

3. After entering the OpenClaw robot creation page, properly save the Client ID and Client Secret. Client Secret is sensitive information. Do not publicly disseminate or write in non\-secure documents.

4. After returning to iDA, click the "Bot created, proceed to enable DingTalk permission" button, enter the DingTalk device authorization page, confirm the application and authorization code that requests access to the account, and click **Log in to the DingTalk account** to continue to complete the authorization.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de22bc42d33f48849ed4bf37c9fc0acf~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/333ba5bff1af421ba23b2af809df30bc~tplv-goo7wpa0wc-image.image) </span>

5. After the authorization is completed, iDA will pop up an "Authorization Successful" prompt on the connector page, indicating that the DingTalk account has been connected. You can return to iDA for Q&A and operate DingTalk messages, documents, calendars, and more.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f34520ba8bf475b8882ecfcf8153047~tplv-goo7wpa0wc-image.image) </span>


<span id="c17434df"></span>
# Step 3: Using DingTalk in iDA


1. After the authorization is completed, return to iDA page, and iDA displays a successful binding prompt. Click the Experience Now button to enter the iDA new conversation page for Q&A.

2. The text box will automatically fill with "Connect my DingTalk, help me:", you can enter the question in the text box, click the send button, and iDA will execute the corresponding task according to the problem.

3. Here is an example of use:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73dc8b5bcba1435eb7bdd2f0e6674f98~tplv-goo7wpa0wc-image.image) </span>

   After iDA creates a task, the DingTalk side will also receive the corresponding task result:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/851175166b0f4a68a03aeaed547154ba~tplv-goo7wpa0wc-image.image) </span>


<span id="6d768c27"></span>
# Common problem

During the use or authorization process, if you encounter the following problems, you can try the methods in the form to process.


|Question |Possible reason |Processing method |
|---|---|---|
|Authorization timeout |DingTalk authorization was not completed within 15 minutes. |Click "Reauthorize" to complete the authorization process again. |
|Show authorization exception |DingTalk side app deleted, permission change or authorization unavailable. |Click the DingTalk card to reconnect and follow the page prompts to complete the authorization. |

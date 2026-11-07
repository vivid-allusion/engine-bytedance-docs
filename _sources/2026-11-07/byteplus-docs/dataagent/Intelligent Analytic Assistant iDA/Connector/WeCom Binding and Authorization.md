---
title: "WeCom Binding and Authorization"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/WeCom_Binding_and_Authorization"
---

The WeCom connector is used to connect the iDA to the WeCom account. After completing the authorization, users can chat with iDA individually or in a group chat in WeCom, and use open capabilities such as messages, documents, schedules, meetings, and to\-dos within the scope of authorization. Through the WeCom connector, iDA can integrate collaborative content in WeCom into the scope of task processing and knowledge retrieval, helping users complete Q&A, information processing, and collaborative tasks in common office platforms.

This article will introduce the authorization process of the WeCom connector, how to use it, and how to handle authorization exceptions.

<span id="91717d21"></span>
# Prerequisite


* **iDA agent has been opened:**  You need to have a usable iDA agent first, and enter the conversation page of the corresponding agent;

* **Have a WeCom account and authorization authority:**  You need to have a WeCom account that can be logged in and used normally to complete the connector authorization;

* At present, the connector supports iDA and general scenario agents, and the old analysis agent needs to be bound according to the corresponding steps.


<span id="20f420d0"></span>
# Step 1: Enter the WeCom connector


1. Log in to the BytePlus console, select iDA, and enter the corresponding project. Find the corresponding agent in the project and click to enter.

2. In the left navigation bar of the agent Q & A interface, click Connector Options to enter the connector management page.

3. On Connector page, click the Connect button of WeCom to proceed to the authorization step.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a8f288af75141bfbeea2b01aca380fa~tplv-goo7wpa0wc-image.image) </span>

<span id="5f3fa766"></span>
# Step 2: Create intelligent robots and empower them

Click the Connect button, the system pops up the QR code interface, you need to use WeCom to scan the code and authorize the system.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/067a393f7d604ca185d7f7ce8193391c~tplv-goo7wpa0wc-image.image) </span>


1. After the QR code pops up, open WeCom, find the More button in the upper right corner of the message list, and scan the code.

2. After scanning the code, click the button to create an intelligent robot according to the system redirection.

3. Follow the system steps to authorize the capabilities that the robot can use. After clicking the Confirm Authorization button, the system automatically creates an intelligent robot and returns to the connector management page on the iDA side.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/950317a211014fc2a3c19e5542bb9c1e~tplv-goo7wpa0wc-image.image) </span>

<span id="8330e200"></span>
# Step 3: Connect WeCom in iDA


1. After the binding is successful, click use on the WeCom side, and the iDA side returns the binding result. You can click the Experience Now button to have a conversation in iDA. On the conversation page, the system will automatically fill in "Connect my WeCom, help me:", and you can have a conversation according to your actual needs.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a03d6b14a224de7b2da197fe5d54c94~tplv-goo7wpa0wc-image.image) </span>

2. An example of use is as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3385ebde84634964a33b379713665fdf~tplv-goo7wpa0wc-image.image) </span>


<span id="03b48fab"></span>
# Common problem

During the use or authorization process, if you encounter the following problems, you can try the processing methods in the form to try processing.


|Question |Possible reason |Processing method |
|---|---|---|
|QR code has expired |Have not completed scanning code in OR code valid period. |After refreshing the QR code, scan the code again to authorize. |
|Show authorization exception |WeCom side app deleted, permission change or authorization unavailable. |Click the WeCom card to reconnect and follow the page prompts to complete the authorization. |

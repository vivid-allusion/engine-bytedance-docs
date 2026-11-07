---
title: "General Events"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/General_Events"
---

The general event module can query and maintain the details of currently supported general events (except virtual events and circled events), and supports operations such as adding events, editing events, setting event status, and accepting event tracking. This article provides you with a hands\-on guide to the basic concepts and functions of general events.

<span id="_1-概述"></span>
# Basic concept


|Term |Concept introduction |
|---|---|
|Event |Describe a series of actions triggered by your users within the product (such as: clicking, swiping, visiting pages, etc.). Event collection is mainly achieved through in\-app event tracking, so it is also called "event tracking data". |
|Event properties |When an event is triggered, information such as the form and location of the event can be collected to describe the event, which is called event properties.<br><br>For example, the event property that starts playing a video can be properties related to the device used by the user, such as operating system, software version, software channel, Internet Protocol Address, etc.; it can also be business\-related video ID, video name, video classification, video label, etc. |
|Preset Events & Preset Properties |* Preset events: The events that come with the SDK provided by the system are uniformly configured by the system to report the timing.<br><br>* Preset properties: The event properties that come with the preset event. |


<span id="_2-功能介绍"></span>
# Operation entrance

After logging into the DataFinder product console, you can go to the General Events page by clicking **Data Management** \> **Metadata Management** \> **General Events** at the top.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3eb3b943033c42d686e8423ee742c098~tplv-goo7wpa0wc-image.image) </span>


* You can view a list of all general events under the current app on the current page, and click on the corresponding event name to view the event details. The filter criteria at the top help you quickly filter queries.

* Users with general event management privileges can also perform management operations such as modification, creation, and state modification of general events.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to manage general events, please contact your app administrator to open the "Data Management\-General Events\-Manageable" function permission for you. Users without permission can only view and cannot operate.   </div>
   

* The general event list only shows the accepted events, and the unaccepted events can be viewed and completed by clicking "Acceptance Events".

* Real\-time event tracking detection is a function that can detect and quickly verify whether the event tracking is correct and the data upload situation in real time; it supports multi\-terminal event tracking verification such as mobile end App (Android, iOS) and WeChat Mini Program.


<span id="db939d05"></span>
# View event details

<span id="0604131d"></span>
## Check the basic information

On the General Events page, you can view a list of all events, which also displays the event's display name, description, and other information. Click on the event name to see more details in the side page that pops up on the right.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0da0365052c44945a87949a2c9e083e3~tplv-goo7wpa0wc-image.image) </span>


* You can check whether the corresponding event is a preset event, what are the properties of the event, and so on.

* The current system has provided you with a large number of preset events and preset properties. It is recommended that you follow up the business requirements before data analytics. After planning the event tracking that needs to be reported for analysis, check whether the preset events have met the business requirements. If not, you can manually create custom events.


<span id="fe3a7a74"></span>
## View change history

DataFinder provides you with event tracking change history function (value\-added function). After clicking on a specific event, you can click the "Change History" tab on the side page that pops up on the right, where you can view the change log information of the current event.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The current change history function is a value\-added function. You need to purchase the "event tracking governance module" separately to use the event tracking blood function. For purchase consultation, you can contact BytePlus technical support staff or your account manager.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b18999f84b4943eeae072d7b0d5746c0~tplv-goo7wpa0wc-image.image) </span>

<span id="f461a8ec"></span>
## Check blood relations

DataFinder provides you with event tracking blood management function (value\-added function). After clicking on a specific event, you can click the "Blood Relationship" tab on the side page that pops up on the right, where you can view the chart/dashboard and user group associated with the current event.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The current event tracking bloodline function is a value\-added function. You need to purchase the "event tracking governance module" separately to use the event tracking bloodline function. For purchase consultation, you can contact BytePlus technical support staff or your account manager.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a7b516353f4421e9be00087f1c18cc3~tplv-goo7wpa0wc-image.image) </span>


* You can view a list of charts and kanban boards using the current event in "Chart Blood", and see if the usage is "direct reference" or "indirect reference". Click the link of the corresponding chart/kanban board to jump to the corresponding chart/kanban board.

* You can view the user groups that have used the current event in "Group Blood", and view the current latest number of users in the group, the number of queries in the past 30 days, etc. Click the corresponding group name to jump to the edit configuration page of the corresponding group.


More information on event tracking lineage can be found [Efficiency Improvement Function: Event Tracking Bloodline](https://docs.byteplus.com/docs/DataFinder/Efficiency_Improvement_Function_Event_Tracking_Bloodline).

<span id="73449844"></span>
## View/upload event tracking screenshots

DataFinder provides you with event tracking screenshots (additional purchase is required). If you have contacted BytePlus technical support to turn on this function switch, you can upload/view event tracking screenshots of the current event on the event details page.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The current event tracking screenshot function is a value\-added function. You need to buy the "event tracking governance module" separately before you can use it. For purchase consultation, you can contact BytePlus technical support staff or your account manager.</div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After uploading the event tracking screenshot, other personnel can quickly understand the corresponding operation of the current event in the application interface by viewing the event tracking screenshot, so that other personnel can quickly understand the specific meaning of the current event tracking.</div>


* <div data-tips="true" data-tips-type="tip">After opening the event tracking screenshot function, for Android, the follow\-up event tracking verification can also be done directly through the event tracking screenshot to quickly complete the verification, more about the event tracking screenshot introduction and use guidance can be found <a href="https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification#a8a39f0e">View and use event tracking screenshots</a>.</div>



<span id="206a10de"></span>
# Add and manage events

<span id="_2-1-新增事件"></span>
## New event

Support single new event, also support batch new, the operation guide is as follows.

<span id="9260fd92"></span>
### Single new event

Open the **metadata management \> general event** page, click the "New Event \> Single New Event" button in the upper right corner of the page, you can register the event information in the pop\-up window, and you can only submit one event at a time.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6432b0efd714c2192e4869e068a94a5~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Configuration instructions |
|---|---|
|Event name |Customize the event name of the new event. The configuration requirements are as follows:<br><br><br>* Event names must not duplicate existing or virtual event names.<br><br>* Event name naming convention: Start with a letter or number, followed by letters, numbers, underscores, dots, spaces, and dashes, for a total length of 1 to 255 characters.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After filling in the event name, you can click the intelligent fill below the event name. By filling in some event input information, DataFinder's AI Lab will automatically generate copy such as the display name and event description for you, which can be applied with one click to improve the efficiency of event creation.</div><br> |
|Display Name & Event Category & Event Description |* Presentation Name: It is recommended to fill in the event meaning, for example: click the submit button.<br><br>* Event classification: It is recommended to choose a classification related to the event application scenario.<br><br>* Event description: It is recommended to fill in the event reporting timing, business scenarios and other information, such as when the user clicks the submit button on the registration page to report. |
|Property settings |You can select event properties for the currently added event. Support for adding multiple event properties.<br><br><br>* The currently optional event property is a general event property (the property reported in params), that is, the property selected later is exclusive to the currently added event.<br><br>* Event public properties (properties reported in the header) are properties common to all events and do not need to be set in a single event. When you need to add public properties, you can go to the "Event Properties" page to create them. |


<span id="_2-1-2-批量登记"></span>
### Batch new event

If you need to register multiple events at once, you can use the Bulk New Event feature to increase operational efficiency, allowing you to submit up to 200 events at a time.

Open the **metadata management \> general event** page, click the "New Event \> Batch New Event" button in the upper right corner of the page, download the "event tracking design template" according to the interface prompts, fill in the event tracking information according to the format instructions and upload it.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bdeffd04e6f4418b9c40ee8246700cb4~tplv-goo7wpa0wc-image.image) </span>

<span id="e156e470"></span>
### Build on demand

If you have purchased the enable request management feature, you can create events directly based on the requirements you have created.


1. Open the **Metadata management \> General event** page and click the "New Event \> New on Demand" button in the upper right corner of the page.

2. The page will jump to the request management page, you can refer to [Request Management](https://docs.byteplus.com/docs/DataFinder/Request_Management) to create event tracking requirements and submit them online to complete the event creation.


<span id="_2-2-已有事件追加事件属性"></span>
## Modify the event properties of an event

If you need to append event properties to an event that has been reported, you can click the event name in the list, click "Add Event Properties" on the event details page to append properties to the current event; you can also delete custom properties that have been added to the event.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ca2f8b7a6fb44a29e8c518610abbcfa~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-编辑事件展示名、描述"></span>
## Edit event display name, description, category

It is recommended that you maintain the event display name and event description information in time, which will help application members better understand the business meaning of event tracking. Support for individual modifications or batch modifications.

At the same time, DataFinder's AI Lab provides you with intelligent diagnostic functions, which can intelligently diagnose and give copy optimization suggestions for display names and descriptions. You can apply optimization with one click.


* AI Lab metadata intelligent diagnosis:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The AI metadata diagnostic function has been discontinued <strong>from January 22, 2026</strong>. If you want to continue using it, you can contact your account manager.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81dde813d89b43b2a5c0acb5876c1eb4~tplv-goo7wpa0wc-image.image) </span>

* Manual modification and maintenance:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82ec237587094fc59905eddf9410adcb~tplv-goo7wpa0wc-image.image) </span>


<span id="735cf495"></span>
## Enable/disable/hide events

You can adjust the state of events in the list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b9e04f61f074e6da64ccd140d4bfb0a~tplv-goo7wpa0wc-image.image) </span>

The event processing logic in different states is as follows:


|**State** |**Whether to occupy the quota** |**Whether to build storage** |**Is it available in the product?**  |**Is it billed?**  |**Whether to support exporting data to local** |
|---|---|---|---|---|---|
|**Inactive** |No |No |No |No |No |
|**Active** |Yes |Yes |Yes |Yes |Yes |
|**Hide** |Yes |Yes |No |Yes |Yes |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">See details of currently supported metadata limit <a href="https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification#_3-%E4%B8%8A%E6%8A%A5%E6%95%B0%E6%8D%AE%E9%99%90%E5%88%B6">3. Restrictions on reporting data</a>.</div>


<span id="bad84ea8"></span>
## Bulk delete custom events

You can do bulk deletion after selecting multiple custom events on the event list page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e4ab0f4b6214a9eb63ace3735b6919f~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only delete custom registered metadata is supported, and preset events/properties do not support deletion.</div>


* <div data-tips="true" data-tips-type="warning">The deletion operation performed here only deletes the registered metadata, and does not directly delete the corresponding event data that has been reported to the database.</div>


* <div data-tips="true" data-tips-type="warning">After deletion, a subsequent event with the same name as the deleted metadata can be created, and the data type of the property can be different from before.</div>



<span id="ed4b39eb"></span>
# Acceptance and Verification

<span id="_2-5-验收事件"></span>
## Acceptance event

If you turn on the **event tracking warehousing verification** switch of the data in the **general settings** , then only the accepted events can be warehoused normally and the data can be queried, that is, the general event list only shows the accepted events, and the unaccepted events can be viewed and completed by clicking "Acceptance Events".

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">DataFinder data drop database logic see <a href="https://docs.byteplus.com/docs/DataFinder/Event_Property_Storage_Logic_Description">Event Property Storage Logic Description</a>.</div>



* The upper limit of the acceptance pending event list displays 1000 events, and the excess part cannot be checked.

* You can also manage the event blacklist on the "Data Acceptance" page, and add or remove the required events from the blacklist. There is no limit to the number of blacklist events.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c7523a5451b4138b4d3a653e2a20abb~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d34065f7b264d0ab54d99280e2b8c2e~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-6-验收埋点"></span>
## Validation event tracking

Real\-time event tracking detection is a function that can detect and quickly verify whether the event tracking is correct and the data upload situation in real time; it supports multi\-terminal event tracking verification such as mobile end App (Android, iOS) and WeChat Mini Program. Please refer to the relevant operation instructions .

<span id="_3-常见问题faq"></span>
# Common problem

<span id="1a3ffeff"></span>
## **Q1: How do I delete an event?** 


* The current DataFinder does not support deleting preset events. You can set the status of preset events that do not need to be used to "inactive".

* You can delete custom events.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f36da7bbca6042e895e8a487f4ef9005~tplv-goo7wpa0wc-image.image) </span>


<span id="e4046145"></span>
## **Q2: Why can't the event be found in the analysis module?** 

It is recommended to check the event status first, as inactive events cannot be used. It can be re\-active if required.

<span id="5e59fb46"></span>
## **Q3: How to add event properties?** 

If you need to add event properties to an existing event, you can click "Register event tracking" to add event properties to an existing event.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">General events can only register non\-event public properties, and event public properties need to be registered in the "Event Properties" module.</div>

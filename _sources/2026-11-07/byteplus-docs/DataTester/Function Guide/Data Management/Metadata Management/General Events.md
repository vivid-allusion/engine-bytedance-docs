---
title: "General Events"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/General-Events"
---

The general event module can query and maintain the details of currently supported general events (except virtual events and circled events), and supports operations such as adding events, editing events, setting event status, and accepting event tracking. This article provides you with a hands\-on guide to the basic concepts and functions of general events.

<span id="5fff8bb0"></span>
# Basic concept


|Term |Concept introduction |
|---|---|
|Event |Describe a series of actions triggered by your users within the product (such as: clicking, swiping, visiting pages, etc.). Event collection is mainly achieved through in\-app event tracking, so it is also called "event tracking data". |
|Event properties |When an event is triggered, information such as the form and location of the event can be collected to describe the event, which is called event properties.<br><br>For example, the event property that starts playing a video can be properties related to the device used by the user, such as operating system, software version, software channel, Internet Protocol Address, etc.; it can also be business\-related video ID, video name, video classification, video label, etc. |
|Preset Events & Preset Properties |* Preset events: The events that come with the SDK provided by the system are uniformly configured by the system to report the timing.<br><br>* Preset properties: Event properties that come with a preset event.<br><br><br>The preset event list supported by different data reporting terminals is different. Please refer to the preset event list for details [Preset Property Summary](https://docs.byteplus.com/docs/DataTester/Preset-Property-Summary). |


<span id="aee9b2b0"></span>
# Function introduction

Once logged into the DataTester product console, you can navigate to the General Events page by clicking **Metrics Management** \> **Metadata Management** \> **General Events** in the left navigation bar.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ba44e237bae4cfd96753f20dbfcf89b~tplv-goo7wpa0wc-image.image) </span>


* You can view a list of all general events under the current app on the current page, and click on the corresponding event name to view the event details. The filter criteria at the top help you quickly filter queries.

* Users with general event management privileges can also perform management operations such as modification, creation, and state modification of general events.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to manage general events, please contact your app administrator to open the "Data Management \- General Events \- Manageable" function permission for you. Users without permission can only view and cannot operate.   </div>
   

* The general event list only shows the accepted events, and the unaccepted events can be viewed and completed by clicking "Acceptance Events".

* Real\-time event tracking detection is a function that can detect and quickly verify whether the event tracking is correct and the data upload situation in real time; supports mobile end App (Android, iOS) and WeChat Mini Program.


<span id="747195c3"></span>
## View event details

On the General Events page, you can view a list of all events, which also displays the event's display name, description, and other information. Click on the event name to see more details in the side page that pops up on the right.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32663a11f4e0438297f10c9f6ddc0113~tplv-goo7wpa0wc-image.image) </span>


* You can check whether the corresponding event is a preset event, what are the properties of the event, and so on.

* The current system has provided you with a large number of preset events and preset properties. It is recommended that you follow up the business requirements before data analytics. After planning the event tracking that needs to be reported for analysis, check whether the preset events have met the business requirements. If not, you can manually create custom events.


<span id="9a16fa39"></span>
## New event

Support single new event, also support batch new, the operation guide is as follows.

<span id="0b9fa33e"></span>
### Single new event

Open the **metadata management \> general event** page, click the "New Event \> Single New Event" button in the upper right corner of the page, you can register the event information in the pop\-up window, and you can only submit one event at a time.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11233e4bf78f4767897de8a9c50efe6e~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Configuration instructions |
|---|---|
|Event name |Customize the event name of the new event. The configuration requirements are as follows:<br><br><br>* Event names must not duplicate existing or virtual event names.<br><br>* Event name naming convention: Start with a letter or number, followed by letters, numbers, underscores, dots, spaces, and dashes, for a total length of 1 to 255 characters. |
|Display Name & Event Category & Event Description |* Presentation Name: It is recommended to fill in the event meaning, for example: click the submit button.<br><br>* Event classification: It is recommended to choose a classification related to the event application scenario.<br><br>* Event description: It is recommended to fill in the event reporting timing, business scenarios and other information, such as when the user clicks the submit button on the registration page to report. |
|Property settings |You can select event properties for the currently added event. Support for adding multiple event properties.<br><br><br>* The currently optional event property is a general event property (the property reported in params), that is, the property selected later is exclusive to the currently added event.<br><br>* Event public properties (properties reported in the header) are properties common to all events and do not need to be set in a single event. When you need to add public properties, you can go to the "Event Properties" page to create them. |


<span id="0f5049b4"></span>
### Batch new event

If you need to register multiple events at once, you can use the Bulk New Event feature to increase operational efficiency, allowing you to submit up to 200 events at a time.

Open the **metadata management \> general event** page, click the "New Event \> Batch New Event" button in the upper right corner of the page, download the "event tracking design template" according to the interface prompts, fill in the event tracking information according to the format instructions and upload it.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a8594be4d1747df98a93c11df6bcf5e~tplv-goo7wpa0wc-image.image) </span>

<span id="58a1d47f"></span>
## Modify the event properties of an event

If you need to append event properties to an event that has been reported, you can click the event name in the list, click "Add Event Properties" on the event details page to append properties to the current event; you can also delete custom properties that have been added to the event.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f11433b99a8418082ec9745a9191891~tplv-goo7wpa0wc-image.image) </span>

<span id="35343fa7"></span>
## Edit event display name, description, category

It is recommended that you maintain the event display name and event description information in time, which will help application members better understand the business meaning of event tracking. Support for individual modifications or batch modifications.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce4a4b73462a4e8f9300b3b937a7c407~tplv-goo7wpa0wc-image.image) </span>

<span id="19b8ba95"></span>
## Active/inactive/hide events

You can adjust the state of events in the list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e372d50010a340189ae3a2da8e244333~tplv-goo7wpa0wc-image.image) </span>

The event processing logic in different states is as follows:


|**State** |**Whether to occupy the quota** |**Whether to build storage** |**Is it available in the product?**  |**Is it billed?**  |**Whether to support exporting data to local** |
|---|---|---|---|---|---|
|**Inactive** |No |No |No |No |No |
|**Active** |Yes |Yes |Yes |Yes |Yes |
|**Hide** |Yes |Yes |No |Yes |Yes |


<span id="33f30212"></span>
## Event approval

If you turn on the event tracking and warehousing verification of the data, only the accepted events can find the data, that is, the general event list only shows the accepted events, and the unaccepted events can be viewed and completed by clicking "Acceptance Events".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4150e82a1a414b41bf07d36a8dfaf555~tplv-goo7wpa0wc-image.image) </span>


* The upper limit of the acceptance pending event list displays 1000 events, and the excess part cannot be checked.

* You can also manage the event blacklist on the "Data Acceptance" page, and add or remove the required events from the blacklist. There is no limit to the number of blacklist events.


<span id="d641bd04"></span>
## Validation event tracking

Real\-time event tracking detection is a function that can detect and quickly verify whether the event tracking is correct and the data upload situation in real time; support mobile end App (Android, iOS), WeChat Mini Program, please refer to the relevant operation instructions [Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataTester/Event-Tracking-Real-Time-Verification).

<span id="0b56e5e6"></span>
# Common problem

<span id="db6f4ee9"></span>
## **Q1: How to delete an event?** 

The current Finder does not support deleting existing events. You can set the status of unwanted events to "inactive".

<span id="a7d12a89"></span>
## **Q2: Why can't the event be found in the analysis module?** 

It is recommended to check the event status first, as inactive events cannot be used. It can be re\-active if required.

<span id="aa701bae"></span>
## **Q3: How to add event properties?** 

If you need to add event properties to an existing event, you can click "Register event tracking" to add event properties to an existing event.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">General events can only register non\-event public properties, and event public properties need to be registered in the "Event Properties" module.</div>

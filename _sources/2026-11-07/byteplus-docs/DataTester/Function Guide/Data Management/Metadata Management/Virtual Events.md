---
title: "Virtual Events"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Virtual-Events"
---

DataTester provides you with the "virtual event" function. You can combine multiple general events in DataTester into virtual events through certain logical relationships, and then perform user behavior analysis through virtual events, which is convenient for you to manage and view the combination of conventional composite events.

<span id="07b2c19e"></span>
# Application scenario

The current common scenario is: I want to see the number of deduplicate users who have experienced event A or event B. For example, the number of deduplicated users who viewed page A or page B.

At this point, a virtual event is required: it indicates that either event A or event B occurs.

<span id="5e3d4777"></span>
# Instructions for use

<span id="8de332cb"></span>
## Go to the virtual event list page

After logging in and entering the DataTester console, click **Data Management** \> **Metadata Management** \> **Virtual Events** in the left navigation bar to enter the virtual event list page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d9866cde53941e29ffbecc31db37aa2~tplv-goo7wpa0wc-image.image) </span>


* When clicking to enter the "Virtual Events" page, a list of all created virtual events is displayed by default;

* The list can be filtered by "event name" and "event display name";


<span id="f73f013d"></span>
## Create a virtual event


1. Click New Virtual Event in the upper right corner of the page.

2. In the pop\-up Create Virtual Event page, fill in the corresponding information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d6900067d954a50a80a4f474cee0f0f~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Virtual Event Name & Presentation Name |Customize the name and display name of the virtual event to identify the virtual event, which is easy to find and use when using the virtual event later. |
   |Combined General Events |Select the general events to be combined for the virtual event to be created.<br><br><br>* You can select the corresponding general events based on actual business analysis needs, and support the configuration of filter filters for each selected event.<br><br>* The relationship between the selected multiple general events is or, that is, any hit to a general event indicates that the conditions are met, and the virtual event will be triggered. |
   


<span id="fc5fca97"></span>
## Using virtual events

When creating an indicator, when selecting an indicator event, click to select an event of the "Virtual Event" type. Here is an example of creating a UBA event metric to illustrate the application of virtual events.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f00ff9dc1b04770b2ea553493b69c5e~tplv-goo7wpa0wc-image.image) </span>

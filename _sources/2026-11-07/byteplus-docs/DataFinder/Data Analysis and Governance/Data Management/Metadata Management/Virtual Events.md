---
title: "Virtual Events"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Virtual_Events"
---

DataFinder provides you with the "virtual event" function. You can combine multiple general events in DataFinder into virtual events through certain logical relationships, and then perform user behavior analysis through virtual events, which is convenient for you to manage and view the combination of conventional composite events.

<span id="_1-概念介绍"></span>
# Application scenario

The current common scenario is: I want to see the number of deduplicate users who have experienced event A or event B. For example, the number of deduplicated users who viewed page A or page B.

At this point, a virtual event is required: it indicates that either event A or event B occurs.

<span id="_3-使用说明"></span>
# Instructions for use

<span id="_3-1-虚拟事件列表页"></span>
## Go to the virtual event list page

After logging in and entering the DataFinder console, click **Data Management** \> **Metadata Management** \> **Virtual Events** in the top navigation bar to enter the Virtual Events List page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/871f00d940354c19940cb026d27f5756~tplv-goo7wpa0wc-image.image) </span>


* When clicking to enter the "Virtual Events" page, a list of all created virtual events is displayed by default;

* The list can be filtered by "event name", "event description", and "creator", and the event name and description support fuzzy filtering;


<span id="_3-2-创建新的虚拟事件"></span>
## Create a virtual event


1. Click New Virtual Event in the upper right corner of the page.

2. In the pop\-up Create Virtual Event page, fill in the corresponding information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0afd399873114b698434b8af74a8e7da~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Virtual Event Name & Presentation Name |Customize the name and display name of the virtual event to identify the virtual event, which is easy to find and use when using the virtual event later. |
   |Combined General Events |Select the general events to be combined for the virtual event to be created.<br><br><br>* You can select the corresponding general events based on actual business analysis needs, and support the configuration of filter filters for each selected event.<br><br>* The relationship between the selected multiple general events is or, that is, any hit to a general event indicates that the conditions are met, and the virtual event will be triggered.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you need to combine a large number of events, you can also add events in batches, up to 100 events.</div><br> |
   |Visible range |Configure whether the visibility of virtual events created is visible only to yourself or to everyone.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The default setting for existing created virtual events is "Everyone", and the creator or administrator can modify the configuration of the visible scope.</div><br> |
   


<span id="_3-3-如何选择虚拟事件"></span>
## Using virtual events

After the virtual event is created, you can use the virtual event for user behavior analysis.


* Event selection for event analysis, retention analysis, conversion analysis pages.

* When selecting an event, you can see the type of event and select the virtual event that has been created. Take event analysis as an example:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa23e3873b704a5ba2caf6088e5014d6~tplv-goo7wpa0wc-image.image) </span>

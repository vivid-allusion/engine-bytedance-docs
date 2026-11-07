---
title: "Event Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Event_Properties"
---

Properties are used to describe the dimensional information when the event occurs, including user information (user_id), device information (app version, device number, ip address, device model, etc.), business custom information (custom parameters reported to params), etc. Properties typically include event properties and user properties. This article introduces the classification types and operation points of event properties.

<span id="_1-概述"></span>
# Background information

<span id="17298cb6"></span>
## Basic concept


|Term |Concept introduction |
|---|---|
|Event |Describe a series of actions triggered by your users within the product (such as: clicking, swiping, visiting pages, etc.). Event collection is mainly achieved through in\-app event tracking, so it is also called "event tracking data". |
|Event properties |When an event is triggered, information such as the form and location of the event can be collected to describe the event, which is called event properties.<br><br>For example, the event property that starts playing a video can be properties related to the device used by the user, such as operating system, software version, software channel, Internet Protocol Address, etc.; it can also be business\-related video ID, video name, video classification, video label, etc. |
|Preset Events & Preset Properties |* Preset events: The events that come with the SDK provided by the system are uniformly configured by the system to report the timing.<br><br>* Preset properties: The event properties that come with the preset event.<br><br><br>The preset event list supported by different data reporting terminals is different. Please refer to the preset event list for details [Preset Property Summary Table](https://docs.byteplus.com/docs/DataFinder/Preset_Property_Summary_Table). |


<span id="2c6c3223"></span>
## Event property classification

Event properties can usually be divided into general event properties and event public properties.


|Event property classification |Event Properties Application Description |Data reporting location |
|---|---|---|
|General event properties |* Usually referred to simply as event properties, different events have different event properties, and the same event can define multiple event properties.<br><br>* Take the "play video" event as an example, it contains the following event properties: enter_from (page where the action took place), video_id (video id), etc. |Usually when data is reported, event properties are reported in Params. |
|Event public property |* Refers to a general property that is reported on every event.<br><br>* For example, the DataFinder SDK presets the event public property field of the Device Information class into the Header as a public property for all events. |Usually when data is reported, the event public properties are reported in the header. |


<span id="_2-功能说明"></span>
# Function introduction

<span id="_2-1-新增事件属性"></span>
## Add event properties

You can register event properties when registering event tracking (general events), or you can register event properties separately. If you need to register event properties separately or for event public properties, you can do the following:


1. Select **Data Management \> Metadata Management \> Event Properties** to enter the Event Properties page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/521c475d2fe24621b863679cea78fed6~tplv-goo7wpa0wc-image.image) </span>

2. Click the **Add Event Properties** button to pop up the Add Event Properties side\-pull window. After setting the relevant information, click the **OK** button to complete the Add Event Property.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e642bc6a73c4266b435008ed0c31bff~tplv-goo7wpa0wc-image.image) </span>

   * DataFinder AI Lab provides you with intelligent filling capabilities. After completing the property name, you can click the intelligent filling below. After filling in part of the input information, AI Lab will automatically generate and fill in the display name, data type, and description fields for you.

   * If you register a general event property (params), do not check the **event public property** selection box below, directly select the **associated event** drop\-down box that requires the property to be associated with a specific event (there are events that report this property), if the event is not associated, the event property cannot be used when querying the event.

   * If you register the event public property (header), be sure to check the **event public property** , this does not need to be associated with a specific event. Each event can use event public properties.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Be specific when naming event properties, and use generalized parameter names with caution. Counterexamples: such as time (what time? is timestamp or duration?), name (what's the name?); positive example: such as the order time, it is recommended to name it order_time.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the business meaning is the same, try to reuse the fields that have been defined to avoid flooding the system with fields after arbitrary definition.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The DataFinder SDK has preset common event properties such as device and time, eliminating the need for repeated registration. See the list of preset events for details <a href="https://docs.byteplus.com/docs/DataFinder/Preset_Property_Summary_Table">Preset Property Summary Table</a>.   </div>
   


<span id="_2-2-上传字典"></span>
## Upload dictionary

The dictionary information is used to describe the business meaning translation value corresponding to the event property value, for example: the event property user_is_login, when value = 1 indicates that the user is currently logged in, and when value = 0 indicates that the user is currently not logged in.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After the dictionary setting is completed, the dictionary value can be used for data filtering or grouping display of query results in subsequent data analytics, which improves the operation experience of data analytics.</div>


* <div data-tips="true" data-tips-type="warning">Dictionary values cannot be directly used for index calculation (e.g. total value, average value, maximum value, minimum value, PCT90). When performing index calculation in analysis tools, the original value of the event property needs to be used for calculation, and dictionary value calculation is not supported.</div>



<div data-tips="true" data-tips-type="warning">For more information about the dictionary, see <a href="https://docs.byteplus.com/docs/DataFinder/Effeciency_Dimensional_Dictionary">Effeciency: Dimensional Dictionary</a>.</div>


Operation diagram:

Click the "Upload" button in the **dictionary** column of a message in the list, and you can upload the dictionary table of the current property in the pop\-up window.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be3f57aff3ce46e4a1b4ddb36245d97b~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-验收属性"></span>
## Acceptance Property

The event property list only displays the accepted/registered event properties. For unaccepted properties, you can click the "Acceptance Properties" button to view and complete the acceptance on the "Data Acceptance" page.

You can also manage the event property blacklist on the "Data Acceptance" page, adding or removing required event properties from the blacklist.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18eb8532457040309fab7dcfcf58ca4d~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c2b120bf431459a9894909d7f01eca8~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-修改属性数据类型"></span>
## Modify property data type

If you previously registered the wrong data type or changed to a new type, you can modify the data type field in the list.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Change types are divided into compatible and incompatible changes. Large types transfer historical data to small types without losing historical data (such as string \- \> int), and small types transfer historical data to large types (such as int \- \> float). Please choose your data type carefully.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc6e9e06b7a640aca91671b071e19724~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-批量编辑展示名、属性描述"></span>
## Batch editing display name, property description

If you want to complete the information in batches, you can use DataFinder's AI Lab intelligent diagnosis and one\-click optimization, or you can filter out the events with empty display names and property descriptions, package and export them into csv format documents, fill in the csv documents completely and click the **Modify Information** button to upload and import, and realize batch modification/registration of display and description information.


* AI Lab Intelligent Diagnosis Optimization

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2feea0ff0314c8d8be822de29eb8475~tplv-goo7wpa0wc-image.image) </span>

* post\-export optimization manually

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd153fd74c7744a991757dd9d8887554~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The batch import function only supports modifying the display name and property description, and other fields do not support batch modification.   </div>
   

<span id="63ba3c07"></span>
## Bulk removal of custom event properties

You can perform bulk deletion after selecting multiple custom event properties on the event properties list page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3b1f4b7c21e467eb50c1627e55f04b2~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only delete custom registered metadata is supported, and preset event properties do not support deletion.</div>


* <div data-tips="true" data-tips-type="warning">The deletion operation performed here only deletes the registered metadata, and does not directly delete the corresponding event property data that has been reported to the database.</div>


* <div data-tips="true" data-tips-type="warning">After deletion, an event property with the same name as the deleted metadata can be created later, and the data type of the property can be different from before.</div>



<span id="_3-常见问题faq"></span>
# Frequently Asked Questions FAQ

<span id="_3-1-如何删除事件属性？"></span>
## Q1 How to delete event properties?


* Deleting the preset event property is not supported. If you no longer need the property, you can modify the state to disable it. The disabled event property will no longer build data and cannot be viewed in the analysis module.

* Custom event properties are optional after bulk deletion.


<span id="_3-2-事件属性和用户属性的区别是什么？"></span>
## Q2 What is the difference between event properties and user properties?

Event properties record various dimensional information describing the event, such as operating system, software version, software channel, etc., and can also be article ID, article title, article author, etc.; user properties are properties of the user's own state, such as gender, age, etc.

<span id="_3-3-事件属性验收和新增区别是什么？"></span>
## Q3 What is the difference between event property acceptance and addition?

The effect of adding event properties is the same as that of accepting event properties. Both register event property information in the Data Management\-Event property List so that it can be used in advanced analysis. The difference is that the acceptance property needs to report the data first, and the system can only accept it after detecting the report; while the new event property can be registered before and after the data is reported, you can register the event property in the event tracking design stage, so that the event tracking does not need to be accepted after going online, and can be used directly.

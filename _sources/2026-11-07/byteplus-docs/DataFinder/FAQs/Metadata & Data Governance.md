---
title: "Metadata & Data Governance"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Metadata_Data_Governance"
---

<span id="9dbca3c9"></span>
# Create events/event properties/user properties/virtual events/virtual properties, etc

<span id="e1d1541d"></span>
## Create a virtual event error in SaaS\-Cloud Native: What ServiceableStubError?

If this type of error occurs when trying to create a virtual event, it may be because the created virtual event has the same name as an existing event, which violates the constraints on the uniqueness of event names in the application.

<span id="9b2e6a4f"></span>
# Modify custom events/properties

<span id="bb773f05"></span>
## What is the effect of changing the type of an event property from float to string?

The details are as follows:

(1) This property of historical data is displayed as null

(2) Uploading new data of string type will be displayed normally

(3) Uploading new data of non\-string type will be corrected string, that is, four operations cannot be performed

<span id="51b85f35"></span>
## Attribute type int, after changing to string, what is the impact on the data?

Allows modification, but the historical data can no longer be queried, and then changed back to the original type, it is still available. For example, string\- \> int\- \> string.

<span id="c6d4b491"></span>
## The events are all English names. Can I add Chinese remarks?

Sure. The original English name of the event is displayed by default. You can add a Chinese "event description" to the event by clicking the "Management\-Data Management" function of the navigation bar. After saving, the description content will be displayed together with the event name in the analysis function, which is convenient for understanding the meaning of the event.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ebaa5c692424404b8b7f9b075f1b4cf~tplv-goo7wpa0wc-image.image) </span>

<span id="3e253a15"></span>
## How to batch modify the Chinese display name of an event?

On the Data Management \> metadata Management \> General Events page, there is a check box to the left of the event name. Select the event name that needs to be modified in batches, and then select Export. After exporting, update the event display name and upload it again.

<span id="361f1cdc"></span>
## I have successfully reported the event and generated user_id data. Can I modify the userid now?

No. user_id generated will be associated with the user unique identity ssid, so modification is not supported. You can only report a new user_id and associate a new ssid.

&nbsp;

&nbsp;

<span id="90d8473b"></span>
# Data governance and alerting

<span id="f12b431c"></span>
## The alarm push DingTalk method is sent normally, but the mailbox cannot receive it.

You need to configure the sending mailbox at the finder server level to send emails, otherwise there will be an error prompt.

<span id="6ac473ec"></span>
# Other

<span id="3c8438cd"></span>
## On the metadata management page (event properties, general events, etc.), it is found that the registrant is "runninginfo". What does this mean?

Taking the **metadata management** \> **event properties** page as an example, you might see an attribute on the interface where the registrant is "admin".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21bf0e8433e447aaa8bd93848ed19846~tplv-goo7wpa0wc-image.image) </span>

This type of property is automatically registered by the system for you. DataFinder provides some events and properties for you to the DataFinder metadata service. If you want to collect and report some custom events and properties:


* It is recommended that you log in to the metadata page of the DataFinder console to manually register (create new events/properties) after planning all event tracking requirements.

* If you do not complete the registration on the DataFinder metadata page in advance, but directly collect and report to the DataFinder, the DataFinder will automatically re\-register you into the metadata. In such scenarios, the registrant of such data re\-registered by the system will be marked as "runninginfo".


<span id="6063dd72"></span>
## Is it supported to delete collected data in a SaaS\-cloud native (cloud hosting) scenario? How to delete?

In the SaaS\-cloud native (cloud hosting) scenario, the collected data will be stored in your ByteHouse database. You can log in and enter the ByteHouse database where the data is stored to delete the corresponding data.


* Data collected by DataFinder is usually stored in the events, users, items and other tables. For a detailed introduction to the relevant data table and table fields, please refer to [1.2 Table field description](https://docs.byteplus.com/docs/DataFinder/Custom_SQL_Query#_1-2-%E5%AD%97%E6%AE%B5%E8%AF%B4%E6%98%8E)the data table structure and field description before you delete the data.

* ByteHouse supports data deletion directly in the ByteHouse console interface. It is also recommended that you preview and confirm the data to be deleted in the console in this way, and then delete it after confirming that it is correct. See [ByteHouse help documentation ](https://www.volcengine.com/docs/6517/76334#%E5%88%A0%E9%99%A4%E8%A1%A8)for management of interface table data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/142ba85d0a67469fab90e59ff8810566~tplv-goo7wpa0wc-image.image) </span>

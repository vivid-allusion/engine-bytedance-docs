---
title: "User Properties"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/User-Properties"
---

Properties are used to describe the dimensional information when the event occurs, including user information (user_id), device information (app version, device number, ip address, device model, etc.), business custom information (custom parameters reported to params), etc. Properties typically include event properties and user properties. This article will introduce you to the main points of operation for user properties.

<span id="a149e648"></span>
# Basic concept


|Term |Concept introduction |
|---|---|
|User |The subject of the event behavior, currently supports the use of user_id, ssid, device_id to uniquely identify a user, see details [Supported User Unique Identifiers](https://docs.byteplus.com/docs/DataTester/Supported-User-Unique-Identifiers). |
|User properties |* Properties of the user's own state that are independent of behavior, such as age, gender, etc.<br><br>* Properties related to behavior that do not change or change frequently, such as registration time, VIP level, last payment time, etc. |
|Preset user properties |Preset user properties: User properties preset by the SDK.<br><br>The preset event list supported by different data reporting terminals is different. Please refer to the preset event list for details [Preset Property Summary](https://docs.byteplus.com/docs/DataTester/Preset-Property-Summary). |


<span id="e0a4ee94"></span>
# Function introduction

<span id="13e079c6"></span>
## Add user properties

If you need to register user properties separately, you can do the following:


1. Select **Data Management \> Metadata Management \> User Properties** to enter the User Properties page.

2. Click the **Add User Properties** button to pop up the Add User Properties side\-pull window. After setting the relevant information, click the **OK** button to complete the Add User Properties.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0fe9df1bc82b4af8984ce17e2d90dcf6~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Property name, display name |* Be specific when naming user properties, and use generalized parameter names with caution.<br><br>* If the business meaning is the same, try to reuse the already defined fields to avoid flooding the system with fields after arbitrary definition.<br><br>* The DataTester SDK already has common user properties preset, eliminating the need for duplicate registration. See the list of preset events for details [Preset User Properties](https://docs.byteplus.com/docs/DataTester/Preset-User-Properties). |
   |Data type |Select the data type of the user property in the drop\-down box. Currently, int, string, float, datetime, list, and version are supported.<br><br><br>* The selected user property type must be consistent with the data type of the user property reported later, otherwise the data may not be properly stored.<br><br>* Reported data type and the data type of the database correspondence and detailed data format requirements see [Supported Data Formats (Custom Events/Properties)](https://docs.byteplus.com/docs/DataTester/Supported-Data-Formats-Custom-Events-Properties). |
   |Computational logic |Currently supports on\-demand options to **calculate all values** or **calculate final values**.<br><br><br>* Calculate all values: Analyze all the values that appear during the change of this property. Example: If the property is "Member Category", the user upgrades from "Ordinary Member" to "VIP" on a certain day, and "VIP" is the latest value, then the access, purchase and other events that occur in user a will be classified as "Ordinary User" before the change, and will be classified as "VIP" on the day of the change and after the change.<br><br>* Calculate final value: Analyze only the final value of the property change. Example: For example: if the property is "Member Category", the user upgrades from "Ordinary Member" to "VIP" on a certain day, and "VIP" is the latest value, then all events such as visits and purchases that have occurred in user a's history will be attributed to "VIP". |
   |Property description |Custom property descriptions for easy identification of user properties. |
   


<span id="2bbae74d"></span>
## Property approval

The user property list only displays the accepted/registered user properties. For unaccepted properties, you can click the "Property approval" button to view and complete the acceptance on the "Data Acceptance" page.

You can also manage the user property blacklist on the "Data Acceptance" page, and add or remove the required user properties from the blacklist.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8d4c3221e2e47dbb8a4234a1ef49768~tplv-goo7wpa0wc-image.image) </span>

<span id="7854b1b8"></span>
## Modify property data type

If you previously registered the wrong data type or changed to a new type, you can modify the data type field in the list.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Change types are divided into compatible and incompatible changes. Large types transfer historical data to small types without losing historical data (such as string \- \> int), and small types transfer historical data to large types (such as int \- \> float). Please choose your data type carefully.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59591a67684a484ab4de5d5bfe682458~tplv-goo7wpa0wc-image.image) </span>

<span id="b10281c0"></span>
## Batch editing display name, property description

If you want to modify the display name or properties of a user property, you can:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6151a7580f84f9795ddaf588e1c5bac~tplv-goo7wpa0wc-image.image) </span>


* Single modification: directly click the edit or add button after a property to modify the display name or description of the user property.

* Batch Modification: After selecting multiple user properties to be modified, click the **Batch Export** button at the bottom. After the local modification is completed, click the **Batch Modification** button at the top to import the modification results in batches.

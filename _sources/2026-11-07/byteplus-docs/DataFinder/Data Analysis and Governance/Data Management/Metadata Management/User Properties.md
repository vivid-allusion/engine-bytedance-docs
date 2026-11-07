---
title: "User Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/User_Properties"
---

Properties are used to describe the dimensional information when the event occurs, including user information (user_id), device information (app version, device number, ip address, device model, etc.), business custom information (custom parameters reported to params), etc. Properties typically include event properties and user properties. This article will introduce you to the main points of operation for user properties.

<span id="da9a726f"></span>
# Basic concept


|Term |Concept introduction |
|---|---|
|User |The subject of the event behavior currently supports the use of user_id, ssid, device_id to uniquely identify a user , see for details [Supported User Unique Identifiers](https://docs.byteplus.com/docs/DataFinder/Supported_User_Unique_Identifiers). |
|User properties |* Properties of the user's own state that are independent of behavior, such as age, gender, etc.<br><br>* Properties related to behavior that do not change or change frequently, such as registration time, VIP level, last payment time, etc. |
|Preset user properties |Preset user properties: User properties preset by the DataFinder SDK.<br><br>The preset event list supported by different data reporting terminals is different. Please refer to the preset event list for details [Preset Property Summary Table](https://docs.byteplus.com/docs/DataFinder/Preset_Property_Summary_Table). |


<span id="476faf3f"></span>
# Function introduction

<span id="533b53ea"></span>
## Add user properties

If you need to register user properties separately, you can do the following:


1. Select **Data Management \> Metadata Management \> User Properties** to enter the User Properties page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59fd088a995e4d5e804914a877cb2979~tplv-goo7wpa0wc-image.image) </span>

2. Click the **Add User Properties** button to pop up the Add User Properties side\-pull window. After setting the relevant information, click the **OK** button to complete the Add User Properties.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f95d17995a014430a6726d504a707a64~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Property name, display name |DataFinder AI Lab provides you with intelligent filling capabilities. After completing the property name, you can click the intelligent filling below. After filling in part of the input information, AI Lab will automatically generate and fill in the display name, data type, and description fields for you.<br><br><br>* Be specific when naming user properties, and use generalized parameter names with caution.<br><br>* If the business meaning is the same, try to reuse the fields that have been defined to avoid flooding the system with fields after arbitrary definition.<br><br>* The DataFinder SDK already comes with common user properties, eliminating the need for duplicate registration. See the list of preset events for details [Preset Property Summary Table](https://docs.byteplus.com/docs/DataFinder/Preset_Property_Summary_Table). |
   |Data type |Select the data type of the user property in the drop\-down box. Currently, int, string, float, datetime, list, and version are supported.<br><br><br>* The selected user property type must be consistent with the data type of the user property reported later, otherwise the data may not be properly stored.<br><br>* Reported data type and the data type of the database correspondence and detailed data format requirements see [Supported Data Formats and Event/Property Classification](https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification). |
   |Property description |Custom property descriptions for easy identification of user properties. |
   


<span id="0b3dee05"></span>
## Upload dictionary

Dictionary information is used to describe the user property value corresponding to the value of the business meaning translation value, for example: user property user_is_login, when value = 1 indicates that the user is currently logged in, value = 0 indicates that the user is not currently logged in.

Operation diagram:

Click the "Upload" button in the **dictionary** column of a message in the list, and you can upload the dictionary table of the current property in the pop\-up window.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4000ad2fee145eaa112523699526825~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcd735bfbc6f4d9e9591c9eb1e539056~tplv-goo7wpa0wc-image.image) </span>

<span id="1a957edf"></span>
## Acceptance Property

The user property list only displays the accepted/registered user properties. For unaccepted properties, you can click the "Acceptance Properties" button to view and complete the acceptance on the "Data Acceptance" page.

You can also manage the user property blacklist on the "Data Acceptance" page, and add or remove the required user properties from the blacklist.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/085baebded914ed88a32674210a58cc5~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5b1a5a14a3f4d95b8512aa615a74342~tplv-goo7wpa0wc-image.image) </span>

<span id="fd8ef13f"></span>
## Modify property data type

If you previously registered the wrong data type or changed to a new type, you can modify the data type field in the list.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Change types are divided into compatible and incompatible changes. Large types transfer historical data to small types without losing historical data (such as string \- \> int), and small types transfer historical data to large types (such as int \- \> float). Please choose your data type carefully.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f651062481bf409bbfe363c0d769ba12~tplv-goo7wpa0wc-image.image) </span>

<span id="6e82f9cf"></span>
## Batch editing display name, property description

If you want to complete the information in batches, you can use DataFinder's AI Lab intelligent diagnosis and one\-click optimization, or you can filter out the events with empty display names and property descriptions, package and export them into csv format documents, fill in the csv documents completely and click the **Modify Information** button to upload and import, and realize batch modification/registration of display and description information.


* AI Lab Intelligent Diagnosis Optimization

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28771b52d10748668bb103109bc5395e~tplv-goo7wpa0wc-image.image) </span>

* Post\-export optimization manually

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9fdc5f3cd5242bdaa3fe6c80e68c9fc~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The batch import function only supports modifying the display name and property description, and other fields do not support batch modification.   </div>
   

<span id="b07741f3"></span>
## Bulk removal of custom user properties

You can perform bulk deletion operations after selecting multiple custom user properties on the User Properties List page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95d25ed8dfee406fa949341e5641744e~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only delete custom registered metadata is supported, and preset user properties do not support deletion.</div>


* <div data-tips="true" data-tips-type="warning">The deletion operation performed here only deletes the registered metadata, and does not directly delete the corresponding user property data that has been reported to the database.</div>


* <div data-tips="true" data-tips-type="warning">After deletion, a user property with the same name as the deleted metadata can be created later, and the data type of the property can be different from before.</div>

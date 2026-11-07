---
title: "Subject File"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Subject_File"
---

<span id="_1-功能概述"></span>
# 1. Function Overview

In this module, users can view and manage subject attributes, behavior timestamps, business detail data. Define data archive fields as interpretable data features under different subjects for business applications. Include:


* Subject Attribute Configuration: Describing the unique characteristics of the subject, such as age/gender;

* Behavior Event Configuration: Subject's behavior logs, recording specific behavior events and their contents (attributes);

* Business Detail Configuration: Subject's business data details, including detail or summary data in certain scenarios, such as sales data.


<span id="bb73beb0"></span>
# 2. Prerequisites

Administrator and individuals with permission to view or add/edit/delete data archives in Project Center\-Module\-Data Archive Management can use this module.

<span id="0fe80256"></span>
# 3. Usage Example


|**Concept** |**Explanation** |**Mapping relationships with segmentation components example** |
|---|---|---|
|Subject Attribute |The most basic feature information that describes the subject's ownership/address/interests/preferences etc. is the most fundamental information to build the subject's portrait, providing the content of "Who am I," such as identity, gender, address fields, etc. |In the **User Segmentation**, select customers of different city types:<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f0515fcff57c457a8acdb332987a743b.png) </span> |
|Behavioral Event |Behavioral events are data content constructed logically from Event + User, providing behavioral data of "what time I did what, and what results occurred," thus requiring a fixed data structure for behavioral events, defining event names and event attributes. |Select customers who clicked on products from July 5th to July 14th more than 100 times, and the shop names related to the products contain "phone."<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4f9962bb0a8a351d823963e02a0fc996.png) </span> |
|Business Details |Data recording the actual business process, providing data on business factual processes beyond behaviors, showing "what time created or produced business results." |Based on business consumption records, select customers whose consumption amount from July 5th to July 14th is more than 100 and whose membership type is ordinary maintenance customers and ordinary development customers.<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ec76c1f485052d85711b55cffbc56e93.png) </span> |


<span id="7ebd7904"></span>
# 4. Operation Instructions

<span id="b8c302d9"></span>
## 4.1 Subject Property Configuration

> It is the unique feature of the subject, such as age/gender.


Display subject property information, including field name, display name, description, source table, data type, etc., where display name and description can be modified.

Support finding corresponding subject property information through search keywords, and also support quick filtering by status.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f28534bd8d9eb77fc00fa26f24b9d51c.png) </span>

Support single or batch set **Enable/Disable/Not Display** operations:


* Enable: it means to activate the normal use of the corresponding subject property.

* Disable: it means the corresponding subject property is not allowed to be used. Disabling the field will make downstream services unavailable, so operate with caution.

* Not Display: After changing fields like **import tags, calculation tags, sorting tags** in data archives to "**Not Display**", errors will occur in subsequent calculations for these tags, while other tags remain unaffected.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a3de1c507348b6d6aeab6b2e099b8a35.png) </span>

Click the **Configuration** button to support linking dimension tables for subsequent association queries.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b44017c0af9dc71583070f28f3ab7396.gif) </span>

Click the **Batch Upload Display Name** in the upper right corner to batch modify the display names of corresponding main entity attributes by uploading files, which can be applied in modules such as tags/clusters/individual portraits. For example, when creating cluster selection rules, the modified display name will be displayed when selecting main entity attributes.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9292a0119f35bb5e4bb239fab2853ead.png) </span>

On the upload page, users can upload files by dragging and dropping or clicking the upload button (provide a template for reference):

Notice:


* Supported file extensions for upload: .xlsx .csv.

* Only support uploading one file, with a size of ≤100M.

* The headers must be "Attribute Name," "Display Name," "Field Description," "Source Table."

* Start uploading field values from the second row by default.

* Only read data from the first sheet.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_986983c1765024d7e2eaafc6f9bb28ee.png) </span>

<span id="ed0ec825"></span>
## 4.2 Behavior Event Configuration

> The behavior log of the subject records specific behavioral events and the content (attributes) of the events.


<span id="416f51ee"></span>
### 4.2.1 **General Events**

**Application Scenario:**  The names of events in behavioral events are mostly in English. Through this function, you can configure the corresponding Chinese name and description for the event, making it easier for business colleagues to understand when creating tags.

<span id="242d6d7f"></span>
#### 4.2.1.1 **View Event Information List**

Display event information of behavioral data, including event name, display name, event description, source, event status, etc. Support finding corresponding event information by searching event name/display name keywords, and support quick filtering by event status.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47de3ea5d2dc47e492b7f65d969bc287~tplv-goo7wpa0wc-image.image) </span>

Support single or batch settings for **Start/Disable/Not Display** operations:


* Enable: Open the corresponding attribute for normal use.

* Disable: The corresponding attribute is not allowed to be used. Disabling a field will make downstream systems unavailable, so please proceed with caution.

* Not Display: The used attribute continues to function normally, but the corresponding attribute is not displayed in new scenarios.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71873f473e0a4ca5803eebeb24e2a444~tplv-goo7wpa0wc-image.image) </span>

<span id="dcb5c4ad"></span>
#### **4.2.1.2 Behavior Events Addition**

Click on "Add General Event" to support single creation (to individually create events, flexible modification of display names), batch creation (quickly upload multiple events, one\-click batch upload).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8493bdb2ce564c4cb4fffe1fccba40ad~tplv-goo7wpa0wc-image.image) </span>

Single Creation: Select the source table (a table registered in the data source), fill in the event name, display name, event description.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/035f706c114749a293d4fa24a8f21762~tplv-goo7wpa0wc-image.image) </span>

Batch Creation: Upload data according to the template specifications, including the source table, event name, display name, event description.


* Support file extensions: .xlsx .csv

* Only support uploading one file, with size ≤100M


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b788476237e470c84c562a748489743~tplv-goo7wpa0wc-image.image) </span>

<span id="59ec791b"></span>
### 4.2.2 Virtual Events

**Instructions:**  DataFinder product and third\-party behavioral data archives support creating virtual events.

Below is an example of customers who have purchased VeCDP and DataFinder simultaneously:

**Glossary:**  Virtual Events refer to breaking down and combining one or more original events through certain logical relationships to create virtual events, facilitating users to manage and view the combination of common complex events.

> Original event: An event generated by reporting via SDK or importing data.


**Statistical caliber of virtual events**:


* Between multiple original events, there is an "or" relationship. If one event is triggered, it indicates that the condition is met, and the virtual event is considered triggered. At the same time, filtering criteria can also be applied to each original event.

* A user triggers multiple combined original events in a virtual event, and when checking the number of unique users who triggered this virtual event. View the number of occurrences of this virtual event, without deduplication.


<span id="b6cec238"></span>
#### 4.2.2.1 **Create or edit virtual events**

Needs to operate in the DataFinder product.

<span id="3c067c7c"></span>
#### **4.2.2.2 View Virtual Events**

In the behavior profile configuration page, DataFinder virtual events & corresponding event categories are displayed by default, and cannot be edited/managed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c26225beb5142cd8fb7344e7a588039~tplv-goo7wpa0wc-image.image) </span>

<span id="0b848534"></span>
#### **4.2.2.3 Application scenarios for virtual events in VeCDP**

In tags, clusters, insights, and individual portraits, the selection or display of virtual events is supported, such as:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0cc20d47241e85117b264b2700911d9f.png) </span>

<span id="00772b29"></span>
### 4.2.3 General Attributes

**Application scenarios:**  The general attribute names in behavioral events are mostly in English. Through this function, you can configure the Chinese names and descriptions corresponding to event attributes, making it easier for business colleagues to understand when creating labels.

<span id="d6cf28df"></span>
#### 4.2.3.1 View the list of general attribute information


* Display event attribute information of behavioral data, including event attribute name, display name, event attribute description, etc.

* Support searching for corresponding event attribute information by searching for event name/display name keywords and quick filtering by event status.

* Support the use of multi\-value attributes.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb57c3c51508473eb18cce8d1fa2d773~tplv-goo7wpa0wc-image.image) </span>

Click the **configure** button to support linking to the dimension table for subsequent associated queries.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c54f3dc8d7664d4abe46c79e1933e337~tplv-goo7wpa0wc-image.image) </span>

<span id="900042af"></span>
#### 4.2.3.2 Upload Dimension Dictionary

Support uploading dimension dictionary files for translating attribute values and converting poorly readable numerical values into more readable text. Click **View** button, support **single or batch upload**.


* Support adding single configuration with an upper limit of 1000 rows.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d647bd68423c4915a9747ee38208acb0~tplv-goo7wpa0wc-image.image) </span>

Batch upload:


* Support extensions: .xlsx .csv

* Only support uploading one file, ≤10M

* Upload modes supported: overwrite (batch upload content will completely replace existing content), append (based on existing content, batch add configurations of enumeration values, if original values are duplicated, the newest configuration will be adopted)


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98c3551734d14345b3cf2412277002e5~tplv-goo7wpa0wc-image.image) </span>

<span id="a16f201f"></span>
#### 4.2.3.3 **Add General Event Properties**

Click "Add Event Attribute", support **single creation** (individually create events, flexibly modify display names), **batch creation** (quickly upload multiple events, one\-click batch upload).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/916a7d8ced92426ab8b24656bf5e7513~tplv-goo7wpa0wc-image.image) </span>

**Single creation:**  Select the source table (a table registered in the data source), fill in event attribute name, event attribute type, event attribute display, event description.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f285a68cb3a14c43839deafc2a6d8dde~tplv-goo7wpa0wc-image.image) </span>

**Batch Create:**  Upload data according to the template specifications, including property name, display name, attribute description, corresponding event, and data type.


* Support file extensions: .xlsx .csv

* Only support uploading one file, with ≤100M


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1145b39063934882809e9c21f544eae4~tplv-goo7wpa0wc-image.image) </span>

<span id="20e7ba35"></span>
### 4.2.4 Virtual Property

Virtual property is the secondary processing of general properties, which can be achieved through the four arithmetic operations of SQL expressions and some string manipulation functions.

<span id="b6f38c82"></span>
#### 4.2.4.1 **View the list of virtual property information**


* Display event attribute information, including event attribute name, display name, data type, etc.

* Support finding corresponding event attribute information by searching event name/display name keywords, and also support quick filtering by event status.

* Support the use of multi\-value attributes.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d2dcf21e1624d9e9734c586dd1cb1a7~tplv-goo7wpa0wc-image.image) </span>

<span id="e8f67053"></span>
#### 4.2.4.2 Upload Dimension Dictionary

Support uploading dimensional dictionary files to translate attribute values, turning poorly readable numbers into highly readable text. Click the  **"Settings"**  button to support **singular or batch uploads**.


* Single addition supports configuring up to 1000 lines.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cc7c9956bb0479da8ab3e02c323e049~tplv-goo7wpa0wc-image.image) </span>

Batch upload:


* Support file extensions: .xlsx .csv

* Only support uploading a single file, and ≤10M

* Upload mode supports: overwrite (batch uploaded content will completely replace the existing content), append (based on existing content, batch add configurations of enumeration values. If there are duplicates in the original values, the newest configuration will be used).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74e4d685390440f0af6159057afee214~tplv-goo7wpa0wc-image.image) </span>

<span id="7d1c2a05"></span>
#### 4.2.4.3 **Add virtual attributes**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aaa174174aaf47f1895bd71262968bcd~tplv-goo7wpa0wc-image.image) </span>

Basic Information:

Virtual property type: string, int, float, datetime, array

**SQL Expression:**  After writing the SQL expression, you can click on the bottom left to format or validate it.

**Associated with Events:**  You can choose "Any Association" or "All Associations." Any association links events that use any property in the SQL (with values) to virtual properties; All associations link events that use all properties in the SQL (with values) to virtual properties.

<span id="8e83631f"></span>
### 4.2.4 Event Classification

When VeCDP and DataFinder are deployed together, VeCDP synchronizes Finder event classifications by default and does not support editing or management.

\*Note: Only public categories are currently displayed, not private categories.

In event classification, users can customize event classifications.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4dce51dcf2bb499593b677fb3650b41f~tplv-goo7wpa0wc-image.image) </span>

Provide lineage view function to help users clearly understand the source and flow of data. Lineage information can be displayed in an intuitive graph or concise list format, and can be exported in Excel (xlsx) and CSV formats for further analysis and use.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cc07967ae99343a046745e9877314169.png) </span>

&nbsp;

<span id="065a5160"></span>
## 4.3 Business Detail Configuration

> Details of the subject's business data, including detailed or summarized data in certain scenarios, such as sales data.


Display attribute information in detailed data, including attribute name, display name, attribute description, source table, data type, data dictionary, status, etc., where display name and description can be modified. Support finding corresponding subject attribute information through search keywords and quickly filter by status.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3067f27ede1eaaa70e65acaa6554a324.png) </span>

Click the **configure** button to support associating with dimension tables for subsequent associated queries.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_59402cff6e0587e4bd75db1d64ddc8f7.png) </span>

Support batch uploading display names, enabling bulk modification of corresponding detailed data display names through uploading files, which can later be applied in tag/segmentation/individual portrait modules. For example, when creating segmentation circle selection rules, the modified display name will be shown when selecting detailed data from the drop\-down.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_450c7134c8d93894b015ed81ee5251de.png) </span>

Support **uploading data dictionaries.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2fbf1d29ccf463fafa9793cb6947451~tplv-goo7wpa0wc-image.image) </span>

On the upload page, users can upload files by dragging and dropping or by clicking.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Supported file extensions for upload: .xlsx .csv</div>


* <div data-tips="true" data-tips-type="warning">Only support uploading a single file, and ≤100M</div>


* <div data-tips="true" data-tips-type="warning">The header must be "Property Name", "Display Name", "Field Description", "Source Table"</div>


* <div data-tips="true" data-tips-type="warning">Upload field values starting from the second row by default</div>


* <div data-tips="true" data-tips-type="warning">Only read data from the first sheet</div>

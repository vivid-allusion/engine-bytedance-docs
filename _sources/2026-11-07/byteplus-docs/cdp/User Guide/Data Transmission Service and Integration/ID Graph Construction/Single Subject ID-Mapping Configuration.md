---
title: "Single Subject ID-Mapping Configuration"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Single_Subject_ID-Mapping_Configuration"
---

<span id="_1-功能概述"></span>
# 1. Overview of Features

Through the **VeCDP\-Data Management\-ID Graph Construction** feature, fragmented data related to the same user's multiple accounts can be integrated based on user IDs, phone numbers, device numbers, and other ID information. This function consolidates fragmented data from various sources within the enterprise, helping marketing or operational personnel identify the same user across different channels to achieve precise marketing and refined operations.

<span id="fafcd6ed"></span>
# 2. Usage Restrictions

Only the group administrator (i.e., the admin account) can configure the ID graph.

<span id="680b738b"></span>
# 3. Application Scenarios

In scenarios involving a single subject, most of the time revolves around the "**user**" for ID recognition and linking. Common scenarios include:


* **Cross\-platform User Identification**: Users may use the same service on different devices (e.g., PC, mobile, tablet). ID\-Mapping helps companies identify the same user behind these devices to provide a seamless cross\-device experience.

* **Marketing Activity Optimization**: Through ID\-Mapping, companies can more accurately understand user profiles and significant characteristics, combining attribute, order, and behavioral data to analyze user preferences comprehensively. This optimization refines marketing strategies, achieves precise ad placement, boosts conversion rates, and enhances user engagement.

* **Personalized Recommendations**: By leveraging user attributes, orders, and behavioral data insights to understand user profiles, companies can offer more personalized content recommendations, enhancing the user experience.


<span id="ed00de73"></span>
# 4. Noun Explanation


|Noun |Explanation |
|---|---|
|One ID |Also known as BaseID or reference ID, it is the unique identity ID of the subject. |
|Subject |Also known as entity/object, often refers to individuals/vehicles/locations that can be operated for growth or insight analysis. |
|ID |Represents a sequence of numbers for a subject, such as a phone number. |
|ID Type |Definition of the data information that defines the subject's identity, often referring to specific identifiers that follow the subject, such as user ID, device ID, etc., can be understood as identity ID. |
|ID Identify Code |Unique identifier of the ID, can be defined using English + underscores. |
|ID Data Type |Base data type, default can be selected as string type. |
|Channel Identification |Official types used to mark downstream identifiable channels, such as Phone/IDFA for mobile phone. |
|Data Set |In the ID graph construction module, specifically refers to the dataset of offline full ID, currently only supports Hive type dataset. |
|Full update |Read the latest partition data update data every day P_date (date partition) = the latest day. |
|Incremental update |Read all historical partition data update data every day P_date (date partition) <= the latest day. |
|Multiple subject conversion relationships |By configuring the relationship data and transformation strategy between multiple subjects, build conversion relationships, commonly used in recommendation, matchmaking, and data interchange scenarios, such as finding potential customer information corresponding to a car through its tag data. |


<span id="14b5b8ae"></span>
# 5. Operation Guide

**ID\-Mapping data preparation and configuration process is as follows:** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e434ed79c3cb4e719f14dd8f9da1f81d~tplv-goo7wpa0wc-image.image" width="1134px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>When preparing the data, please note:</strong></div>



1. <div data-tips="true" data-tips-type="tip">All data needs to be stored logically according to the full table, meaning each partition contains all IDs.</div>


2. <div data-tips="true" data-tips-type="tip">The full dataset output by visual modeling needs to be stored in Hive and a specific date field selected as the primary partition.</div>



After completing the data preparation in the first three steps, the following introduces the OneID configuration operation (Step 4):

<span id="181c17f5"></span>
## 5.1 **Step 1: Configure the Subject**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Instructions</div>


<div data-tips="true" data-tips-type="tip">Purpose: Define a new main object, also known as an entity/object, often referring to individuals/vehicles/locations that can be used for operational growth or insight analysis.</div>


<div data-tips="true" data-tips-type="tip">Outcome: A set of OneID data content will be generated around each main subject. OneID (also known as BaseID) is the unique identity ID of the subject.</div>


The operation steps are as follows:


1. Click on **Data Management\-ID Graph Construction.** 

2. Choose **Create New Subject** button and fill in the corresponding subject information, including:

* Subject Type: Used to distinguish the classification identifiers of the subject, such as person, vehicle, shop, product, etc.

* Subject Avatar: A default avatar will be displayed based on the selected subject type, and this avatar will serve as an identification displayed on the homepage and individual portraits.

* Subject Name: The name by which the subject, such as a person/vehicle, can be understood and recognized.

* Subject Description: A detailed description of the subject, such as users who use xx to represent people.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e264157ae504ac9adbf21ded3fc0abf~tplv-goo7wpa0wc-image.image" width="1902px" /></div>


<span id="8eb65ba5"></span>
## **5.2 Step Two: Configure OneID**

<span id="36e8b972"></span>
### **Step 1: Configure ID Types**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Description</div>


<div data-tips="true" data-tips-type="tip">Purpose: Used to define the unique identity identifier of the main subject, including metadata for identification and all identification data.</div>


<div data-tips="true" data-tips-type="tip">Definition: ID, also known as user identification, is user\-marked data reported on different channels, such as device IDs, Email IDs.</div>


<div data-tips="true" data-tips-type="tip">Outcome: The most basic data source for OneID generation, theoretically requiring each ID to configure data containing all users' information (full ID data).</div>


The operational steps are as follows:


1. **Configuration ID Type**. On this page, click the  **“+”**  button to create a new ID type.

   There are two ways to create IDs, namely template batch creation and custom creation. The operational steps for these two methods will be introduced separately.



|**Creation Method** |**Operating Instructions** |**Product Screenshot** |
|---|---|---|
|When selecting the **Template Batch Creation** method. |The system will provide an ID creation template, which can be referenced to bulk create ID types that need to participate in ID Mapping. Users can modify the names and English identifiers of ID types based on actual needs in the template. After completion, click **Confirm** to proceed. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53d3784d434840f5907c391382bb9d05~tplv-goo7wpa0wc-image.image) </span> |
|When selecting custom creation mode \*\*\*\* |Custom ID types can be created as needed. Supports the creation of custom single IDs or combination IDs, such as phoneid for single ID, appid+openid (WeChat Mini Program) for combination ID.<br><br>**Step 1: Fill in basic ID type information.** <br><br><br>* When configuring **Single ID**, fill in the corresponding information on the ID configuration page:<br><br>   * ID Name: Used to represent the ID's name;<br><br>   * ID Type Description: Used to distinguish and understand the ID's descriptive information;<br><br>   * ID English Identifier: The unique identifier of the ID, which is also the parameter field for open interface interaction, can be defined using English + underscore;<br><br>   * ID Data Type: Used to create the type definition for storing IDs, it is recommended to keep consistent with the data warehouse type, you can choose character type, numeric type. If unsure, default to String.<br><br>   * Channel Identification Tag: used to mark the official type that downstream can identify, is an important label that downstream systems can recognize, for example, choosing Phone means downstream tasks can send messages, please choose carefully. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/720fd8d00f2141ca9260d4595aa47596~tplv-goo7wpa0wc-image.image) </span> |
||* When configuring **combination ID**, fill in the corresponding information on the ID configuration page:<br><br>   * Fill in the names, descriptions, English labels, and data types of ID1 and ID2 respectively;<br><br>   * Advanced configuration of combination ID: Define the optional dimension names of ID1 through the dimension table, used for classification selection when circling, will not participate in the generation of OneID. For example, constructing a combination ID with App_ID + Open_ID, at this time the App_name can be obtained through the dimension table mapping. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93fb20d0c8104b66a9017d106d685440~tplv-goo7wpa0wc-image.image) </span> |
||**Step 2: Configure full ID data:** <br><br><br>* Is data configured: If enabled, the full data source of the ID can be configured, and after configuration, the ID can be used in the next step "OneID Configuration."<br><br>* Data Source:<br><br>   * Offline + Real\-time Data: Can simultaneously configure offline full data and real\-time data, mutually correcting.<br><br>   * Only real\-time data: No need to configure offline data, real\-time data can be generated in real time through the "Visual Modeling" real\-time ID Mapping operator.<br><br>* When selecting "Offline + Real\-time Data" as the data source, further selection of the data set needed for configuration is required. Note: Only Hive data sets updated daily can be selected here, otherwise the dropdown list may not find it.<br><br>* Update Method: Supports two methods: full and incremental updates.<br><br>* ID Type Corresponding Fields: Simply select the field corresponding to the ID in the dataset. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b232bcb60e37411085b0ab46df34ef71~tplv-goo7wpa0wc-image.image) </span> |


\***Notice:** 


* The English identifier corresponding to the ID is unique to the entire group, and can be modified as needed in case of duplication.

* The creation of ID types is still in the preparatory stage for OneID, and the ID will not yet be directly involved in OneID generation.

* IDs created through templates default to real\-time data input, which means data is input into this ID through real\-time visual modeling. For offline IDM modeling, editing and configuring offline datasets are required.


<span id="96daab79"></span>
### **Step 2: Create ID Reference Relationship**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Reference Relationship</strong>: The key to ID fusion connectivity lies in establishing a link\*\*++ between IDs++\*\*. IDs connected can be defined as a OneID. At this point, this connection is the reference relationship. Typically, reference relationships are combined with priority to define the generation order and fusion rules of OneID.</div>


Operation steps are as follows:


1. Click the  **"+"**  button to the right of the reference relationship to create a new reference relationship.

2. Configure reference relationship information:

* Select the relationship dataset: Only support Hive datasets updated on a daily basis; otherwise, the dropdown list may not find it.

* Select the IDs needed to establish relationships: Based on the dataset to establish reference relationships between IDs, first select the ID and then select the field corresponding to the ID dataset.

* Select the ID mapping logic: Support one\-to\-one relationship, one\-to\-many relationship (e.g., one device DeviceID associated with multiple phone numbers), many\-to\-one relationship, many\-to\-many relationship.

* Reference strategy: When IDs refer to each other, if there is a one\-to\-many relationship, to refer to the most reasonable ID corresponding to OneID, you need to specify the strategy field and strategy logic. If not configured, the system default strategy will be used. For example, when referencing "Device ID" as in "Phone ID," there is a situation where one Device ID corresponds to multiple Phone IDs in the data. In this case, the Phone ID with the **latest usage time** can be set as the reference Phone ID. The **time** used here is the strategy field, with **latest** being the strategic logic;

* Unbind: The OneID generation sequence will first refer to the already generated OneID, followed by the latest reference relationship. After activating the unbind button, the OneID generation process will prioritize the reference relationship of the latest day, followed by considering the reuse of the already generated OneID, thereby ensuring that the OneID is under the latest binding relationship.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb8431a6dac44ef28a0211c024acc21a~tplv-goo7wpa0wc-image.image" width="1902px" /></div>


\***Attention:** 


* The ID type selected in this step must have been prepared in the previous step and have full data configuration enabled.

* This configuration is still part of the preparation for OneID setup. The OneID will not be generated at this stage.

* Any changes made to the above configurations that are not involved in OneID will not have any impact on OneID.


<span id="559ffb4a"></span>
### **Step3：Configure ID Generation Graph**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Explanation</div>


<div data-tips="true" data-tips-type="tip">Purpose: Define the generation logic of OneID through ID priority and the reference relationship between IDs. This is the core configuration of OneID.</div>


<div data-tips="true" data-tips-type="tip">Result: This stage determines how OneID is generated, ultimately producing standardized OneID data.</div>


**Important reminder:** 

Currently, the OneID generation strategy & reference strategy support configuration. OneID enforces one\-to\-one, whether OneID is variable, offline reference real\-time, reference relationships. For explanations and scenario suggestions of various generation strategies and reference strategies, please refer to the document "[OneID Generation Strategy & Reference Strategy](https://www.volcengine.com/docs/7139/1282860)".

**The operation steps are as follows:** 

Add ID to the OneID generation graph.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e4d619fedf14695a4bed174b2b0814b~tplv-goo7wpa0wc-image.image" width="1558px" /></div>


Adjust the priority order of the ID by dragging it.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68a9ac171d8247ba82a5ff82f9ef755c~tplv-goo7wpa0wc-image.image" width="1303px" /></div>


Add reference relationships for the ID.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50bb454d4e79462aa481c8150090000a~tplv-goo7wpa0wc-image.image" width="1318px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Points to Note:</strong></div>



* <div data-tips="true" data-tips-type="tip">IDs with the highest priority are not recommended to configure reference relationships.</div>


* <div data-tips="true" data-tips-type="tip">It is recommended to configure reference relationships for IDs with non\-highest priority.</div>


* <div data-tips="true" data-tips-type="tip">IDs with low priority should reference IDs and are not recommended for reverse referencing.</div>


* <div data-tips="true" data-tips-type="tip">When adding each ID reference relationship, only reference relationships containing that ID can be selected, meaning that reference relationships like mobile number = device number can only be added to the mobile number or device number.</div>

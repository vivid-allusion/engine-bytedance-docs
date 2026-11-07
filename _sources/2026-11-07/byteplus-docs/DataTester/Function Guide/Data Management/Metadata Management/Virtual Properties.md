---
title: "Virtual Properties"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Virtual-Properties"
---

Virtual properties can meet the needs of secondary processing of property values. You can create a virtual property by writing four operations and partial string operation functions in SQL expressions, which are later used for user properties, some or all event properties. This article introduces you to the considerations and usage guidelines for virtual properties.

<span id="07cc00be"></span>
# Usage restrictions

An application can create a limited number of virtual properties. When the maximum number of virtual properties created reaches the limit, the "Create Virtual Property" button will not be clickable.


* SaaS\-cloud\-native, SaaS\-non\-cloud\-native: An application can create up to 200 virtual properties.

* Privatization: An application can create up to 5000 virtual properties.


<span id="9c08978f"></span>
# Create virtual properties


1. After logging in to the DataTester console, click on the left navigation bar **Data Management** \> **metadata Management** \> **Virtual Properties** to enter the Virtual Properties page.

2. Click the **Create Virtual Property** button in the upper right corner of the page, create a new virtual property, and configure the virtual property parameters in the pop\-up side border.

3. Configure virtual property parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4bc96ec0985147f190e4ae47ca109ee5~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Configuration instructions** |
   |---|---|
   |Attribute type |* Event virtual properties: New event properties computed from existing properties. Original attributes can come from event attributes or user attributes.<br><br>* User virtual properties: New user properties calculated based on the properties of the user table. |
   |Attribute name |Required, can only be named in English and characters. The rule is [a\-zA\- Z_] [0\-9a\-zA\- Z_] \*, within 100 characters in length. Case\-sensitive (consistent with the status quo). We will increase the default prefix to $ *vp* |
   |Data type |Configure the value data type of virtual properties: string, int, float, datetime, list |
   |SQL expression |Fill in the SQL expression fragment for the processing of the property. You can manually fill in SQL expressions. Currently, properties starting with special characters such as numbers and Chinese are supported by using backquotes, such as **event_params. '123'**  , **user_profiles. '123'**  .<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">There is currently no limit to the number of properties involved in an expression, and only the first section of SQL will be executed.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The general configuration capabilities of SQL expressions are as follows. For more scenario\-based example demos, please refer to the <strong>++SQL Expressions Demo ++</strong>section below.</div><br> |
   |Association<br><br>(Only event properties need to be configured) |Configure how virtual properties are associated:<br><br><br>* Associate as long as one of them has a value (either): Events associated with any of the properties used in SQL are associated with virtual properties<br><br>* All are associated with values (all): Events that are associated with all properties in SQL are associated with virtual properties<br><br><br>The similarities and differences between related events are described as follows:<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cff80fbe3c77476f9df934bc639aaf45~tplv-goo7wpa0wc-image.image) </span> |
   

4. Complete the above operations and click **OK** to create a virtual property.


<span id="4568fa7f"></span>
# SQL Expression Demo

<span id="640ee976"></span>
## Demo1: Perform four operations on property values

 **[Example 1]** 


* Example scenario:

   Suppose event tracking has two attributes buried: event attribute (float type attribute) "cost price cost_price" and "sales price sale_price", when we want to calculate profit, we can directly create a new virtual event attribute "profit $vp_profit". At this point, we can use "addition, subtraction, multiplication and division"

* SQL expression:

   ```SQL
   event_params.sale_price - event_params.cost_price
   ```
   


 **[Example 2]** 


* Example scenario:

   Assuming that the event tracking has buried attributes: event attributes "principal", "interest rate (month) interest_rate" and "month duration", it is necessary to calculate the "sum of principal and interest of wealth management products".

* SQL expression:

   ```SQL
   event_params.principal + event_params. principal * pow(event_params.interest_rate, event_params.duration)
   ```
   


<span id="1de8b89c"></span>
## Demo2: Extracting some fields from property values

 **[Example 1]** 


* Example scenario: Suppose there is an attribute when event tracking: the event attribute "URL full_url", hoping to extract the domain name information. For example, `https://console.volcengine.com/DataTester/app/178497/dashboard/6807670720953319944`want to extract `console.volcengine.com`

* SQL expression:

   ```SQL
   domain(event_params.full_url)
   ```
   

   Specific URL related functions, specific URL related functions, please refer to [SQL Custom Query](https://docs.byteplus.com/docs/DataTester/SQL-Custom-Query)the list of functions.


 **[Example 2]** 


* Example scenario: Suppose there is an attribute when event tracking: the event attribute "content details body_json", the attribute content is a string in json format, such as:

   ```json
   {"product": "DataTester", "user_name": "管理员"} //Administrator
   ```
   

   Want to extract product information: DataTester

* SQL expression:

   ```SQL
   JSONExtractString(event_params.body_json,'product')
   ```
   

   For specific JSON related functions, please refer to [SQL Custom Query](https://docs.byteplus.com/docs/DataTester/SQL-Custom-Query)the list of functions in.


<span id="89817ea7"></span>
## Demo3: Merging multiple attribute values

 **[Example 1]** 


* Example scenario:

   Suppose event tracking reports the wrong attribute name, for example, first reports the event attribute "product name produc_name", after running for a month, finds that the name is misspelled, and then reports a new event attribute "product name product_name". Then when analyzing, you want to be able to analyze all the data simultaneously.

* SQL expression:

   ```SQL
   if(event_params.product_name IS NOT NULL, event_params.product_name, event_params.produc_name)
   ```
   


 **[Example 2]** 


* Example scenario: Suppose there is an attribute when event tracking: the event attribute "price", which is a float type, has values of 10.56, 200.345

   If you want to increase the display to 10.56 yuan and 200.345 yuan, you can create virtual properties using the following rules:

* SQL expression:

   ```SQL
   concat('￥',toString(event_params.price))
   ```
   


<span id="a4f47bd0"></span>
## Demo4: Calculation accuracy of uniform attribute values


* Example scenario:

   Suppose there is an attribute when event tracking: the event attribute "price", which is a float type, has values of 10.56, 200.345

   If you want to round only integer parts, such as 11 or 200, you can create virtual properties using the following rules:

* SQL expression:

   ```SQL
   round(event_params.price,0)
   ```
   


<span id="2ced8507"></span>
## Demo5: Labeling customers


* Example scenario:

   Suppose there is an attribute when event tracking: the user attribute "accumulated consumption amount total_cost" is a float type

   We hope to distinguish the membership level of users according to the consumption amount, such as:

   
   |**Cumulative consumption amount** |**VIP level** |
   |---|---|
   |＞=1000 |black gold |
   |[500,1000) |diamond |
   |[200,500) |platinum |
   |[100,200) |gold |
   |<100 |bronze |
   

* SQL expression:

   ```SQL
   multiIf(
   user_profiles.total_cost<100,'bronze',
   user_profiles.total_cost>=100 and user_profiles.total_cost<200 ,'diamond',
   user_profiles.total_cost>=200 and user_profiles.total_cost<500,'platinum',
   user_profiles.total_cost>=500 and user_profiles.total_cost<1000,'gold',
   'black gold'
   )
   ```
   


<span id="fb608adc"></span>
## Demo6: Type Conversion


* Example scenario:

   Assume that there are attributes when event tracking: the event attribute "video time media_duration_info" is a float type, representing milliseconds. I hope to convert it to an int type and convert it to minutes for easy calculation.

* SQL expression:

   ```SQL
   cast(event_params.media_duration_info/1000/60 as Nullable(int))
   ```
   

   Note: After slotting, all event attributes in the Map column are of type nullable, so when converting the attribute type by cast, no matter what type it is converted to (int, float, etc.), you need to use the function assumeNotNull to wrap the attribute to ensure that the converted attribute type is nullable, otherwise it will cause problems with type conversion. Use methods: Nullable (int), Nullable (float), etc.


<span id="9426960a"></span>
# Edit/Delete Virtual Properties

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7191494e834b43868179cb0e097bece0~tplv-goo7wpa0wc-image.image) </span>


* Edit virtual properties

   After entering the "Virtual Properties" interface, you can see all the virtual properties that have been created. Select the virtual properties you want to edit and click "Edit" at the bottom of the operation column to edit.

* Delete virtual property

   If you need to delete a virtual property, select the virtual property you want to edit and click "Delete" at the bottom of the action column to delete the virtual property.


<span id="cf5b5d91"></span>
### Instructions for writing and modifying "display name, attribute description, dictionary, data type"

Virtual properties provide the writing and modification of "display name, property description, dictionary, data type", as follows:


* Modifying any field will restart the validation SQL.

* The existing dictionary will be deleted after the SQL expression is changed.

* If the following prompt appears next to the virtual property, it means that the virtual property has expired. The failure situation is as follows:


The user or event public attributes used are disabled.

2) The type of attribute used has been modified.

3) is deleted.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d1c5a4f527e41748f7e4366d31a9137~tplv-goo7wpa0wc-image.image) </span>


* Invalid virtual properties will not support editing of any fields.

* If a prompt appears when displaying the name during editing (as shown in the figure below), please enter the editing page to check or see if you have this permission;


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54bed10e395a449bbb634c7b639f9181~tplv-goo7wpa0wc-image.image) </span>

<span id="e688e2c8"></span>
# Reference: Scope of application of virtual properties


|**Function** |**Description** |
|---|---|
|Custom query |Not applicable. |
|Virtual event |Apply. When used in a query, any virtual event attribute contained in an event can be selected. |
|Circle event |Event virtual properties do not apply, user virtual properties do. |
|Arbitrary event |Not applicable, including: any_event and any_active_event. |
|Analysis subject |Apply, create, and use as normal properties. |
|Attribute association |Apply. |
|User path |Apply. |
|Virtual property |Not applicable. Virtual properties are not allowed to be created based on virtual properties, and expressions for virtual properties of user types are not allowed to contain event properties. |

---
title: "Virtual Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Virtual_Properties"
---

Virtual properties can meet the needs of secondary processing of property values. You can create a virtual property by writing four operations and partial string operation functions in SQL expressions, which are later used for user properties, some or all event properties. This article introduces you to the considerations and usage guidelines for virtual properties.

<span id="db94e086"></span>
# Usage restrictions

An application can create a limited number of virtual properties. When the maximum number of virtual properties created reaches the limit, the "Create Virtual Property" button will not be clickable.


* SaaS\-cloud\-native: An application can create up to 200 virtual properties.

* Privatization: An application can create up to 5000 virtual properties.


<span id="_2-创建-编辑虚拟属性"></span>
# Create virtual properties


1. After logging into the DataFinder console, click **Data Management** \> **Metadata Management** \> **Virtual Properties** in the top navigation bar to enter the Virtual Properties page.

2. Click the **Create Virtual Property** button in the upper right corner of the page, create a new virtual property, and configure the virtual property parameters in the pop\-up side border.

3. Configuration basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c370e01d855c4e8e813eea497b573bf6~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Configuration instructions** |
   |---|---|
   |Property name |Required, can only be named in English and characters. The rule is [a\-zA\- Z_] [0\-9a\-zA\- Z_] \*, within 100 characters in length. Case\-sensitive (consistent with the status quo). We will increase the default prefix to $ *vp* |
   |Property type |* Event virtual properties: New event properties computed from existing properties. Original properties can come from event properties or user properties.<br><br>* User virtual properties: New user properties calculated based on the properties of the user table. |
   |Presentation name & property description |Customize the property name and description information of the virtual property. |
   |Available range |Configure the visibility of the virtual narrative.<br><br><br>* Only available to yourself: Only visible to yourself, no one else can see or use the created virtual property.<br><br>* Public use: Everyone can see and use the created virtual properties. |
   |Data type |Configure the value data type of virtual properties: string, int, float, datetime, list |
   |Association |Configure how virtual properties are associated:<br><br><br>* Any association: Events associated with any property used in SQL are associated with virtual properties<br><br>* All Associations: Events that are associated with all properties in SQL are associated with virtual properties<br><br><br>The similarities and differences between related events are described as follows:<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a62bf3140dc4902812cf2d5a5f58acf~tplv-goo7wpa0wc-image.image) </span> |
   

4. Configuration expression. Fill in the SQL expression fragment for the processing of the property.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">There is currently no limit to the number of properties involved in an expression, and only the first section of SQL will be executed.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The general configuration capabilities of SQL expressions are as follows. For more scenario\-based example demos, see the <strong>++SQL Expressions Demo ++</strong>section below.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26893cea938f4aa3b6f4a5291f3f39e3~tplv-goo7wpa0wc-image.image) </span>

   * You can search and select related properties or functions in the property selection box and function selection box below, and double\-click to refer the corresponding properties and functions to the text box of the SQL expression with one click.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you have both DataFinder and CDP enabled, in a SaaS\-cloud native environment, when creating virtual properties, the expression of virtual properties supports referencing cdp tags to create virtual event properties and virtual user properties, and the syntax is <strong>tags. 'xxx'</strong> .      </div>
      

   * You can also manually fill in SQL expressions. Currently, properties starting with special characters such as numbers and Chinese are supported by using backquotes, such as **event_params. '123'**  , **user_profiles. '123'**  .

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">In a SaaS\-cloud native environment, creating virtual event properties allows you to directly reference the business dimension (item table) data by manually filling in SQL expressions, for example, <code>concat (item_profiles.fund.name, event_params price)</code>.      </div>
      

5. Click **Online Results Test** in the lower right corner of the page to test expression configuration results. After the configuration expression is fully entered, you can instantly view the processed property value by customizing the original value.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4937b09adcbd49979f20c71af8f91f8c~tplv-goo7wpa0wc-image.image) </span>

6. Complete the above operations and click **OK** to create a virtual property.


<span id="110c358d"></span>
# SQL Expression Demo

<span id="c873b368"></span>
## Demo1: Perform four operations on property values

 **[Example 1]** 


* Example scenario:

   Suppose event tracking has two properties buried: event property (float type property) "cost price cost_price" and "sales price sale_price", when we want to calculate profit, we can directly create a new virtual event property "profit $vp_profit". At this point, we can use "addition, subtraction, multiplication and division".

* SQL expression:

   ```SQL
   event_params.sale_price - event_params.cost_price
   ```
   


 **[Example 2]** 


* Example scenario:

   Assuming that the event tracking has buried properties: event properties "principal", "interest rate (month) interest_rate" and "month duration", it is necessary to calculate the "sum of principal and interest of wealth management products".

* SQL expression:

   ```SQL
   event_params.principal + event_params. principal * pow(event_params.interest_rate, event_params.duration)
   ```
   


<span id="b5ba5b28"></span>
## Demo: Extracting some fields in a property value

 **[Example 1]** 


* Example scenario: Suppose there is an property when event tracking: the event property "URL full_url", hoping to extract the domain name information. For example, `https://console.volcengine.com/datafinder/app/178497/dashboard/6807670720953319944`want to extract `console.volcengine.com`

* SQL expression:

   ```SQL
   domain(event_params.full_url)
   ```
   

   Specific URL related functions, specific URL related functions, please refer to [Custom SQL Query](https://docs.byteplus.com/docs/DataFinder/Custom_SQL_Query)the list of functions.


 **[Example 2]** 


* Example scenario: Suppose there is an property when event tracking: the event property "content details body_json", the property content is a string in json format, such as:

   ```json
   {"product": "datafinder", "user_name": "管理员"} //manager
   ```
   

   Want to extract product information: datafinder

* SQL expression:

   ```SQL
   JSONExtractString(event_params.body_json,'product')
   ```
   

   For specific JSON related functions, please refer to [Custom SQL Query](https://docs.byteplus.com/docs/DataFinder/Custom_SQL_Query)the list of functions in.


<span id="a9c794b5"></span>
## Demo3: Merging multiple property values

 **[Example 1]** 


* Example scenario:

   Suppose event tracking reports the wrong property name, for example, first reports the event property "product name produc_name", after running for a month, finds that the name is misspelled, and then reports a new event property "product name product_name". Then when analyzing, you want to be able to analyze all the data simultaneously.

* SQL expression:

   ```SQL
   if(event_params.product_name IS NOT NULL, event_params.product_name, event_params.produc_name)
   ```
   


 **[Example 2]** 


* Example scenario: Suppose there is an property when event tracking: the event property "price", which is a float type, has values of 10.56, 200.345

   If you want to increase the display to 10.56 yuan and 200.345 yuan, you can create virtual properties using the following rules:

* SQL expression:

   ```SQL
   concat('￥',toString(event_params.price))
   ```
   


<span id="56ea733b"></span>
## Demo4: Calculation accuracy of uniform property values


* Example scenario:

   Suppose there is an property when event tracking: the event property "price", which is a float type, has values of 10.56, 200.345

   If you want to round only integer parts, such as 11 or 200, you can create virtual properties using the following rules:

* SQL expression:

   ```SQL
   round(event_params.price,0)
   ```
   


<span id="97f16f35"></span>
## Demo5: Labeling customers


* Example scenario:

   Suppose there is an property when event tracking: the user property "accumulated consumption amount total_cost" is a float type

   We hope to distinguish the membership level of users according to the consumption amount, such as:

   
   |**cumulative consumption amount** |**VIP level** |
   |---|---|
   |＞=1000 |black gold |
   |[500,1000) |diamond |
   |[200,500) |Platinum |
   |[100,200) |gold |
   |<100 |bronze |
   

* SQL expression:

   ```SQL
   multiIf(
   user_profiles.total_cost<100,'青铜', //bronze
   user_profiles.total_cost>=100 and user_profiles.total_cost<200 ,'钻石', //diamond
   user_profiles.total_cost>=200 and user_profiles.total_cost<500,'白金', //platinum
   user_profiles.total_cost>=500 and user_profiles.total_cost<1000,'黄金', //gold
   '黑金' //black gold
   )
   ```
   


<span id="b02b061a"></span>
## Demo6: Type Conversion


* Example scenario:

   Assuming that there are properties when event tracking: the event property "video time media_duration_info" is a float type, representing milliseconds. I hope to convert it to an int type and convert it to minutes at the same time, which is convenient for calculation.

* SQL expression:

   ```SQL
   cast(event_params.media_duration_info/1000/60 as Nullable(int))
   ```
   

   Note: After slotting, all event properties in the Map column are of type nullable, so when converting the property type through cast, no matter what type it is converted to (int, float, etc.), you need to use the function assumeNotNull to wrap the property to ensure that the converted property type is nullable, otherwise it will cause problems with type conversion. Use methods: Nullable (int), Nullable (float), etc.


<span id="67c2eb8c"></span>
# Edit/Delete Virtual Properties

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf274588068b4165bdfb4e3a9c888122~tplv-goo7wpa0wc-image.image) </span>


* Edit virtual properties

   After entering the "Virtual Properties" interface, you can see all the virtual properties that have been created. Select the virtual properties you want to edit and click "Edit" at the bottom of the operation column to edit.

* Delete virtual property

   If you need to delete a virtual property, select the virtual property you want to edit and click "Delete" at the bottom of the action column to delete the virtual property.


<span id="“展示名、属性描述、字典、数据类型”的编写和修改说明"></span>
### Instructions for writing and modifying "display name, property description, dictionary, data type"

Virtual properties provide the writing and modification of "display name, property description, dictionary, data type", as follows:


* Modifying any field will restart the validation SQL.

* The existing dictionary will be deleted after the SQL expression is changed.

* If the following prompt appears next to the virtual property, it means that the virtual property has expired. The failure situation is as follows:

   1）The user or event public properties used are disabled.

   2) The type of property used has been modified.

   3) is deleted.


<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/f118943127cb4393bf85301b346ab68d) </span>


* Invalid virtual properties will not support editing of any fields.

* If a prompt appears when displaying the name during editing (as shown in the figure below), please enter the editing page to check or see if you have this permission;


<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/16d334ce14764f04b603ba12c9d81819) </span>

<span id="a5ece633"></span>
# Reference: Scope of application of virtual properties


|**Function** |**Describe** |
|---|---|
|Custom query |Not applicable. |
|Virtual event |Apply. When used in a query, any virtual event property contained in an event can be selected. |
|Circle event |Event virtual properties do not apply, user virtual properties do. |
|Arbitrary event |Not applicable, including: any_event and any_active_event. |
|Analysis subject |Apply, create, and use as normal properties. |
|Property association |Apply. |
|User path |Apply. |
|Virtual property |Not applicable. Virtual properties are not allowed to be created based on virtual properties, and expressions for virtual properties of user types are not allowed to contain event properties. |

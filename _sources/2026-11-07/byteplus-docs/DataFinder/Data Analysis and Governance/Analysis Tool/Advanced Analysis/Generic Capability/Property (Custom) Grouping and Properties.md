---
title: "Property (Custom) Grouping and Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Property_Custom_Grouping_and_Properties"
---

DataFinder supports filtering user data or grouping query results based on properties (for example, filtering or grouping user purchase behavior data by "gender"). At the same time, DataFinder provides you with the ability to customize the grouping of properties (for example, divide the "city" property into "first\-tier", "new first\-tier", etc.), which is convenient for flexible use of the properties after custom grouping for data filtering or grouping display. This article introduces you to the functional logic and usage guidance for property creation custom grouping rules and property grouping presentation.

<span id="一、概念介绍"></span>
# Application scenario


|Comparison term |Property custom grouping rules |Query results are grouped in property dimensions |
|---|---|---|
|Application scenario |Custom property grouping provides the ability to rework property values for more flexible analysis needs.<br><br>For example, the property [City] can be custom grouped, and the grouping is named as the city level:<br><br><br>* Group value 1 [first\-tier cities], the rule is cities = Beijing, Shanghai, Shenzhen, Guangzhou;<br><br>* Group value 2 [New first\-tier cities], the rule is cities = Hangzhou, Chengdu, Chongqing;<br><br>* Group value 3 [non\-first\-tier cities], other cities are classified as non\-first\-tier cities<br><br><br>In the future, when you need to use the property [City] for property filtering or grouping display, you can select the property [City], or you can directly select the created first\-tier cities, new first\-tier cities and other groupings. |For example, when you are querying and analyzing the sales of a certain product, you want to see the characteristics of male and female users' consumption behavior separately. At this time, you can group the consumption behavior indicators on the [gender] property. |
|Operation entrance |Usually when selecting a property, when the mouse hovers to the property name and then calls up the property details card, a grouping rule can be added to the corresponding property under the card.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b49fe3972c714c23841973837add1e6f~tplv-goo7wpa0wc-image.image) </span> |When using the analysis tool, you can set the property grouping display of query results in the top query configuration area.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/561ebf52b9c74d0089281dc36ddbb2ab~tplv-goo7wpa0wc-image.image) </span> |


<span id="二、功能描述"></span>
# Property **custom grouping rules**

<span id="1e62ebb7"></span>
## Function Description

After collecting and reporting the property data, you can further classify and group the property data, so that you can flexibly choose to use the entire property data or choose one of the grouped data when using the property data later. The following describes the support and grouping logic of the custom grouping function from the two dimensions of property type and property data format.

<span id="a8491e57"></span>
### Property type


|Property type |Whether to support custom grouping rules |
|---|---|
|Event/user properties |Support.<br><br><br>* Contains virtual event/user properties.<br><br>* Contains preset event/user properties and custom event/user properties.<br><br>* Contains event public properties and event properties. |
|User grouping |Not supported. |
|User tag |Not supported. |


<span id="e025078c"></span>
### Property data format: string/version


|Property data type |Whether to support |Custom grouping logic |
|---|---|---|
|string/version |Support |* Grouping rules: Support for character type (string), time type (datetime) properties to perform a variety of operator calculations (equal to not equal to, including not including, regular matching does not match, etc.) to generate grouping values.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f407af1c1624bd5b01c38503b4a3522~tplv-goo7wpa0wc-image.image) </span><br><br>* After grouping data format and supported operators: character type (string), time type (datetime) property After creating a custom grouping, the property type of the custom grouping is unified as character type (string), and the operators supported for subsequent use of custom grouping are "=", "≠". |


<span id="961855ac"></span>
### Property data formats: int, float


|Property data type |Whether to support |Custom grouping logic |
|---|---|---|
|int/float |support |* Grouping rules:<br><br>   * It supports grouping numeric (int, float) properties with numerical group spacing, and supports fixed or customized group spacing for numerical grouping.<br><br>   * It supports the creation of up to 100 custom groups.<br><br>      For example, divide the values into 4 groups with spacing: [1, 5], (5, 10], (10, 50], and others.<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ac1e42d66f24e0fb15fce9f27eded1b~tplv-goo7wpa0wc-image.image) </span><br><br>* Data formats and supported operators after grouping: Numeric (int, float) properties After creating a custom grouping, the property types of the custom grouping are unified as character types (string), and the operators supported for subsequent use of custom grouping are "=", "≠".<br><br>   The following is an example of int:<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c15162064c9540d4bc50b5f967ac81fa~tplv-goo7wpa0wc-image.image) </span> |


<span id="1e551550"></span>
### Property data format: datetime


|Property data type |Whether to support |Custom grouping logic |
|---|---|---|
|datetime |support |* Grouping rules: Support custom grouping of time type (datetime type) properties "by month", "by minute" and other time intervals.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a3ba7f9173604dd1931287e2cde96c6e~tplv-goo7wpa0wc-image.image) </span><br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Monthly: Grouping datetime properties by month, properties will be divided into 12 groups: 1, 2, 3,..., 12, representing January to December respectively.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By minute: Grouping datetime properties by minute granularity, the properties will be grouped into 60 groups: 0, 1, 2,..., 59, representing [0, 1) minutes, [1, 2) minutes, [2, 3) minutes, ..., [59, 60) minutes.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By hour: Grouping datetime properties by hour granularity, the properties will be grouped into 24 groups: 0, 1, 2,..., 23, representing [0, 1) hours, [1, 2) hours, [2, 3) hours,..., [23, 24) hours, respectively.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By day of the week: Grouping the datetime property by day of the week granularity, the properties will be divided into 7 groups: 1, 2,....., 7 , representing Monday, Tuesday,....., Sunday .   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By day within the month: Grouping the datetime property by day granularity within the month, the properties will be grouped into groups of 31 : 1, 2,....., 31, respectively representing 1st to 31st of the month .   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By week within the year: Group the datetime property by week granularity within the year, with the first week of each year as the week that falls on January 4 of that year, and Monday as the beginning of each week. Properties will be divided into 53 groups: 1, 2, ..., 53, representing the 1st to 53rd week of the year respectively.   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For example, the week in which January 4, 2025 is located is December 30, 2024 day to January 5, 2025, with a grouping value of "1" is the first week of 2025, which is December 30, 2024 day to January 5, 2025 this week .   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Quarterly: Grouping datetime properties by quarter, the properties will be divided into 4 groups: 1, 2, 3, and 4, representing 1 to 4 quarters respectively.   </div><br>   <br><br>* The data format and supported operators after grouping: The grouping rules created by the time type (datetime type) property, the property type is unified as the numerical type (int), and the supported operators when using custom grouping later are "=", "≠".<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c76ce635f5d14638a642b7bcbcb4b640~tplv-goo7wpa0wc-image.image) </span> |


<span id="bed2f4e0"></span>
### Property data format: list


|Property data type |Whether to support |Custom grouping logic |
|---|---|---|
|List |Not supported |The properties of the list type do not currently support custom grouping. |


<span id="8a3a7350"></span>
## Usage restrictions

Some preset properties, such as ab_version, user_is_new, etc., do not support grouping. The values of most of these preset properties are themselves grouped, so you don't need to group them manually again.

<span id="c07e6f97"></span>
## Operation steps

<span id="_2-1-新建自定义属性分组"></span>
### **New custom grouping rule**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06d87420fa7046ee9eb7e2ee95df71b8~tplv-goo7wpa0wc-image.image) </span>


* **Function Entry** : Analysis Tools \- Property Details \- Add Grouping Rules

* **Custom grouping rule configuration**:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0413351e06846109d219108c57723f1~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Property Group Name & Property Group Presentation Name |Custom property group name and display name for easy lookup and recognition in subsequent use. After the property group name is successfully created, modification is not supported. |
   |Property group permission |Supports setting whether the currently created property grouping is only available to itself or accessible to all.<br><br><br>* Self\-only: Only the creator of a custom group can view and use this group.<br><br>* Accessible to all: This group can be viewed and used by all project members. |
   |Property grouping rule |Properties in different data formats support different property grouping rules, as detailed in the Function Description section above. |
   


<span id="_2-2-使用自定义属性分组"></span>
### **Manage custom property grouping rules**


* **View** : In the properties drop\-down menu, below the original properties, you will see the property groupings you created and the ones accessible to all.

* **Modification: Modifying only groups where the owner is an individual is supported.**  Modifying a custom property group will affect all queries that use this custom property group. Please evaluate the impact carefully.


<span id="e361414b"></span>
# Property Filtering: Filtering the data to be analyzed

You can filter user behavior data based on reported property data to filter out target user data for analysis. If you create custom grouping rules for properties, you can also filter properties directly based on the custom grouping you create.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b6c3d9e041d4c88a61c4e384f6f159d~tplv-goo7wpa0wc-image.image) </span>


* Function entry: In various analysis tools and other pages, you can click the filter button to filter properties based on properties. In the case of event analysis, you can add property filtering when selecting a metric event, or property filtering when segmenting a target user.

* Function description:

   * When filtering properties, you can select properties in the drop\-down box, or you can select custom groups of properties that have been created.

   * When searching for properties, use fuzzy search to search for properties, user\-created custom property groupings, and public custom property groupings.

   * When filtering with any custom property grouping, the operator only supports "=" and "≠".


<span id="32349003"></span>
# Property grouping: query results are displayed in groups

<span id="85168b3d"></span>
## Function Description

With the property grouping function, you can group and display query analysis result data based on an property or custom property grouping rules. The following describes the main logic that supports the grouping and presentation of query results using properties from various dimensions.


* Property type dimension for grouping

   
   |Property type |Whether to support query result property group display |
   |---|---|
   |Event/user properties |Support.<br><br><br>* Contains virtual event/user properties.<br><br>* Contains preset event/user properties and custom event/user properties.<br><br>* Contains event public properties and event properties. |
   |User grouping |Support. |
   |User tag |Support, if the user label function is not turned on, it cannot be used. You need to turn on the function before you can use it. |
   

* Property data format dimension

   
   |Property data type |Property group presentation logic |Property grouping example |
   |---|---|---|
   |string<br><br>version<br><br>int<br><br>float<br><br>datetime<br><br>list |When performing property group display, DataFinder supports adding multiple property groups. Each property group display will be sorted according to the following logic and then display the query results.<br><br><br>1. The DataFinder is grouped according to the actual property value of the corresponding property.<br><br>2. After the grouping is completed, the DataFinder will cumulatively sum the indicators of the query in each property grouping, and sort the summation results in reverse order.<br><br>3. DataFinder will judge the display according to the maximum display of "first xxxx items" set by the interface.<br><br>   * If the actual number of subgroups is less than or equal to "top xxxx items", all grouping results are displayed.<br><br>   * If the actual number of groups is greater than the maximum "top xxxx items", only the set number of groups will be displayed according to the above sorting results.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Properties of type string/version/int/float/datetime are grouped, summed, and displayed according to the value of the property; properties of type list are grouped, summed, and displayed according to the elements in the list property.</div><br> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3eec680208f4b62b09055dae3e01674~tplv-goo7wpa0wc-image.image) </span><br><br><br>1. There is a string property "province", and the DataFinder will group the results of all provinces reported to the warehouse by value. Assuming that all the provinces reported to DataFinder include Beijing, Shanghai, Guangdong,..., Tokyo, Washington, etc., a total of 300 provinces, the DataFinder will be divided into 300 groups.<br><br>2. The metric queried in Event Analysis is "Total Number (PV) " for "User Registration" events, and DataFinder accumulates the "Total Number (PV) " for all "User Registration" events within each property grouping, sorted from highest to lowest by the sum result.<br><br>3. If the grouping display is set to display only the first 200 groupings, and there are 300 groupings after the actual grouping, only the sorted first 200 grouping results will be displayed in the query results. |
   |JSON |Currently, reporting properties of JSON type is not supported, and grouping properties of JSON type is not supported. If your property is of type JSON, see below [Use example](https://docs.byteplus.com/docs/DataFinder/Property_Custom_Grouping_and_Properties#3d2800e4). ||
   


<span id="4a163271"></span>
## Precautions

When using the property grouping feature, if you do not configure any property filters, DataFinder will default to a property filter for you: filter out data with property values of empty (null), so that you can better compare and see the metric data in each meaningful grouping .

Take event analysis as an example:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4757a28f90c84d1ea2d3541e6c27a762~tplv-goo7wpa0wc-image.image) </span>


* If you do not configure any property filtering conditions in the event metrics and segmentation filters, but only configure the use of the "platform type" property for grouping query results, then in the query results, DataFinder will filter out the indicator data with the "platform type" property value as empty, and only display the indicator results with platform type properties for you, and remove the data without platform type properties.

* If you configure property filters, property grouping will filter according to the property filter conditions you configure , and the property grouping function presets to filter out data with property values of empty (null). This filter condition no longer takes effect.


<span id="4e739bba"></span>
## Usage restrictions


* Currently, up to 20 property groups are supported.

* Each property grouping currently displays data for up to the first 1000 grouped results.


<span id="2b9db4e3"></span>
## Operation steps


1. In the query configuration area at the top of the analysis tool page, you can click **Property Grouping** to add a custom grouping rule for a property or property, and set the query result chart to display the grouped result data of the "top xx items" after sorting according to the grouping logic.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6872278d762841b6aa05625f96860d4b~tplv-goo7wpa0wc-image.image) </span>

2. For properties of type datetime, you can also set whether the query results need to be aggregated.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52a891676bca4efd8802800571bf0af6~tplv-goo7wpa0wc-image.image) </span>

   * Do not summarize (default): It is enough to group and display directly according to the selected datetime property, and the query result data is not processed.

   * Time period summary: Support selection by month, by minute, by hour, by day of the week and other time periods, the index data grouped by each property is summarized. Scenarios that wish to analyze user behavior characteristics within certain time periods may be summarized by time period, examples can be found below [Example 2: Analyzing the behavior of users from Monday to Sunday](https://docs.byteplus.com/docs/DataFinder/Property_Custom_Grouping_and_Properties#1d5d2e9f).


<span id="3d2800e4"></span>
# Use example

<span id="1fafd5b2"></span>
## Example 1: How nested JSON type properties are reported and used for filtering and grouping

The current DataFinder does not support direct reporting and use JSON type property data. If your business data itself is JSON type, you can refer to the following solutions for reporting and use.


* Example scenario: For example, a property of type JSON page_args:

   ```JSON
   {"page_args":{
       "moment_id":"123",
       "moment_type":123
       }
   }
   ```
   

* Event tracking report processing: In this scenario, it is currently recommended to convert JSON data into String by escaping and then report it. For example:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c14f0c66598e4e4d9f5f593c01530c3b~tplv-goo7wpa0wc-image.image) </span>

* Use after reporting:

   1. After escaping to a String type, you can use the virtual property feature in the DataFinder to create a virtual property, and in the definition expression of the virtual property, the `get_json_object ()`method extracts the value of the nested object in the corresponding JSON property. See virtual properties for details and instructions on how to use them [Virtual Properties](https://docs.byteplus.com/docs/DataFinder/Virtual_Properties).

      For example:

      ```SQL
      $vp_moment_type: toInt64OrZero(get_json_object(event_params.pages_args,'$.moment_type'))
      ```
      

      The above expression extracts the moment_type from the initial JSON property into the newly created $vp_moment_type virtual property.

   2. If you want to use this property value for filtering or grouping, you can directly select the virtual property $vp_moment_type.


<span id="1d5d2e9f"></span>
## Example 2: Analyzing the behavior of users from Monday to Sunday


* Example scenario: Suppose you have collected user behavior data from an application for half a year and want to analyze it to see if there are any differences in user behavior from Monday to Sunday.

* Property grouping example: You can set the property grouping "by day of the week" to summarize.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24ff6b50c12a4e98ab46dfd9505eb481~tplv-goo7wpa0wc-image.image) </span>

   Then when querying and displaying user behavior data later:

   * The query results will be divided into 7 groups by day of the week, representing Monday to Sunday.

   * Each group aggregates all the data for the corresponding group.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14253e422c024d48b7eb733b534ee6d8~tplv-goo7wpa0wc-image.image) </span>

      For example, in the example shown in the figure above, in the Monday grouping, the query results summarize the data for all Mondays in the query time frame (nearly 180 days, by month granularity).

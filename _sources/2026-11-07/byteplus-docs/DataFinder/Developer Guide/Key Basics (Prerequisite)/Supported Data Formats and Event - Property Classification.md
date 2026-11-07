---
title: "Supported Data Formats and Event/Property Classification"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification"
---

Growth analysis supports SDKs in multiple languages. The data reported by these SDK interfaces needs to use a unified data format in the underlying data model. The preset events/properties provided by the system have followed this unified data format. If you need custom events/properties, or have used other event tracking reporting tools before, you need to use DataFinder to define the data format of custom events/properties in strict accordance with the supported data formats. This article provides you with detailed data format requirements.

<span id="58a34278"></span>
# Background information

When collecting and reporting data using various types of SDKs:


* You need to integrate the corresponding SDK in each end first.

* Subsequent SDKs will report the collected data in JSON format.

* After receiving the reported data, the system will process the JSON data and drop it into the database. The data type after dropping the database has a corresponding relationship with the data type in the reported JSON.

   <img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI1MTlweCIgaGVpZ2h0PSIxMDBweCIgdmlld0JveD0iLTAuNSAtMC41IDUxOSAxMDAiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDMxMiA2NyBMIDM4NS42MyA2NyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM5MC44OCA2NyBMIDM4My44OCA3MC41IEwgMzg1LjYzIDY3IEwgMzgzLjg4IDYzLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIxOTIiIHk9IjM3IiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDY3cHg7IG1hcmdpbi1sZWZ0OiAxOTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+SlNPTjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjEyIiB5PSI3IiB3aWR0aD0iODAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTdweDsgbWFyZ2luLWxlZnQ6IDIxM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5TREsgY29sbGV0aW5nIGFuZCByZXBvcnRpbmc8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjQwMSIgeT0iMiIgd2lkdGg9IjExMCIgaGVpZ2h0PSIzMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTA4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTdweDsgbWFyZ2luLWxlZnQ6IDQwMnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5EYXRhIHByb2Nlc3NpbmcgJmFtcDsgc3RvcmluZyBpbiBkYXRhYmFzZTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzk2IiB5PSIzNyIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA2N3B4OyBtYXJnaW4tbGVmdDogMzk3cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRhdGEgaW4gZGF0YWJhc2U8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTEyIDY3IEwgMTg1LjYzIDY3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTkwLjg4IDY3IEwgMTgzLjg4IDcwLjUgTCAxODUuNjMgNjcgTCAxODMuODggNjMuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIiIHk9IjM3IiB3aWR0aD0iMTEwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEwOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDY3cHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFsbC1zaWRlcyBjb2RlIGludGVncmF0ZSBTREs8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjwvZz48L3N2Zz4=" />


Of which:


* When integrating the SDK at each end, some system preset events/properties support configuring whether to collect and report in the code, and also support defining custom events/properties.

* See the **Property Data Types** section below for details on the JSON data types that support collection and reporting, and the correspondence with the database data types after the database is dropped; see the **Log Structure** section below for examples of reported JSON.

* After the data collection is reported, the system processes the reported data. When the database is dropped, different types of data can be calculated to generate different index data, which is convenient for subsequent analysis and use. For details of supported calculation applications, please refer to the **different data types application** section below.

* For data collection reporting, see the section **Restrictions on reporting data** below.


<span id="bad3e525"></span>
# Event/**Property** Classification

According to the business data analytics scenario of growth analysis, Finder classifies events and properties at the following business level for you. Later, when you integrate the SDK and configure event tracking, you can configure the corresponding events/properties according to your business needs.


|**Event/Property Classification** ||**Business Meaning Statement** |
|---|---|---|
|System preset |Preset event public properties |General properties that are reported for each event preset by the system. For example, the device information class field reported by the Finder SDK. |
||Preset events and event properties |System preset event tracking events and event properties. |
||Preset user properties |System\-preset properties that describe the user's own state. |
|Custom |Custom event public properties |Customer\-defined event public properties other than the preset event public properties. |
||Custom events and event properties |Customer\-defined events and event properties other than preset events and event properties. |
||Custom user properties |Customer\-defined user properties other than the preset user properties. |


<span id="_1-属性数据类型"></span>
# 1. **Property** data types

<span id="0fe19d5c"></span>
## Precautions


* **When customizing events/properties, the value should not contain escape characters.** 

   When creating a custom event or property, ensure that the format of the corresponding event and property meets the format requirements of this article, and that the value of the custom property does not contain special characters such as escape character classes, such as "\ n". If you include such special characters, it may cause subsequent data to be reported successfully, but query analysis will lead to incorrect query results, you need to delete the special characters or use virtual properties, see [Microscope Function](https://docs.byteplus.com/docs/DataFinder/Microscope_Function)the FAQ in.

* **The data type of a property is determined by the data type at the first drop.** 

   For example, you added an event property to the console interface that has a data type of string. After the new creation is completed, this property has been dropped from the database. When the data is reported later, if the reported property data type changes to number again, it will not affect the property data type of the dropped database. It will only cause the reported property data type to be inconsistent with the property data type of the dropped database, resulting in possible reporting errors and other issues.

   You can view the data types of properties in your existing environment in **Application Management** \> **Data Management** in the console interface.


<span id="7fb56cc3"></span>
## **Property** data type correspondence

Property data types are as follows:


|**Acquisition Data Type \- Chinese Name** |**Acquisition data type \- JSON** |**Database type** |**Extra instructions** |**Sample data** |
|---|---|---|---|---|
|**integer** |number |int64 |Value range: [\-9223372036854775808, 9223372036854775807] |1024 |
|**floating point number** |number |float64 |8 bytes, maximum precision 16 bits |10.24 |
|**string** |string |string |UTF\-8 encoding, no longer than: |"1024" |
|**array** |array |list |Supports up to 500 elements, the element data type supports string, and all elements in an array must be of the same type.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the data falls into the database, the elements of the list will be deduplicated, such as [5, 5, 5], which becomes [5]; [5, 5, 6], which becomes [5, 6]; [5, 6, 5], which becomes [5, 6].</div><br> |["10", "24"] |
|**Date Time** |string |datetime |Reporting format:<br><br><br>* "yyyy\-MM\-dd HH:mm:ss"<br><br>* "Yyyy\-MM\-dd HH: mm: ss + Offset" (where + Offset is the time zone offset)<br><br>* "Yyyy\-MM\-dd HH: mm: ss. SSS" (where SSS is milliseconds)<br><br>* "Yyyy\-MM\-dd HH: mm: ss. SSS + Offset" (same as before)<br><br><br>Date range: [1970, 2099]<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a datetime report of the form "2020\-07\-07 01:22:33", the default is the time zone of the application level;</div><br><br><br><div data-tips="true" data-tips-type="tip">If you need to specify a timezone, you need to report the "2020\-07\-07 T13:46:08.342 + 08:00" format.</div><br> |"2020\-10\-24 23:47:12"<br><br>"2020\-10\-24 23:47:12+08:00"<br><br>"2020\-10\-24 23:47:12.102"<br><br>"2020\-10\-24 23:47:12.102+08:00" |
|**version** |string |string |The reporting format of version class data is:<br><br><br>* 2 to 6 segments<br><br>* Period Separation<br><br>* Each paragraph has a maximum of 5 digits.<br><br><br>When the system finds that the format of the value of the reported data matches, it will automatically set the data type to the version type. Version types can be sorted by a numeric collation or filtered by greater than and less than operators.<br><br>The regular expression corresponding to the format requirements is: ^ [0\-9] {1,5} (. [0\-9] {1,5}) {1,5} $<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the version type data is stored in storage, the data format is string, and it will be further processed as the version type data in subsequent query analysis. The filter conditions supported during query are the filter conditions supported by the version type data.</div><br> |"10.2"<br><br>"1.02.4"<br><br>"1.02.4.12345.22345.32345" |
|**Other types** |object/boolean |string |It supports reporting data of object and boolean (bool: yes/no) data types, but it will be converted into a string for storage. |\-\- |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The current DataFinder does not support directly collecting and reporting the data of the nested JSON structure. In this scenario, it is currently recommended to convert the JSON data into a String by escaping and then report it. For example:</div>


<div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7d252aefa294acb8160572704ccadbd~tplv-goo7wpa0wc-image.image" width="1049px" /></div>


<span id="_2-不同数据类型应用"></span>
# 2. Computing applications supported by different data types


* **Different property data types, computable metrics**

   
   |**Category** |**Analysis function** |**Data type** |**Calculation method** |
   |---|---|---|---|
   |event |event analysis |* (all) |total number of times<br><br>total headcount<br><br>per capita |
   |event |distribution analysis |* (all) |total number of times<br><br>days<br><br>hours |
   |event properties |general purpose |int<br><br>float |Press sum.<br><br>Press... find the average<br><br>press... average person<br><br>Press... for percentiles |
   |event properties |general purpose |Int<br><br>float<br><br>string<br><br>list<br><br>datetime |Press... to deduplicate<br><br>Press... deduplicate with user |
   

* **Different property data types, operators available as filter criteria**

   
   |**Type** |**Empty** |**Not empty** |**Equal** |**Not equal** |**Greater than** |**Less than** |**Greater than or equal to** |**Less than or equal to** |**Contain** |**Do not include** |**Regular match** |
   |---|---|---|---|---|---|---|---|---|---|---|---|
   |**string** |✓ |✓ |✓ |✓ | | | | |✓ |✓ |✓ |
   |**integer** |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ | | | |
   |**floating point** |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ | | | |
   |**array** |✓ |✓ | | | | | | |✓ |✓ | |
   |**Date Time** |✓ |✓ | | | | | | | | | |
   |**version** |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
   

   * The string type can be selected as "null" and "not null" to match null or non\-null.

   * The date type property has a separate filter (as shown in the table below):

   
   |**Operator name** |**Explain** |
   |---|---|
   |**fixed range** |The time of the selected property is within a fixed time frame, which can be any day or days from the last 365 days to the next 365 days. |
   |**At the current time** |The time of the selected property is between the time the query was initiated and the relative time period set by the user.<br><br>Optional conditions:<br><br><br>1. Past {N} hours {before, within, to {M} days} (value range: 1 < = N < = 365, N must be greater than M, 365 \> = N \> M \> 0)<br><br>2. Future {N} hours {before, within, to {M} days} (value range: 1 < = N < = 365, N must be less than M, 365 \> = N \> M \> 0) |
   |**Today and** |The time of the selected property is between the day the query was initiated (natural days) and the relative number of days (natural days) set by the user.<br><br>Optional conditions:<br><br><br>1. Past {N} days {before, within, to {M} days} (value range: 1 < = N < = 365, N must be greater than M, 365 \> = N \> M \> 0)<br><br>2. Future {N} days {before, within, to {M} days} (value range: 1 < = N < = 365, N must be less than M, 365 \> = N \> M \> 0) |
   |**In the event** |The time of the selected property is within a period of time relative to the current event. Due to the time of the event, this operator is only used as a filter for the event.<br><br>Optional conditions:<br><br><br>1. Day, Week, and Month: The natural day, week, or month on which the event occurred<br><br>2. Before {N} {days, seconds, minutes, hours, weeks} (the days and weeks at this time are not calculated as natural days or natural weeks, but are calculated from the time when the event occurs)<br><br>3. After {N} {days, seconds, minutes, hours, weeks} (same as before)<br><br><br>The value range of N:<br><br><br>* Day: 1 < = N < = 365 (currently executed according to the sky\-level limit)<br><br>* Second: 1 < = N < = 365<br><br>* Points: 1 < = N < = 365<br><br>* Hours: 1 < = N < = 168<br><br>* Week: 1 < = N < = 52 |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Considerations for selecting different data formats:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to sum, average, and filter according to the range of intervals, you must use int and float numeric types.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The data type that requires a time filter must be defined as the datetime format.   </div>
   


<span id="_3-上报数据限制"></span>
# 3. Restrictions on reporting data

<span id="_3-1-一般限制"></span>
## 3.1 General restrictions


* There is no limit to the total number of reported events for a single application.

* A single application supports no more than 1000 types of meta\-events (different applications do not affect each other, excluding virtual events).

* The recommended number of properties for a single event is within 300, and the maximum is 500 (different events do not affect each other).

* The maximum number of user properties should not exceed 500.

* The number of public properties of a single application custom event does not exceed 100;

* The event name is recommended to be no more than 64 characters and a maximum of 255 characters.

* Event property names and user property names should not exceed 64 characters.

* The length of the property value is recommended to not exceed 255 characters. In special cases (such as url, etc.) ;

* Event property names are prohibited from being user_unique_id, ssid, event_id;

* Property names are not allowed to be the same as preset property names; preset property documentation can be viewed [Preset Property Summary Table](https://docs.byteplus.com/docs/DataFinder/Preset_Property_Summary_Table).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the above limit is exceeded, the excess event and property data may be automatically discarded by the system. Please check out more <a href="https://docs.byteplus.com/docs/DataFinder/Storage_Details_Original_Data_Quality">Storage Details (Original Data Quality)</a>.</div>


<span id="_3-2-事件时间限制"></span>
## 3.2 Event time limit

With data imported by the client side SDK (iOS, Android), the server level by default only receives data within 7 days of the event occurrence time and 24 hours back.

<span id="_3-3-命名限制"></span>
## 3.3 Naming restrictions


1. In the Events table, the same property name is not allowed to have multiple property types, only one property type.

2. In the users table, the same property name is not allowed to have multiple property types, only one property type.

3. The same property name, if it exists in both the events and users tables, can have the same or different data types in both tables.


<span id="_3-4-属性长度和范围的限制"></span>
## 3.4 Limitations on property length and range


|**Chinese name** |**Database type** |**Extra instructions** |
|---|---|---|
|**integer** |int64 |Value range: [\-9223372036854775808, 9223372036854775807] |
|**floating point number** |float64 |8 bytes, maximum precision 16 bits |
|**string** |string | |
|**Version (string)**  |version(string) |Format: 1.2 to 6 paragraphs 2. English period separation 3. Maximum 5 digits per paragraph<br><br>Example: 1.1.2 4321 |
|**array** |list |Supports up to 500 elements, the element data type supports string, and all elements in an array must be of the same type. |
|**Date Time** |datetime |Date range: [1970, 2099] |


<span id="_4-日志结构"></span>
# 4. Data format description

DataFinder event data is divided into behavior data, user property data, and Item (business object) property data. The main process of data processing is depicted in the figure below. Data is collected and reported, internal data distribution, data processing, and finally data storage. In addition, offline/real\-time data docking capabilities are provided through bypass data output capabilities.

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3OTVweCIgaGVpZ2h0PSI0NTVweCIgdmlld0JveD0iLTAuNSAtMC41IDc5NSA0NTUiPjxkZWZzLz48Zz48cmVjdCB4PSI1MjIiIHk9IjE0MiIgd2lkdGg9IjI3MCIgaGVpZ2h0PSIyNDAiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIiIHk9IjIiIHdpZHRoPSI0OTAiIGhlaWdodD0iNDUwIiBmaWxsPSIjZTZlNmU2IiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDgyIDgyIEwgODIgMTAyIEwgMjQyIDEwMiBMIDI0MiAxMTUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNDIgMTIwLjg4IEwgMjM4LjUgMTEzLjg4IEwgMjQyIDExNS42MyBMIDI0NS41IDExMy44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIyIiB5PSIyMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZDVlOGQ0IiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1MnB4OyBtYXJnaW4tbGVmdDogMjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Q2xpZW50LXNpZGUgU0RLPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDI0MiA4MiBMIDI0MiAxMTUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNDIgMTIwLjg4IEwgMjM4LjUgMTEzLjg4IEwgMjQyIDExNS42MyBMIDI0NS41IDExMy44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjE4MiIgeT0iMjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2Q1ZThkNCIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNTJweDsgbWFyZ2luLWxlZnQ6IDE4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5TZXJ2ZXItc2lkZcKgU0RLPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDQwMiA4MiBMIDQwMiAxMDIgTCAyNDIgMTAyIEwgMjQyIDExNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDI0MiAxMjAuODggTCAyMzguNSAxMTMuODggTCAyNDIgMTE1LjYzIEwgMjQ1LjUgMTEzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzQyIiB5PSIyMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZDVlOGQ0IiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1MnB4OyBtYXJnaW4tbGVmdDogMzQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkJ1c2luZXNzIGFwcGxpY2F0aW9ucyBkaXJlY3RseSBjYWxsIE9wZW5BUEk8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjQyIDE1MiBMIDI0MiAxNzQuNSBMIDgyIDE3NC41IEwgODIgMTkwLjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gODIgMTk1Ljg4IEwgNzguNSAxODguODggTCA4MiAxOTAuNjMgTCA4NS41IDE4OC44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjQyIDE1MiBMIDI0MiAxOTAuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNDIgMTk1Ljg4IEwgMjM4LjUgMTg4Ljg4IEwgMjQyIDE5MC42MyBMIDI0NS41IDE4OC44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjQyIDE1MiBMIDI0MiAxNzQuNSBMIDQxMiAxNzQuNSBMIDQxMiAxOTAuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MTIgMTk1Ljg4IEwgNDA4LjUgMTg4Ljg4IEwgNDEyIDE5MC42MyBMIDQxNS41IDE4OC44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIyIiB5PSIxMjIiIHdpZHRoPSI0NDAiIGhlaWdodD0iMzAiIHJ4PSI0LjUiIHJ5PSI0LjUiIGZpbGw9IiNkNGUxZjUiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDQzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEzN3B4OyBtYXJnaW4tbGVmdDogMjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RGF0YSBjb2xsZWN0aW5nIGFuZCByZXBvcnRpbmc8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjQyIDMyMiBMIDI0MiAzNDcgTCA4MiAzNDcgTCA4MiAzNjUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA4MiAzNzAuODggTCA3OC41IDM2My44OCBMIDgyIDM2NS42MyBMIDg1LjUgMzYzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMjIiIHk9IjM3MiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmMmNjIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA0MDJweDsgbWFyZ2luLWxlZnQ6IDIzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPmV2ZW50IHJlcG9ydHMgZGF0YTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAyNDIgMjU3IEwgMjQyIDI4NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDI0MiAyOTAuODggTCAyMzguNSAyODMuODggTCAyNDIgMjg1LjYzIEwgMjQ1LjUgMjgzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTgyIiB5PSIxOTciIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZmZjJjYyIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjI3cHg7IG1hcmdpbi1sZWZ0OiAxODNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGI+VXNlciBkYXRhPC9iPjxiciAvPjxiciAvPnVzZXJfcHJvZmlsZSByZXBvcnRzIGRhdGE8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjE4MiIgeT0iMzcyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmYyY2MiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDQwMnB4OyBtYXJnaW4tbGVmdDogMTgzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPnVzZXJfcHJvZmlsZSByZXBvcnRzIGRhdGE8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjQyIDMyMiBMIDI0MiAzNDcgTCA0MTIgMzQ3IEwgNDEyIDM2NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQxMiAzNzAuODggTCA0MDguNSAzNjMuODggTCA0MTIgMzY1LjYzIEwgNDE1LjUgMzYzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA0MTIgMjU3IEwgNDEyIDI3NyBMIDI0MiAyNzcgTCAyNDIgMjg1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjQyIDI5MC44OCBMIDIzOC41IDI4My44OCBMIDI0MiAyODUuNjMgTCAyNDUuNSAyODMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzNTIiIHk9IjE5NyIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmMmNjIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMjdweDsgbWFyZ2luLWxlZnQ6IDM1M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Yj5EZXZpY2UgZGF0YTwvYj48YnIgLz48YnIgLz5pdGVtX3Byb2ZpbGUgcmVwb3J0cyBkYXRhPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzNTIiIHk9IjM3MiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmMmNjIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA0MDJweDsgbWFyZ2luLWxlZnQ6IDM1M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5pdGVtX3Byb2ZpbGUgc3RvcmVzIGluIGRhdGFiYXNlPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDI0MiAzMjIgTCAyNDIgMzY1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjQyIDM3MC44OCBMIDIzOC41IDM2My44OCBMIDI0MiAzNjUuNjMgTCAyNDUuNSAzNjMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMiIgeT0iMjkyIiB3aWR0aD0iNDQwIiBoZWlnaHQ9IjMwIiByeD0iNC41IiByeT0iNC41IiBmaWxsPSIjZDRlMWY1IiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA0MzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMDdweDsgbWFyZ2luLWxlZnQ6IDIzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRhdGEgcHJvY2Vzc2luZyAmYW1wOyBzdG9yaW5nIGluIGRhdGFiYXNlPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDgyIDI1NyBMIDgyIDI3NyBMIDI0MiAyNzcgTCAyNDIgMjg1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjQyIDI5MC44OCBMIDIzOC41IDI4My44OCBMIDI0MiAyODUuNjMgTCAyNDUuNSAyODMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMiIgeT0iMTk3IiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmYyY2MiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIyN3B4OyBtYXJnaW4tbGVmdDogMjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGI+QmVoYXZpb3IgZGF0YTwvYj48YnIgLz48YnIgLz5ldmVudCByZXBvcnRzIGRhdGE8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNjEyIDI2MiBMIDY0MiAyNjIgTCA2NDIgMjEyIEwgNjY1LjYzIDIxMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDY3MC44OCAyMTIgTCA2NjMuODggMjE1LjUgTCA2NjUuNjMgMjEyIEwgNjYzLjg4IDIwOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA2MTIgMjYyIEwgNjQyIDI2MiBMIDY0MiAzMTIgTCA2NjUuNjMgMzEyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjcwLjg4IDMxMiBMIDY2My44OCAzMTUuNSBMIDY2NS42MyAzMTIgTCA2NjMuODggMzA4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI1NTIiIHk9IjE4MiIgd2lkdGg9IjYwIiBoZWlnaHQ9IjE2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjNjY2NmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA1OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDI2MnB4OyBtYXJnaW4tbGVmdDogNTUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5EYXRhIE91dHB1dDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNjcyIiB5PSIxODIiIHdpZHRoPSIxMDAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iIzY2NjZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMTJweDsgbWFyZ2luLWxlZnQ6IDY3M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBmb250LXdlaWdodDogYm9sZDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RGF0YSBleHBvcnQ8YnIgLz5PcGVuQVBJPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NzIiIHk9IjI4MiIgd2lkdGg9IjEwMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjNjY2NmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMxMnB4OyBtYXJnaW4tbGVmdDogNjczcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5XZWJob29rLy4uLi4uLjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA0OTIuNSAyNjkuNSBMIDQ5Mi41IDI1My41IEwgNDk5LjUgMjUzLjUgTCA0OTkuNSAyNDMgTCA1MjEuNSAyNjEuNSBMIDQ5OS41IDI4MCBMIDQ5OS41IDI2OS41IFoiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjwvZz48L3N2Zz4=" />


* In the process of reporting data collection through the Data Access SDK or OpenAPI, see the **data collection reporting format** section below for details on the data collection reporting format.

* In the privatization scenario, the event tracking data collected and reported into the DataFinder and distributed internally supports subscription through Kafka. For details of the data format when Kafka subscribes, please refer to the **Kafka Subscription Data Format** section below.

* DataFinder will process the data collected and reported and stored in the inventory. For the data format after the database, please refer to the **data warehousing format** section below.

* DataFinder provides you with a data output function that supports the output of the collected data. For the data format of the external output, please refer to the **Data External Output Format** section below.


<span id="614b343d"></span>
## Data collection reporting format


* The reporting data format is based on a JsonObject and consists of three core components:

   
   |Reporting data components |Detailed description |
   |---|---|
   |**header** |Global public properties are one\-to\-many related to events, and a batch of reported events will correspond to the same header public property. The content of the header is subject to the value of the above timepiece, not the value when the event occurs. Therefore, it is not recommended to set the strong binding in the header if the change is frequent and the event is generated. |
   |**events** |Contains a list of all events reported this time. Events is the main information carrier for all types of data reporting. Generally, each event includes:<br><br><br>* Event: event name, the **type name of some scenes to report special data**<br><br>* Params: data content, the content is json string or Json escape string. The key value of parmas is different in each reported event. In the behavior event report, it is the event property, the preset property and its corresponding value.<br><br><br>(On the iOS/Android side, the event reporting field is **event_v3** , which is equivalent to events) |
   |**user** |User ID, the content is Json string, **some scenes do unique type reporting logo**<br><br>(Some SDK/client side /Http OpenApi will report directly in the form of user_unique_id key\-value pairs, and the field location may also be placed in the Header) |
   |Special instructions |* In addition to the above three parts, each end/SDK will add its own unique key in the time report, please refer to the documentation of each end/SDK for details.<br><br>* Some data reporting **does not follow** a common format, using API\-specific formats to report/update data. |
   

* Example of reporting data: behavioral data

   
   <Tabs>
   <Tab zoneid="AbPaOn7h2M" title="Example of event reporting by Web JavaScript SDK">
   <TabTitle>Example of event reporting by Web JavaScript SDK</TabTitle>
   
   ```JSON
   {
       "events": [
           {
               "event": "report-core",
               "params": "{\"timePoints\":8041,\"pageChanged\":false,\"url\":\"https://datarangers-onpremise.volces.com/datafinder/project/1/overview\",\"index\":6,\"event_index\":1723194789910}",
               "local_time_ms": 1723194773504,
               "is_bav": 1,
               "session_id": "dc3b61d7-de7d-4f8d-b5bd-2f70******"
           },
           {
               "event": "report-core",
               "params": "{\"timePoints\":7963,\"pageChanged\":false,\"url\":\"https://e168-2-169.datarangers-onpremise.volces.com/datafinder/project/1/overview\",\"index\":3,\"event_index\":1723194789909}",
               "local_time_ms": 1723194773426,
               "is_bav": 1,
               "session_id": "dc3b61d7-de7d-4f8d-b5bd-2f707*******"
           }
       ],
       "user": {
           "user_unique_id": "1",
           "web_id": "73742566315817*****"
       },
       "header": {
           "app_id": 666***,
           "os_name": "mac",
           "os_version": "10_15_7",
           "device_model": "Macintosh",
           "language": "zh-CN",
           "platform": "web",
           "sdk_version": "5.1.25",
           "sdk_lib": "js",
           "timezone": 8,
           "tz_offset": -28800,
           "resolution": "2304x1296",
           "browser": "Chrome",
           "browser_version": "126.0.0.0",
           "referrer": "",
           "referrer_host": "",
           "width": 2304,
           "height": 1296,
           "screen_width": 2304,
           "screen_height": 1296,
           "tracer_data": "{\"$utm_from_url\":1}",
           "custom": "{\"product_name\":\"DataFinder\",\"op_project_id\":1,\"op_project_name\":\"Q2套件联动项目\",\"org_id\":1,\"org_name\":\"默认集团\",\"overview_org_id\":1,\"custom_module_name\":\"overview\"}"
       },
       "local_time": 1723194773
   }
   ```
   
   
   
   </Tab>
   <Tab zoneid="rCDiY90rdo" title="Android side report example">
   <TabTitle>Android side report example</TabTitle>
   
   ```JSON
   {
       "magic_tag": "ss_app_log",
       "header": {
           "user_unique_id": "demo-user",
           "platform": "Android",
           "sdk_lib": "Android",
           "device_model": "M2012K11AC",
           "device_brand": "Redmi",
           "device_manufacturer": "Xiaomi",
           "cpu_abi": "arm64-v8a",
           "sdk_target_version": 29,
           "git_hash": "9******",
           "os": "Android",
           "os_api": 33,
           "os_version": "13",
           "sdk_version": 6161052,
           "sdk_version_code": 16160651,
           "sdk_version_name": "6.16.10-rc2",
           "channel": "rangers-applog-android-demo",
           "not_request_sender": 0,
           "aid": "41****",
           "app_region": "CN",
           "density_dpi": 440,
           "display_density": "xxhdpi",
           "resolution": "2400x1080",
           "language": "zh",
           "timezone": 8,
           "region": "CN",
           "tz_name": "Asia\/Shanghai",
           "tz_offset": 28800,
           "mc": "02:00:00:00:00:00",
           "build_serial": "",
           "sim_serial_number": [],
           "access": "wifi",
           "package": "com.bytedance.applog_android_demo",
           "app_version": "1.0",
           "app_version_minor": "",
           "version_code": 1,
           "update_version_code": 1,
           "manifest_version_code": 1,
           "display_name": "AppLogDemo",
           "rom": "MIUI-V14.0.8.0.TKHCNXM",
           "rom_version": "miui_V140_V14.0.8.0.TKHCNXM",
           "register_time": 1724047691534,
           "sig_hash": "426ae63a9a05da4fb9fab2d62******",
           "sim_region": "gb",
           "clientudid": "8c147ad4-cef8-44ca-80c9-290a64******",
           "openudid": "bd847f5860******",
           "cdid": "a993ec8b-c84b-45e8-a500-8b513c******",
           "oaid": "8413ca902******",
           "bd_did": "U4OQ2JBC4WXYORCJ2YIG3W3R6J4KFADIZYITIEI2NNX33KH******",
           "install_id": "19246099776******",
           "ssid": "d51f5553-fe09-4354-9d3e-77f974******"
       },
       "time_sync": {
           "server_time": 1724047683,
           "local_time": 1724047769
       },
       "launch": [
           {
               "local_time_ms": 1724048552318,
               "tea_event_index": 1001,
               "session_id": "a3a90b05-3f81-41b8-a975-6275a5******",
               "user_unique_id": "demo-user",
               "ssid": "d51f5553-fe09-4354-9d3e-77f974******",
               "datetime": "2024-08-19 14:22:32",
               "$page_title": "AppLogDemo",
               "$page_key": "com.bytedance.applog_android_demo.ui.MainActivity",
               "$resume_from_background": "true"
           }
       ],
       "terminate": [
           {
               "local_time_ms": 1724047719134,
               "tea_event_index": 1004,
               "session_id": "ca5d7949-975d-40e7-a204-c20a21******",
               "stop_timestamp": 1724047719,
               "duration": 9,
               "datetime": "2024-08-19 14:08:39",
               "user_unique_id": "demo-user",
               "ssid": "d51f5553-fe09-4354-9d3e-77f974******",
               "launch_from": 1,
               "$page_title": "AppLogDemo",
               "$page_key": "com.bytedance.applog_android_demo.ui.MainActivity",
               "activites": [
                   [
                       "com.bytedance.applog_android_demo.ui.MainActivity",
                       10
                   ]
               ]
           }
       ],
       "event_v3": [
           {
               "local_time_ms": 1724047709380,
               "datetime": "2024-08-19 14:08:29",
               "tea_event_index": 1014,
               "session_id": "ca5d7949-975d-40e7-a204-c20a21******",
               "user_unique_id": "demo-user",
               "ssid": "d51f5553-fe09-4354-9d3e-77f974******",
               "event": "bav2b_page",
               "is_bav": 1,
               "params": {
                   "page_key": "com.bytedance.applog_android_demo.ui.MainActivity",
                   "refer_page_key": "",
                   "is_back": 1,
                   "duration": 9754,
                   "page_title": "AppLogDemo",
                   "refer_page_title": "",
                   "page_path": "com.bytedance.applog_android_demo.ui.MainActivity",
                   "referrer_page_path": "",
                   "$app_version": "1.0"
               }
           }
       ],
       "local_time": 1724048552
   }
   ```
   
   
   
   </Tab>
   <Tab zoneid="B64e2aq7DJ" title="Example of iOS reporting">
   <TabTitle>Example of iOS reporting</TabTitle>
   
   ```XML
   {
       "event_v3" : [
         {
           "local_time_ms" : 1741080789854,
           "$user_unique_id_type" : null,
           "params" : {
             "page_title" : "Title",
             "refer_page_manual_key" : "null(launch)",
             "refer_page_key" : "null(launch)",
             "page_key" : "MainViewController",
             "refer_page_title" : "null(launch)",
             "$app_version" : "1.0",
             "_additional" : "ddd"
           },
           "event" : "bav2b_page",
           "user_unique_id" : null,
           "ab_sdk_version" : "1328,1313",
           "track_id" : "DC02C87C-AC5F-4F19-B040-D66CCC******",
           "ssid" : "46f3c7f0-11bd-4665-b918-140ba6******",
           "session_id" : "12C76765-710D-4B8F-A82B-815932******",
           "nt" : 1,
           "datetime" : "2025-03-04 17:33:09",
           "tea_event_index" : 1881
         }
       ],
       "time_sync" : {
         "local_time" : 1741077898,
         "server_time" : 1741077898
       },
       "magic_tag" : "ss_app_log",
       "header" : {
         "app_version_minor" : "1",
         "region" : "CN",
         "access" : "mobile",
         "os_version" : "18.3.1",
         "device_model" : "iPhone17,4",
         "user_unique_id_type" : null,
         "platform" : "ios",
         "app_name" : "applog_oc_demo",
         "vendor_id" : "3F23F3D3-8BAD-4A58-BE17-C26A22******",
         "sdk_version" : 61702,
         "display_name" : "ObjCExample",
         "channel" : "App Store",
         "sdk_lib" : "ios",
         "app_region" : "CN",
         "ab_sdk_version" : "1328,1313",
         "user_agent" : "ObjCExample 1.0 rv:1 (iphone; iOS 18.3.1; en_CN)",
         "idfa" : "00000000-0000-0000-0000-000000000000",
         "device_platform" : "iphone",
         "install_id" : "1950995378******",
         "user_unique_id" : null,
         "os" : "iOS",
         "tz_name" : "Asia\/Shanghai",
         "tz_offset" : 28800,
         "app_language" : "en",
         "is_upgrade_user" : false,
         "aid" : "418165",
         "ssid" : "46f3c7f0-11bd-4665-b918-140ba6******",
         "package" : "com.data.extrackerzw",
         "is_jailbroken" : false,
         "language" : "zh",
         "sdk_version_code" : 10061702,
         "bd_did" : "66RRMWG6ALLWZYNCPFORUL5YY3ENZDYWCN4XU7JL73S6EKH6******",
         "app_version" : "1.0",
         "resolution" : "1290*2796",
         "timezone" : 8
       },
       "launch" : [
         {
           "start_timestamp" : 1741080789,
           "$resume_from_background" : true,
           "user_unique_id" : null,
           "app_version" : "1.0",
           "$user_unique_id_type" : null,
           "local_time_ms" : 1741080789567,
           "ab_sdk_version" : "1328,1313",
           "track_id" : "3884587B-D7F9-47CC-91D1-77C1F4******",
           "ssid" : "46f3c7f0-11bd-4665-b918-140ba6******",
           "session_id" : "12C76765-710D-4B8F-A82B-815932******",
           "tea_event_index" : 1880,
           "datetime" : "2025-03-04 17:33:09",
           "nt" : 1
         }
       ],
       "local_time" : 1741080790
     }
   ```
   
   
   
   </Tab>
   </Tabs>
   

   Combining the above examples, we can see that:

   * The header part contains the global public properties of the application perspective such as the operating system and device where the application is located; the web side also includes the application identification app_id, and the information on the Android side is included in the authentication information, which will be filled in the subsequent data stream processing.

   * In the user part, on the Android side, the user information is placed in the header in user_unique_id key\-value pairs; the Web side contains two user identities: user_unique_id and web_id, which are used to generate/match the Finder's user unique identity after reporting.

   * Events/event_v3 contains multiple behavior events in list format, in each event, event is the name of the behavior, params is the non\-global verbose property of the event, and is a Json string or Json escape string of multiple key\-value pairs.

      Some of the information in header, user, events/event_v3 is part of the terminal/SDK to report its own properties, which are automatically generated when reporting.

* Report Data Example: User Property Data

   The following is an example of user property data reporting :

   ```JSON
   {
       "user": {
           "user_unique_id": "74481585297"   //user unique identifier
       },
       "header": {
           "ab_sdk_version": "91223,83097",   //AB test vid
           "app_channel": "App Store",    //App channel
           "app_name": "news_article",    //App name
           "app_package": "com.ss.android.article.news",   //App package name
           "app_version": "5.1.3",        //App version
           "client_ip": "10.100.1.1",     //client side ip address
           "device_model": "SM-G9250",    //Equipment model
           "os_name": "Android",          //operating system
           "os_version": "6.0.1",         //operating system version
           "traffic_type": "app"
       },
       "events": [
           {
               "event": "__profile_set",    //operation name
               "params": "{\"age\": 10}",    //set properties
               "local_time_ms": 1489573628001   //the timestamp of the event
           }，
           {
               "event": "__profile_unset",    //operation name
               "params": "{\"name\":\"tom\"}",    //set properties
               "local_time_ms": 1489573628001   //the timestamp of the event
           }
       ]
   }
   ```
   

   In this example, the reported data follows the user, header, and events segments.

   * In the events section, the first and second event values represent the name of the specific operation rather than the event name, as __profile_set indicates a user property setting operation;

   * Params is the data content of the operation. [5.1 Reporting user properties](https://docs.byteplus.com/docs/DataFinder/HTTP_API#_5-1-%E4%B8%8A%E6%8A%A5%E7%94%A8%E6%88%B7%E5%B1%9E%E6%80%A7)

* Report data example: Item property data

   The following is an example of user property data reporting :

   
   <Tabs>
   <Tab zoneid="HdBiQevXyY" title="Item attribute reporting example">
   <TabTitle>Item attribute reporting example</TabTitle>
   
   ```JSON
   {
       "user": {
           "user_unique_id": "__rangers"   //Business object report, fixed as __rangers
       },
       "header": {
           "app_name": "8ca70e31ea744de18a1407a750c4e281" //app_name value, one-to-one correspondence with app_id
       },
       "events": [
           {
               "event": "__item_set",
               "params": "{\"item_name\":\"Mobile_No\",\"item_id\":\"item_test_002\",\"device_model\":\"thinkphone\"}",
               "local_time_ms": 1721735668446
           }
       ]
   }
   ```
   
   
   
   </Tab>
   <Tab zoneid="ZfZ0qSs8Ti" title="Item event correlation reporting example">
   <TabTitle>Item event correlation reporting example</TabTitle>
   
   ```JSON
   {
       "user": {
           "user_unique_id": "74481585297"
       },
       "header": {
           "app_name": "8ca70e31ea744de18a1407a750c4e281"
       },
       "events": [
           {
               "event": "video_play",
               "params": { "title": "video title 5!",
       "__items": "[{\"Mobile_No\":[{\"id\":\"item_test_002\"}]}]"},
               "local_time_ms": 1721735668446
           }
       ]
   }
   ```
   
   
   
   </Tab>
   </Tabs>
   

   In this example, the reported data follows the user, header, and events segments:

   * In the Item property report, user_unique_id is not the meaning of the user identity, but is reported through the __rangers identification of the user property;

   * With the value of the event __item_set represented as a specific data operation,

   * The value in params is the specific data of an Item. In the Item association report, use __items in the params field to indicate that this part of the data is the association between the configuration event video_play and Item. The remaining keys are reported as normal behavior event properties.


<span id="c41f13cb"></span>
## Data warehousing format

The data formats that can be seen after warehousing are as follows:


* **SaaS**

   ```Plain
   {
           "user": {
               "ssid": "",                // SSID
               "user_unique_id": "",      // user_unique_id, stored in string_profiles{'uuid'}
               "web_id": 0,               // anonymous ID of website-side, stored in string_profiles{'web_id'}
               "device_id": 0,            // anonymous ID of mobile-side and Mini-program side
               "user_register_time": ""   // User first event triggering time
           },
           "params": {
               "language": "zh-CN",
               "region": "",
               "app_version": "unknown",
               "app_region": "",
               "app_channel": "",
               "app_language": "",
               "os_version": "10",
               "os_name": "10",
               "device_model": "Windows NT 10.0",
               "device_brand": "",
               "network_type": "",
               "network_carrier": ""
           },
           "items":{
               "sku": [{
                   "id": "",
                   "property_1": "",     // property 1 defined by current item
                   "property_1": "",     // property 2 defined by current item
               }]
           },
           "event_name": "predefine_pageview",
           "app_id": "2174",             // string, application id in rangers
           "app_name": "数据发现者",       // string, application name in rangers
           "server_time": 1606783082,    // int(timestamp), the time when the server receives the event, accurate to milliseconds
           "time": 1606783080,           // int(timestamp), time = local_time_ms/1000, The unit is seconds.
           "event_date": 1606783080      // date, calculated based on time, but only accurate to days.
   }
   ```
   


<span id="99c92c36"></span>
## Data output format

Data that has been warehoused can be queried and analyzed directly on the DataFinder, and it also supports exporting data to other analysis platforms, such as exporting data to your data warehouse.

<span id="_5-faq"></span>
# 5.FAQ

<span id="q1：事件属性数据类型传输错误，需要修改怎么办？"></span>
### **Q1: Event property data type transmission error, how to modify?** 

Description: During the business iteration process, the meaning of the property changes, or an error occurs during the reporting process, and what should I do if it needs to be modified?

**A1:** 


1. Step 1: The administrator modifies the product front\-end interface and selects Application Management \- Data Management.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0ce309ff1ad4aceb427b15950715862~tplv-goo7wpa0wc-image.image) </span>

2. Step 2: Find the corresponding property name.

   The preset properties in the figure (properties collected by the growth analysis SDK by default, no need to report manually) The data type is gray, indicating that it cannot be modified. Only properties reported manually during code event tracking can be modified.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fbba26c26ea45ae999737964a2aa0ee~tplv-goo7wpa0wc-image.image) </span>

3. Step 3: Select the modified property type.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_38d32287218f9db76158725dda7e703a) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13dc1e019027412d93ae66a00e67bb7e~tplv-goo7wpa0wc-image.image) </span>

   The system will prompt you according to the modified data type, and the conversion data rules are as follows. Only for event properties, not for user properties.

   
   |**Raw data type** |**Raw data example** |**New data types** |**New data example** |**Historical data** |**New data** |Other instructions |
   |---|---|---|---|---|---|---|
   |Value is a numeric class string |"1" |int |1 |Do not lose |Report according to the new data type, and the warehousing is normal. |Allows modification, and historical data is not lost, can be queried. |
   |Value is a numeric class string |"0.1" |float |0.1 |Do not lose |Report according to the new data type, and the warehousing is normal. | |
   |Value is a non\-numeric string |"abc" |int |0 |damaged |Report according to the new data type, and the warehousing is normal. | |
   |float |0.1，0.61.1，1.7 |int |Round down (take the integer before the decimal point), 0.1, 0.6 will become 0; 1.1 and 1.7 will become 1. |Do not lose |Report according to the new data type, and the warehousing is normal. | |
   |int |1 |string |lost |lost |Report according to the new data type, and the warehousing is normal. |Allows modification, but the historical data can no longer be queried, and then changed back to the original type, it is still available. For example, string\- \> int\- \> string. |
   |int |1 |float |lost |lost |Report according to the new data type, and the warehousing is normal. | |
   |float |0.1 |string |lost |lost |Report according to the new data type, and the warehousing is normal. | |
   |In addition to the above table, in other cases of conversion, such as string\-datetime, historical data will be lost, reported according to the new data type, warehousing is normal, and it cannot be converted to the original type. The operation is irreversible. Please proceed with caution. | | | | | | |
   

4. Step 4: You need to develop the code level and report it according to the new data format.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After modifying the front\-end data type, please modify the code in time, otherwise there will be warehousing failure or data loss.</div>


<span id="q2：-各端数据类型传输不一致，系统如何处理？如何修改？"></span>
### **Q2: The data type transmission at each end is inconsistent. How does the system handle it? How to modify it?** 

Description: For example, the IOS side first passes in the format of the A property as a numeric type, and the Android side passes in the format of the A property as a string type. How does the system handle it at this time, and what will the result be?

**A2** : The type of an property is determined by the data type imported for the first time. If data of different data types is passed in later, the system will try to convert it. If the conversion is successful, it will be put into storage. If the conversion fails, the property information value is' 0 'into storage, which is equivalent to the loss of property information, but the event is reported normally.

The specific conversion success information is as follows:


|**Raw data type** |**New data types** |**Is the conversion successful?**  |**Other instructions** |
|---|---|---|---|
|int、float、datetime、list |string |Yes | |
|Numeric string, e.g. '1', '0.1' |int、float |Yes |The original data type is string, but the value is the number 123456. |
|float |int |Yes |However, the data after the decimal point will be lost. |
|int |float |Yes | |
|The remaining data types failed to be converted. | | | |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is necessary to avoid this problem on the data verification side. If it occurs, please adjust the data format on the wrong side in time, otherwise it will cause data loss.</div>


<span id="q3：-是否接受时间戳string的上报，会自动解析成datetime格式吗？"></span>
### **Q3: Do you accept the reporting of timestamp string, will it be automatically parsed into datetime format?** 

**A3**: timestamp is not supported, only date and time formats are supported.

<span id="q4：datetime是否接受按天级别格式的数据，-yyyy-mm-dd"></span>
### **Q4: Whether datetime accepts data in day\-level format, "yyyy\-MM\-dd"** 

**A4**: Not supported. The supported datetime reporting format is "yyyy\-MM\-dd HH: mm: ss".

<span id="q5：-埋点-设计时，如何选择正确的数据类型？"></span>
### **Q5: How to choose the correct data type when designing event tracking?** 


|**Chinese name** |**Database type** |**Application scenario** |
|---|---|---|
|**integer** |int64 |Numerical sums, averages, and other calculations are required, and there will be no decimal cases. For example: age, integer amount. |
|**floating point number** |float64 |Numerical sums, averages, and other calculations are required, and decimal cases will occur. For example: discount amount, duration. |
|**string** |string |Common text class properties, such as: page title, button name, product category. ID types that do not need to be calculated, such as content ID, product ID. |
|**array** |list |Collections, a property has multiple values, but filtering requires a single filter. Example: An entertainment news item belongs to multiple content tags, {'Hot', 'Entertainment', 'News'} Example: An item belongs to multiple product tags |
|**Date Time** |datetime |Those that need to be filtered by date range |
|**version** |string |When you need to sort versions |


<span id="q6：为什么会一段的版本值？不是版本格式要求至少两段么？"></span>
### **Q6: Why is there a version\-related field with a value format of "xx" instead of a value format of at least two paragraphs such as "xx.xx"?** 

By default, when the system encounters data that has been cut into at least two segments by "." (e.g. 2.0), it automatically determines that it is a version type. For fields of known version types, DataFinder will release this restriction, allowing the value of the version field to be reported without ".", for example: 2.

This restriction is lifted in such scenarios because in some cases, the true version number is only one paragraph. Of course, in this case, you can also choose to report the version number as an int.

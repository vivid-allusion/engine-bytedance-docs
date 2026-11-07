---
title: "Supported Data Formats (Custom Events/Properties)"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Supported-Data-Formats-Custom-Events-Properties"
---

DataTester supports SDKs in multiple languages. The data reported by these SDK interfaces needs to use a unified data format in the underlying data model. The preset events/properties provided by the system have followed this unified data format. If you need custom events/properties, you need to define the data format of custom events/properties strictly according to the supported data formats. This article provides you with detailed data format requirements.

<span id="d77c2a88"></span>
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


<span id="7a712f36"></span>
# Event/**Property** Classification

According to the business data analytics scenario of growth analysis, Finder has classified the events and properties at the following business level for you. Later, when you integrate the SDK and configure the event tracking, you can configure the corresponding events/properties according to your business needs.


|**Event/Property Classification** ||**Business Meaning Statement** |
|---|---|---|
|System preset |Preset event public properties |General properties that are reported for each event preset by the system. For example, the device information class field reported by the Finder SDK. |
||Preset events and event properties |System preset event tracking events and event properties. |
||preset user properties |System\-preset properties that describe the user's own state. |
|Custom |Custom event public properties |Customer\-defined event public properties other than the preset event public properties. |
||Custom events and event properties |Customer\-defined events and event properties other than preset events and event properties. |
||custom user properties |Customer\-defined user properties other than the preset user properties. |


<span id="adb3a7f7"></span>
# 1. **Property** data types

<span id="f31fbdeb"></span>
## Precautions


* **When customizing events/properties, the value should not contain escape characters.** 

   When creating a custom event or property, ensure that the format of the corresponding event and property meets the format requirements of this article, and that the value of the custom property does not contain special characters such as escape character classes, such as "\ n". If you include such special characters, it may cause subsequent data to be reported successfully, but the query results will be incorrect during query analysis. You need to delete the special characters or use virtual properties.

* **The data type of a property is determined by the data type at the first drop.** 

   For example, you added an event property to the console interface that has a data type of string. After the new creation is completed, this property has been dropped from the database. When the data is reported later, if the reported property data type changes to number again, it will not affect the property data type of the dropped database. It will only cause the reported property data type to be inconsistent with the property data type of the dropped database, resulting in possible reporting errors and other issues.

* You can view the data types of properties in an existing environment in the product interface, Application Management \- Data Management.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f9def0064024c779db795384ac2502a~tplv-goo7wpa0wc-image.image) </span>


<span id="cf97f7c4"></span>
## **Property** data type correspondence

The following data types are available:


|**Acquisition Data Type \- Name** |**Acquisition data type \- JSON** |**Database type** |**Extra instructions** |**Sample data** |
|---|---|---|---|---|
|**Integer** |number |int64 |Value range: [\-9223372036854775808, 9223372036854775807] |1024 |
|**Floating point number** |number |float64 |8 bytes, maximum precision 16 bits |10.24 |
|**String** |string |string |No more than 1024 characters in length, UTF\-8 encoding |"1024" |
|**Array** |array |list |Supports up to 500 elements, the element data type supports string, and all elements in an array must be of the same type.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the data falls into the database, the elements of the list are deduplicated, such as [5, 5, 5], which becomes [5]; [5, 5, 6], which becomes [5, 6]; [5, 6, 5], which becomes [5, 6].</div><br> |["10", "24"] |
|**Date Time** |string |datetime |Reporting format:<br><br><br>* "yyyy\-MM\-dd HH:mm:ss"<br><br>* "Yyyy\-MM\-dd HH: mm: ss + Offset" (where + Offset is the time zone offset)<br><br>* "Yyyy\-MM\-dd HH: mm: ss. SSS" (where SSS is milliseconds)<br><br>* "Yyyy\-MM\-dd HH: mm: ss. SSS + Offset" (same as before)<br><br><br>Date range: [1970, 2099]<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a datetime report of the form "2020\-07\-07 01:22:33", the default is the time zone of the application level;</div><br><br><br><div data-tips="true" data-tips-type="tip">If you need to specify a timezone, you need to report the "2020\-07\-07 T13:46:08.342 + 08:00" format.</div><br> |"2020\-10\-24 23:47:12"<br><br>"2020\-10\-24 23:47:12+08:00"<br><br>"2020\-10\-24 23:47:12.102"<br><br>"2020\-10\-24 23:47:12.102+08:00" |
|**Version** |string |string |The reporting format of version class data is:<br><br><br>* 2 to 6 segments<br><br>* Period Separation<br><br>* Each paragraph has a maximum of 5 digits.<br><br><br>When the system finds that the format of the value of the reported data matches, it will automatically set the data type to the version type. Version types can be sorted by a numeric collation or filtered by greater than and less than operators.<br><br>The regular expression corresponding to the format requirements is: ^ [0\-9] {1,5} (. [0\-9] {1,5}) {1,5} $<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the version type data is stored in storage, the data format is string, and it will be further processed as the version type data in subsequent query analysis. The filter conditions supported during query are the filter conditions supported by the version type data.</div><br> |"10.2"<br><br>"1.02.4"<br><br>"1.02.4.12345.22345.32345" |
|**Other types** |object/boolean |string |It supports reporting data of object and boolean (bool: yes/no) data types, but it will be converted into a string for storage. |\-\- |


<span id="7bc035a0"></span>
# 2. Application of different data types


* **Different property data types, computable metrics**



|Category |Analysis function |Data type |Calculation method |
|---|---|---|---|
|Event |experimental report |* (all) |total number of times<br><br>total headcount<br><br>per capita |
|Event |experimental report |* (all) |total number of times<br><br>days<br><br>hours |
|Event properties |general purpose |int<br><br>float |Press sum.<br><br>Press... find the average<br><br>press... average person<br><br>Press... for percentiles |
|Event properties |general purpose |Int<br><br>float<br><br>string<br><br>list<br><br>datetime |Press... to deduplicate<br><br>Press... deduplicate with user |



* **Different property data types, operators available as filter criteria**



|Type |Empty |Not empty |= |≠ |greater than |less than |greater than or equal to |less than or equal to |contain |Do not include |regular match |
|---|---|---|---|---|---|---|---|---|---|---|---|
|String |✓ |✓ |✓ |✓ | | | | |✓ |✓ |✓ |
|Integer |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ | | | |
|Floating point |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ | | | |
|Array |✓ |✓ | | | | | | |✓ |✓ | |
|Date Time |✓ |✓ | | | | | | | | | |
|Version |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |



* The string type can be selected as "null" and "not null" to match null or non\-null.

* The date type property has a separate filter (as shown in the table below):



|**Operator name** |**Description** |
|---|---|
|**Fixed range** |The time of the selected property is within a fixed time frame, which can be any day or days from the last 365 days to the next 365 days. |
|**At the current time** |The time of the selected property is between the time the query was initiated and the relative time period set by the user.<br><br>Optional conditions:<br><br><br>1. Past {N} hours {before, within, to {M} days} (value range: 1 < = N < = 365, N must be greater than M, 365 \> = N \> M \> 0)<br><br>2. Future {N} hours {before, within, to {M} days} (value range: 1 < = N < = 365, N must be less than M, 365 \> = N \> M \> 0) |
|**Today and** |The time of the selected property is between the day the query was initiated (natural days) and the relative number of days (natural days) set by the user.<br><br>Optional conditions:<br><br><br>1. Past {N} days {before, within, to {M} days} (value range: 1 < = N < = 365, N must be greater than M, 365 \> = N \> M \> 0)<br><br>2. Future {N} days {before, within, to {M} days} (value range: 1 < = N < = 365, N must be less than M, 365 \> = N \> M \> 0) |
|**In the event** |The time of the selected property is within a period of time relative to the current event. Due to the time of the event, this operator is only used as a filter for the event.<br><br>Optional conditions:<br><br><br>1. Day, Week, and Month: The natural day, week, or month on which the event occurred<br><br>2. Before {N} {days, seconds, minutes, hours, weeks} (the days and weeks at this time are not calculated as natural days or natural weeks, but are calculated from the time when the event occurs)<br><br>3. After {N} {days, seconds, minutes, hours, weeks} (same as before)<br><br><br>The value range of N:<br><br><br>* Day: 1 < = N < = 365 (currently executed according to the sky\-level limit)<br><br>* Second: 1 < = N < = 365<br><br>* Points: 1 < = N < = 365<br><br>* Hours: 1 < = N < = 168<br><br>* Week: 1 < = N < = 52 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Considerations for selecting different data formats:</div>



* <div data-tips="true" data-tips-type="tip">If you need to sum, average, and filter according to the range of intervals, you must use int and float numeric types.</div>


* <div data-tips="true" data-tips-type="tip">The data type that requires a time filter must be defined as the datetime format.</div>



<span id="96c0ead5"></span>
# 3. Restrictions on reporting data

<span id="e19f1723"></span>
## **3.1 General restrictions**


* There is no limit to the total number of reported events for a single application.

* A single application supports no more than 1000 types of meta\-events (different applications do not affect each other, excluding virtual events).

* The recommended number of properties for a single event is within 300, and the maximum is 500 (different events do not affect each other).

* The maximum number of user properties should not exceed 500.

* The number of public properties of a single application custom event does not exceed 100;

* The event name is recommended to be no more than 64 characters and a maximum of 255 characters.

* Event property names and user property names should not exceed 64 characters.

* The length of the property value is recommended to be no more than 255 characters, and the maximum support is 1024 characters in special cases such as URLs;

* Event property names are prohibited from being user_unique_id, ssid, event_id;

* Property names are not allowed to be the same as preset property names; preset property documentation can be viewed [Preset Property Summary](https://docs.byteplus.com/docs/DataTester/120909).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the above limit is exceeded, the excess event and property data may be automatically discarded by the system.</div>


<span id="044ce3e8"></span>
## **3.2 Event time limit**

With data imported by the client side SDK (iOS, Android), the server level by default only receives data within 7 days of the event occurrence time and 24 hours back.

<span id="35ce555c"></span>
## **3.3 Naming restrictions**


1. In the Events table, the same property name is not allowed to have multiple property types, only one property type.

2. In the users table, the same property name is not allowed to have multiple property types, only one property type.

3. The same property name, if it exists in both the events and users tables, can have the same or different data types in both tables.


<span id="3796c109"></span>
## **3.4 Limitations on property length and range**


|Chinese name |Database type |Extra instructions |
|---|---|---|
|Integer |int64 |Value range: [\-9223372036854775808, 9223372036854775807] |
|Floating point number |float64 |8 bytes, maximum precision 16 bits |
|String |string |Maximum support for 1024 characters. |
|Version (string) |version(string) |Format: 1.2 to 6 paragraphs 2. English period separation 3. Maximum 5 digits per paragraph<br><br>Example: 1.1.2 4321 |
|Array |list |Supports up to 500 elements, the element data type supports string, and all elements in an array must be of the same type. |
|Date Time |datetime |Date range: [1900, 2099] |


<span id="3b189017"></span>
# 4. Log structure

The data formats that can be seen after warehousing are as follows:


* **Privatization**


```json
{
    "time": 1606301031,
    "server_time": 1606249381,
    "local_time_ms": 1606301031000,
    "device_id": "6912716898461553676",
    "os": "ios",
    "params": {
        "package": "package",
        "app_version": "1.0.6",
        "device_model": "iphone 6s plus",
        "timezone": "8.0",
        "os_version": "10.3.2",
        "session_depth_range": "5",
        "session_id": "762891435873043",
        "network_carrier": "TELCEL",
        "language": "zh",
        "exit_page": "http://datarangers.com.cn/pages/index/3",
        "product_name": "default_to_b",
        "resolution": "375x667",
        "platform": "ios",
        "loc_country_id": "1814991",
        "app_channel": "线下扫码下载", //offline sacnning QR code
        "device_brand": "苹果", //Apple
        "browser": "chrome",
        "os_name": "ios",
        "loc_province_id": "1280239",
        "session_duration_range": "100-200",
        "client_ip": "118.213.201.135",
        "loc_city_id": "1279540",
        "browser_version": "68.0.3440",
        "network_type": "mobile",
        "duration": 117,
        "session_depth": 5,
        "screen_width": 375,
        "localtime_ms": 1606301031000,
        "screen_height": 667,
        "session_duration": 117,
        "is_login": 1
    }
}
```


<span id="8a1eaa0f"></span>
# 5.FAQ

<span id="b349054a"></span>
### **Q1: The data type transmission at each end is inconsistent. How does the system handle it? How to modify it?** 

Description: For example, the IOS side first passes in the format of the A property as a numerical type, and the Android side passes in the format of the A property as a string type. How does the system handle it at this time, and what will the result be?

**A2:**  The type of an property is determined by the data type imported for the first time. If data of different data types is passed in later, the system will try to convert it. If the conversion is successful, it will be put into storage. If the conversion fails, the property information value is' 0 'into storage, which is equivalent to the loss of property information, but the event is reported normally.

The specific conversion success information is as follows:


|Raw data type |New data types |Is the conversion successful? |Other instructions |
|---|---|---|---|
|int、float、datetime、list |string |Yes | |
|Numeric string, e.g. '1', '0.1' |int、float |Yes |The original data type is string, but the value is the number 123456. |
|float |int |Yes |However, the data after the decimal point will be lost. |
|int |float |Yes | |
|The remaining data types failed to be converted. | | | |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is necessary to avoid this problem on the data verification side. If it occurs, please adjust the data format in the wrong side in time, otherwise it will cause data loss.</div>


<span id="62a03250"></span>
### **Q2: Do you accept the reporting of timestamp string, will it be automatically parsed into datetime format?** 

**A3:**  timestamp is not supported, only date and time formats are supported.

<span id="cac062bd"></span>
### **Q3: Whether datetime accepts data in day\-level format, "yyyy\-MM\-dd"** 

**A4:**  Support. (Reporting format: "yyyy\-MM\-dd")

<span id="cdd4c03a"></span>
### **Q4: How to choose the correct data type when designing event tracking?** 


|Name |Database type |Application scenario |
|---|---|---|
|Integer |int64 |Numerical sums, averages, and other calculations are required, and there will be no decimal cases. For example: age, integer amount. |
|Floating point number |float64 |Numerical sums, averages, and other calculations are required, and decimal cases will occur. For example: discount amount, duration. |
|String |string |Common text class properties, such as page title, button name, product category. ID types that do not need to be calculated, such as content ID, product ID. |
|Array |list |Collections, a property has multiple values, but filtering requires a single filter. Example: An entertainment news item belongs to multiple content tags, {'Hot', 'Entertainment', 'News'} Example: An item belongs to multiple product tags |
|Date Time |datetime |Need to filter by date range |
|Version |string |When you need to sort versions |


<span id="48a456a6"></span>
### **Q5: Why is there a version value for a paragraph? Isn't the version format required to have at least two paragraphs?** 

By default, when the system encounters data that has been cut into at least two segments by "." (e.g. 2.0), it automatically determines that it is a version type. For fields of known version types, we will release this restriction to allow no "." values, such as 2, to be reported. Because in some cases, the version number is only one paragraph. Of course, in this case, you can also choose to report the version number as an int.

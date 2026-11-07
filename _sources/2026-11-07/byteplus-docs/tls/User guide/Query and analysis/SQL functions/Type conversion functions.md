---
title: "Type conversion functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Type-conversion-functions"
---

This topic describes the syntax of type conversion functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="f9689f6b"></span>
## List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>



|Function |Function Syntax |Description |
|---|---|---|
|CAST |CAST(KEY AS type) |Converts the data type of the KEY. |
|TRY_CAST |TRY_CAST(KEY AS type) |Converts the data type of the KEY. |
|TYPEOF |TYPEOF(KEY) |Returns the data type of the Key. |


<span id="2f2b2886"></span>
## CAST function

The CAST function is used to convert the data type of the KEY. When using the CAST function to convert data types, if the data type conversion of a value fails, the system terminates the entire retrieval analysis operation.

<span id="0668b699"></span>
### Function syntax


* syntax format

   ```SQL
   CAST(KEY AS type)
   ```
   

* parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   |type |The SQL data type with optional values of bigint, varchar, double, boolean, timestamp, decimal, array, or map. For example `CAST (JSON_PARSE (KEY) AS array (varchar))`.<br><br>For the mapping between index data types and SQL data types, see [Data type mapping relationship](https://docs.byteplus.com/docs/tls/Type-conversion-functions#676bbbd1). |
   

* Return value description

   The return value data type is the same as the `type` parameter.


<span id="4677b980"></span>
### Function example


* Scenario

   The `child_type` field value is of varchar type, and the `child_type`field value is converted to type map (varchar, varchar) through the CAST function.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The index data type of the <code>child_type</code>field in this example is text. If the index data type is json, the following statement will give an error.   </div>
   

* Log sample

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6dc7efcde3c245e8b5dc00b56a21defd~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT CAST(JSON_PARSE(child_type) AS MAP(varchar, varchar))
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33ce9a100b8f4368b476c1d834b3fb3a~tplv-goo7wpa0wc-image.image) </span>


<span id="ccbd2040"></span>
## TRY_CAST function

TRY_CAST function is used to convert the data type of the KEY. When using the TRY_CAST function to convert a data type, if the data type conversion of a value fails, the system will return NULL and continue processing by skipping the value.

<span id="9589bb6a"></span>
### Function syntax


* syntax format

   ```SQL
   TRY_CAST(KEY AS type)
   ```
   

* parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   |type |SQL data type with optional values of bigint, varchar, double, boolean, timestamp, decimal, array, or map. For example `TRY_CAST (JSON_PARSE (KEY) AS array (varchar))`.<br><br>For the mapping between index data types and SQL data types, see [Data type mapping relationship](https://docs.byteplus.com/docs/tls/Type-conversion-functions#676bbbd1). |
   

* Return value description

   The return value data type is the same as the `type` parameter.


<span id="c4c070ce"></span>
### Function example


* Scenario

   Converts a `ReqTime` field value to a varchar type and returns that data type.

* Query and analysis statement

   ```SQL
   * | SELECT ReqTime,TYPEOF(TRY_CAST(ReqTime AS varchar))
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a2de28bdff94a45a1741fffaf54eda5~tplv-goo7wpa0wc-image.image) </span>


<span id="69748a0a"></span>
## TYPEOF

The TYPEOF function returns the data type of the Key.

<span id="fb84c071"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TYPEOF(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   

* Return value description

   The return value is of the Varchar type.


<span id="32d96a92"></span>
### Example


* Scenario

   Check the data type of the `Method` field.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb3aac5eda6a4031bc0a051402a1e428~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT TYPEOF(Method)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/488d691eb0d04939810513472c1dd672~tplv-goo7wpa0wc-image.image) </span>


<span id="676bbbd1"></span>
## Data type mapping relationship

The correspondence between index data types and SQL data types is shown in the following table:


|< div style = "width: 250px" \> Index data type |< div style = "width: 250px" \> SQL data type |
|---|---|
|long |bigint |
|text |varchar |
|double |double |
|json |varchar |

---
title: "HyperLogLog functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/HyperLogLog-functions"
---

This topic describes the syntax of the type HyperLogLog functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="37283f2e"></span>
## function list

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, the TLS console does not support displaying strings of the HyperLogLog type. You can convert the HyperLogLog type to the binary type through type conversion functions. For the instructions of the type conversion functions, please refer to <a href="https://docs.byteplus.com/docs/tls/Type-conversion-functions#2f2b2886">CAST function</a>, <a href="https://docs.byteplus.com/docs/tls/Type-conversion-functions#ccbd2040">TRY_CAST function</a>.</div>


* <div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>




|Function |Function syntax |Description |
|---|---|---|
|APPROX_SET |APPROX_SET(KEY) |Estimates the number of distinct values in the KEY field. |
|EMPTY_APPROX_SET |EMPTY_APPROX_SET() |Construct a null value of the HyperLogLog data type. |
|MERGE |MERGE(KEY) |Merge multiple HyperLogLogLogs into one HyperLogLog. |


<span id="6d0df886"></span>
## APPROX_SET

APPROX_SET function is used to estimate the number of distinct values in the KEY field. The value of the maximum standard error is 0.01625 by default.

<span id="cbbc6b57"></span>
### Function syntax


* Syntax format

   ```SQL
   APPROX_SET(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   

* Return value description

   The data type of the return value is of the hyperLogLog type.


<span id="f288cab8"></span>
### Example


* Scenario

   Estimate the number of requests by request ID and return the result as HyperLogLog encoding.

* Query and analysis statement

   ```SQL
   * | SELECT CAST(APPROX_SET(ReqID) AS varbinary)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1ec8122e52b48118dd5c5393189488f~tplv-goo7wpa0wc-image.image) </span>


<span id="7a123737"></span>
## EMPTY_APPROX_SET

EMPTY_APPROX_SET function is used to construct a null value of the HyperLogLog data type.

<span id="fa09f7b0"></span>
### Function syntax


* Syntax format

   ```SQL
   EMPTY_APPROX_SET()
   ```
   

* Return value description

   The data type of the return value is of the hyperLogLog type.


<span id="54fea76a"></span>
### Function example


* Scenario

   Constructs a null value of the HyperLogLog type.

* Query and analysis statement

   ```SQL
   * | SELECT CAST(EMPTY_APPROX_SET() AS varbinary) LIMIT 1
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5781942cb9a74bb9a2b3f9e125628107~tplv-goo7wpa0wc-image.image) </span>


<span id="8f3be24c"></span>
## MERGE

The MERGE function is used to merge multiple HyperLogLogLogs into one HyperLogLog.

<span id="1f3740c5"></span>
### Function syntax


* Syntax format

   ```SQL
   MERGE(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the hyperLogLog type. |
   

* return value description

   The data type of the return value is of the hyperLogLog type.


<span id="a00f16b0"></span>
### Function example


* Scenario

   Use the APPROX_SET function to estimate the number of requests per hour (HyperLogLog type), and then use the MERGE function to combine all the request numbers into one HyperLogLog.

* Query and analysis statement

   ```SQL
   * | SELECT CAST(MERGE(UV) AS varbinary) 
   FROM  (
       SELECT
         DATE_TRUNC('hour', __time__) AS time,
         APPROX_SET(ReqID) AS UV
       GROUP BY
         time
       ORDER BY
         time
     )
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36b25430f8904689a2f29e57c17297b4~tplv-goo7wpa0wc-image.image) </span>

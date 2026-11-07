---
title: "Map functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Map-function"
---

This topic describes the syntax of the map functions supported by the Torch Log Service and offers examples on how to use the functions.

<span id="1547e1c2"></span>
## function list

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>



|Function |Function Syntax |Description |
|---|---|---|
|Subscript operator |[x] |Returns the x\-th element in an array. |
|CARDINALITY |CARDINALITY(KEY) |Calculates the number of key\-value pairs in a map. |
|ELEMENT_AT |ELEMENT_AT(map, key) |Obtains the value of the specified key in the map. |
|HISTOGRAM |HISTOGRAM(KEY) |Groups the query and analysis results and returns the results in JSON format. |
|MAP |MAP() |Constructs an empty Map. |
||MAP(KEY1, KEY2) |Maps two arrays to a map. |
|MAP_AGG |MAP_AGG(KEY1, KEY2) |Aggregates data and maps it to a map. Each key corresponds to a unique value. |
|MAP_FILTER |MAP_FILTER(KEY, lambda_expression) |Filters elements in a map based on a lambda expression. |
|MAP_KEYS |MAP_KEYS(KEY) |Extracts all the keys in the map and returns them as an array. |
|MAP_VALUES |MAP_VALUES(KEY) |Extracts the values of all the keys in the map and returns them as an array. |
|MULTIMAP_AGG |MULTIMAP_AGG(KEY1, KEY2) |Aggregates data and maps it to a map. Each key can correspond to multiple values. |


<span id="e931b0ed"></span>
## Subscript operator

The subscript operator is used to return the x\-th element in an array. It is equivalent to the ELEMENT_AT function.

<span id="64dffd70"></span>
### Function **syntax**


* Syntax format

   ```SQL
   [x]
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |Specify the index of the element to be retrieved, starting from 1. The value is of the bigint type. |
   

* Return value description

   The return value can be of any data type.


<span id="7dd920b2"></span>
### Example


* Example1

   * Scenario

      Construct a map `{"lily":19, "lucy":27, "regan":25}` and return the value of `lily`.

   * Query and analysis statement

      ```SQL
      * | SELECT map(array['regan', 'lucy', 'lily'], array[25, 27, 19])['lily']
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e700313f79a4092abe43460c27c6802~tplv-goo7wpa0wc-image.image) </span>

* Example2

   * Scenario

      The value of the `child_type` field is of the varchar type. First, convert the value of the `child_type` field to the map(varchar, varchar) type through the CAST function, and then obtain the key value of `kind` through the subscript operator.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">In this example, the index data type of the <code>child_type</code> field is text. If the index data type is json, null will be returned.      </div>
      

   * Log Sample

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98b69c7c5d2a459fb79ba123f13e445a~tplv-goo7wpa0wc-image.image) </span>

   * Query and analysis statement

      ```SQL
      * | SELECT CAST(JSON_PARSE(child_type) AS MAP(varchar, varchar))['kind']
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a859e0a873d4471aadeb4d7d52e8ce9~tplv-goo7wpa0wc-image.image) </span>


<span id="01b69c95"></span>
## CARDINALITY

The CARDINALITY function is used to calculate the number of key\-value pairs in a map.

<span id="c0d2ba69"></span>
### Function syntax


* Syntax format

   ```SQL
   CARDINALITY(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of map type. |
   

* Return value description

   The return value is of the bigint type.


<span id="c9e50cb9"></span>
### Function example


* Scenario

   The value of the `child_type` field is of the varchar type. Convert the value of the `child_type` field to the map(varchar, varchar) type through the CAST function, and then calculate the number of key\-value pairs in the map by using the CARDINALITY function.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In this example, the index data type of the <code>child_type</code> field is text. If the index data type is json, null will be returned.   </div>
   

* Log Sample

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98b69c7c5d2a459fb79ba123f13e445a~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT CARDINALITY(CAST(JSON_PARSE(child_type) AS MAP(varchar, varchar)))
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4dd668113e2048959696edc8a7975a73~tplv-goo7wpa0wc-image.image) </span>


<span id="87cb6a9e"></span>
## ELEMENT_AT

The ELEMENT_AT function is used to obtain the value of the specified key in the map.

<span id="1dd160a8"></span>
### Function **syntax**


* Syntax format

   ```SQL
   ELEMENT_AT(map, key)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |map |A field or an expression. Specify a value of map type. |
   |key |Specify a certain key name in the map, and the ELEMENT_AT function will extract the value of that key. |
   

* Return value description

   The return value can be of any data type.


<span id="1c77f8bc"></span>
### Example


* Scenario

   Construct a map `{"lily":19, "lucy":27, "regan":25}` and return the value of `lily`.

* Query and analysis statement

   ```SQL
   * | SELECT ELEMENT_AT(map(array['regan', 'lucy', 'lily'], array[25, 27, 19]),'lily')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9fdbacc5d1d642149ff106701e3978bd~tplv-goo7wpa0wc-image.image) </span>


<span id="da671c3b"></span>
## HISTOGRAM

The HISTOGRAM function is used to group the query and analysis results and return the results in the JSON format. This function is equivalent to `* | SELECT COUNT (*) GROUP BY key`.

<span id="dc50cc8c"></span>
### Function syntax


* Syntax format

   ```SQL
   HISTOGRAM(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of any data type. |
   

* Return value description

   The return value is of the map type.


<span id="21552c1a"></span>
### Function example


* Scenario

   Use the Histogram function to get the number of different response states for all requests.

* Query and analysis statement

   ```SQL
   * | SELECT histogram(status) AS status_count
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/337f3ebb07cb4750b17f9cdb1055a178~tplv-goo7wpa0wc-image.image) </span>


<span id="97d21e39"></span>
## MAP

The MAP function is used to construct an empty Map or to map two arrays into a Map.

<span id="c6333a36"></span>
### Function syntax


* Syntax format

   * Returns an empty Map.

      ```SQL
       MAP()
      ```
      

   * Map two arrays to a map.

      ```SQL
      MAP(KEY1,KEY2) 
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of any data type. |
   

* Return value description

   The return value is of the map type.


<span id="e9379b0d"></span>
### Function example


* Example 1

   * Scenario

      Use the MAP function to map the arrays representing names and ages `['regan', 'lucy', 'lily']`, `[25, 27, 19]` into a map, which corresponds names and ages one by one.

   * Query and analysis statement

      ```SQL
      * | SELECT map(array['regan', 'lucy', 'lily'], array[25, 27, 19])
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fafebe6ad21476283b70ca78a051f4f~tplv-goo7wpa0wc-image.image) </span>

* Example 2

   * Scenario

      Construct an empty map.

   * Query and analysis statement

      ```Plain
      *| SELECT MAP()
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6182d3fa27b4461dbf37fdd9fb27f04c~tplv-goo7wpa0wc-image.image) </span>


<span id="860d2f38"></span>
## MAP_AGG

MAP_AGG function is used to aggregate data and map it to a map. Each key corresponds to a unique value.

<span id="b60d67ed"></span>
### Function syntax


* Syntax format

   ```SQL
   MAP_AGG(KEY1, KEY2)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of any data type.<br><br>KEY1 is the key in the map, and KEY2 is the value in the map. When multiple values of KEY2 exist, a random value is extracted as the value. |
   

* Return value description

   The return value is of the map type.


<span id="fd8d7164"></span>
### Function example


* Scenario

   Query the duration of requests using `ReqID` and `ReqTime`, and map them to a Map using the MAP_AGG function. `ReqID` is the key in the Map, and `ReqTime` is the value in the Map.

* Query and analysis statement

   ```SQL
   * | SELECT MAP_AGG(ReqID, ReqTime) FROM (SELECT ReqID, ReqTime LIMIT 5)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66e2ce82f77d41499e1c6a1303223e99~tplv-goo7wpa0wc-image.image) </span>


<span id="213d4842"></span>
## MAP_FILTER

The MAP_FILTER function filters elements in a map based on a lambda expression.

Function syntax


* Syntax format

   ```SQL
   MAP_FILTER(KEY, lambda_expression)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of map type. |
   |lambda_expression |Lambda expressions. |
   

* Return value description

   The return value is of the map type.


<span id="fefcf99e"></span>
### Function example


* Scenario

   Maps two arrays into a new Map, with non\-null keys in the Map. Where `(k, v) - > v is not null`is a lambda expression.

* Query and analysis statement

   ```SQL
   * | SELECT MAP_FILTER(MAP(array['regan', 'lucy', 'lily'], array[21, NULL, 18]), (k, v) -> v is not null)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e45092af47c3489fa997c42669445144~tplv-goo7wpa0wc-image.image) </span>


<span id="963125d5"></span>
## MAP_KEYS

MAP_KEYS function is used to extract all the keys in the Map and return them as an array.

<span id="1a47ac7d"></span>
### Function syntax


* Syntax format

   ```SQL
   MAP_KEYS(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of map type. |
   

* Return value description

   The return value is of the array type .


<span id="af2520df"></span>
### Function example


* Scenario

   Use the MAP_KEYS function to extract all the keys in the `result`field value.

* Log sample

   ```SQL
   result: {
   type:"pattern-discovery"
   stage:"pattern-clustering"
   progress:"100"
   complete:"false"
   }
   ```
   

* Query and analysis statement

   ```SQL
   * | SELECT MAP_KEYS(TRY_CAST(JSON_PARSE(result) AS MAP(varchar, varchar)))
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17128c53888f4291a6fa6e903f022925~tplv-goo7wpa0wc-image.image) </span>


<span id="67b63ab6"></span>
## MAP_VALUES

MAP_VALUES function is used to extract the values of all keys in the Map and return them as an array.

<span id="2072bb92"></span>
### Function syntax


* Syntax format

   ```SQL
   MAP_VALUES(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of map type. |
   

* Return value description

   The return value is of the array type .


<span id="807d337c"></span>
### Function example


* Scenario

   Use the MAP_VALUES function to extract all the values in the `result`field value.

* Log sample

   ```SQL
   result: {
   type:"pattern-discovery"
   stage:"pattern-clustering"
   progress:"100"
   complete:"false"
   }
   ```
   

* Query and analysis statement

   ```SQL
   * | SELECT MAP_VALUES(TRY_CAST(JSON_PARSE(result) AS MAP(varchar, varchar)))
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4a31b1c6fd4442e8361c0eec38e8b97~tplv-goo7wpa0wc-image.image) </span>


<span id="677a944b"></span>
## MULTIMAP_AGG

MULTIMAP_AGG function is used to aggregate data and map it to a Map.

<span id="75290aa2"></span>
### Function syntax


* Syntax format

   ```SQL
   MULTIMAP_AGG(KEY1, KEY2)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of any data type.<br><br>KEY1 is the key in the map, KEY2 is the value in the map, and the value is in array format. When multiple values exist for KEY2, extract all the values as keys. |
   

* Return value description

   The return value is of the map type.


<span id="337491c3"></span>
### Function example


* Scenario

   Extract the values of the `Action`and `ReqTime`fields and map them to a map. `The Action`field value is the key in the map, the `ReqTime`field value is the value in the map, and the value is in array format.

* Query and analysis statement

   ```SQL
   * | SELECT MULTIMAP_AGG(Action, ReqTime) FROM(SELECT Action, ReqTime LIMIT 5)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e56798b27250419babd796772dca301a~tplv-goo7wpa0wc-image.image) </span>

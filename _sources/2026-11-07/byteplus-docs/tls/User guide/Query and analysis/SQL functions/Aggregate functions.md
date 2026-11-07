---
title: "Aggregate functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Aggregate-functions-2"
---

This topic describes the syntax of aggregate functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="fd76176c"></span>
## List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>



|Function |Function syntax |Description |
|---|---|---|
|ARBITRARY |ARBITRARY(KEY) |Returns an arbitrary non\-empty value in a group of values. |
|AVG |AVG(KEY) |Returns the average of a group of values. |
|BITWISE_AND_AGG |BITWISE_AND_AGG(KEY) |Returns the result of the bitwise AND operation on the values. |
|BITWISE_OR_AGG |BITWISE_OR_AGG(KEY) |Returns the result of the bitwise OR operation on the values. |
|BOOL_AND |BOOL_AND(boolean_expression) |Checks whether all values meet the specified condition. |
|BOOL_OR |BOOL_OR(boolean_expression) |Checks whether a value meets the specified condition exists. |
|CHECKSUM |CHECKSUM(KEY) |Returns the checksum of a group of values. |
|COUNT |COUNT(\*) |Returns the number of values. |
||COUNT(1) |Returns the number of values. |
||COUNT(KEY) |Returns the number of non\-null values. |
|COUNT_IF |COUNT_IF (Boolean Expression) |Returns the number of values that meet the specified condition. |
|EVERY |EVERY(boolean_expression) |Determines whether all values satisfy the specified Boolean expression. |
|GEOMETRIC_MEAN |GEOMETRIC_MEAN(KEY) |Calculates the geometric mean of the values. |
|KURTOSIS |KURTOSIS(KEY) |Calculates the kurtosis of the values. |
|MAP_UNION |MAP_UNION(KEY) |Merges multiple sets of map data. |
|MAX |MAX(KEY) |Returns the maximum value in a group of values. |
|MAX_BY |MAX_BY(KEY1, KEY2) |Queries the KEY1 values associated with the maximum value of KEY2. |
||MAX_BY(KEY1, KEY2, n) |Queries the KEY1 values associated with the top N values of KEY2, returning the results in array form. |
|MIN |MIN(KEY) |Returns the minimum value in a group of values. |
|SUM |SUM(KEY) |Returns the sum of a group of values. |


<span id="ARBITRARY"></span>
## ARBITRARY

The ARBITRARY function returns an arbitrary non\-empty value in a group of values.

<span id="c62360db"></span>
### Function syntax


* Syntax format

   ```SQL
   ARBITRARY(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   

* Return value description

   The data type of the return value is the same as the type of the parameter value.


<span id="db98c046"></span>
### Example


* Scenario

   The function is used to get an arbitrary non\-empty value of the `ReqTime` field.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31e87b253a004dbf92eb9726597b5248~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT ARBITRARY(ReqTime) AS ReqTime
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/047ec9881bc44922b4158584e1cb1928~tplv-goo7wpa0wc-image.image) </span>


<span id="e417c10e"></span>
## AVG

The AVG function returns the average of a group of values.

<span id="bc808a22"></span>
### Function syntax


* Syntax format

   ```SQL
   AVG(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double, bigint, decimal, or real data type. |
   

* Return value description

   The return value is of the double type.


<span id="f84516bc"></span>
### Example


* Scenario

   The function is used to calculate average request duration.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b1b75beb5214918b1dde7f91cf6d3ff~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT AVG(ReqTime)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9fce0f1068884ca7b3d6bd91e34c2f68~tplv-goo7wpa0wc-image.image) </span>


<span id="80610581"></span>
## BITWISE_AND_AGG

BITWISE_AND_AGG function returns the result of the bitwise AND operation on the values.

<span id="4b0e32d7"></span>
### Function syntax


* Syntax format

   ```SQL
   BITWISE_AND_AGG(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify the value of bigint data type. |
   

* Return value description

   The return value is of the bigint type in binary representation.


<span id="293d0660"></span>
### Example


* Scenario

   The function is used to return the result of the bitwise AND operation on the values of the `status` field.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fdb60ee007c4bb3b48813ba24c339b3~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT BITWISE_AND_AGG(status)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b8d000f4f104560a8f31b6fb9563e0e~tplv-goo7wpa0wc-image.image) </span>


<span id="f57f7606"></span>
## BITWISE_OR_AGG

BITWISE_OR_AGG function returns the result of the bitwise OR operation on the values.

<span id="aca77157"></span>
### Function syntax


* Syntax format

   ```SQL
   BITWISE_OR_AGG(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify the value of bigint data type. |
   

* Return value description

   The return value is of the bigint type in binary representation.


<span id="b30d6ee7"></span>
### Example


* Scenario

   The function is used to return the result of the bitwise OR operation on the values of the `status` field.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fdb60ee007c4bb3b48813ba24c339b3~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT BITWISE_OR_AGG(status)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27d8e1592e0e46f285a772f13cd7137e~tplv-goo7wpa0wc-image.image) </span>


<span id="8bfa2a4e"></span>
## BOOL_AND

BOOL_AND function checks whether all values meet the specified condition.

<span id="f6f93169"></span>
### Function syntax


* Syntax format

   ```SQL
   BOOL_AND(boolean_expression)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |boolean_expression |A boolean expression. |
   

* Return value description

   The return value is of the boolean type.


<span id="86af801e"></span>
### Example


* Scenario

   The function is used to check the values of the `status` field are 200. If not, the function returns false.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/636ffa0f1e484415876b542172c01896~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT BOOL_AND(status = 200)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3048592f5f944524b088861f123863a3~tplv-goo7wpa0wc-image.image) </span>


<span id="94fe8fb4"></span>
## BOOL_OR

BOOL_OR function checks whether a value meets the specified condition exists.

<span id="2c2ef6db"></span>
### Function syntax


* Syntax format

   ```SQL
   BOOL_OR(boolean_expression)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |boolean_expression |A boolean expression. |
   

* Return value description

   The return value is of the boolean type.


<span id="116b6ad1"></span>
### Example


* Scenario

   The function is used to check whether the value of the `RespSize` field is less than 20. If yes, the function returns true.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1657a9931de64eb186d46aa76c595df5~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT BOOL_OR(RespSize < 20)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af66ab0b990f487f828ffb18d5f479f9~tplv-goo7wpa0wc-image.image) </span>


<span id="36d179e2"></span>
## **CHECKSUM**

The CHECKSUM function returns the checksum of a group of values.

<span id="7e1ac3d1"></span>
### Function syntax


* Syntax format

   ```SQL
   CHECKSUM(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   

* Return value description

   Data type: String. The result is base64\-encoded.


<span id="5b68bed3"></span>
### Example


* Scenario

   The function is used to calculate the checksum of the values of the `url_test` field.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e498ec4291e2480c90b6bc1cab615160~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT CHECKSUM(url_test) AS request_method
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3910a22253e7433ea396d64dbf4832da~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="fbd52385"></span>
## COUNT

The COUNT function returns the number of values.

<span id="01963dd7"></span>
### Function syntax


* Syntax format

   * The following format returns the number of a group of values:

      ```SQL
      COUNT(*)
      ```
      

   * The following format returns the number of a group of values:

      ```SQL
      COUNT(1)
      ```
      

   * The following format returns the number of non\-null values in a group of values:

      ```SQL
      COUNT(KEY)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   

* Return value description

   The return value is of the integer data type.


<span id="ce32e044"></span>
### Example


* Scenario

   The function is used to calculate the number of requests whose request duration is greater than 40 milliseconds.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/058177fdbd254d3183c4cb3841b07946~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT COUNT(ReqTime) WHERE ReqTime > 40.0
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5c1f94191024308adc8fd0b5ddfa71b~tplv-goo7wpa0wc-image.image) </span>


<span id="ddffcfc7"></span>
## COUNT_IF

The COUNT_IF function returns the number of values that meet the specified condition.

<span id="b030d647"></span>
### Function syntax


* Syntax format

   ```SQL
   COUNT_IF (Boolean Expression)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |Boolean Expression |The value is of the boolean type. |
   

* Return value description

   The return value is of the integer data type.


<span id="820437cb"></span>
### Example


* Scenario

   The function is used to count the number of logs in which the values of the `url_test` field end with `name=xxx`.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6827262bddef46d1a53a0e990d879bc3~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT COUNT_IF(url_test LIKE '%name=xxx') AS count
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70d6eedd8b5347f9a37bb38ee3830f49~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="9c070be8"></span>
## EVERY

The EVERY function is used to determine whether all values satisfy the specified Boolean expression, which is equivalent to [BOOL_AND](https://docs.byteplus.com/docs/tls/Aggregate-functions-2#8bfa2a4e).

<span id="d831fa87"></span>
### Function syntax


* Syntax format

   ```SQL
   EVERY(boolean_expression)
   ```
   

* Parameter description

   
   |parameter |explain |
   |---|---|
   |boolean_expression |Boolean expression. |
   

* Return value description

   The return value is of the boolean type.


<span id="46d260ab"></span>
### Example


* Scenario

   Determine whether the `status`field values are all 200. If not, return false.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/636ffa0f1e484415876b542172c01896~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT EVERY(status = 200)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d013f2966beb4c77881a99d47f3c0af1~tplv-goo7wpa0wc-image.image) </span>


<span id="9e65a019"></span>
## GEOMETRIC_MEAN

GEOMETRIC_MEAN function calculates the geometric mean of the values.

<span id="e114c9f9"></span>
### Function syntax


* Syntax format

   ```SQL
   GEOMETRIC_MEAN(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double, bigint or real data type. |
   

* Return value description

   The return value is of the double type.


<span id="d89c5960"></span>
### Example


* Scenario

   Calculate the geometric mean of the values of the `status` field.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/636ffa0f1e484415876b542172c01896~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT GEOMETRIC_MEAN(status)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47aaea749ae84141818aadd2e4ffdea8~tplv-goo7wpa0wc-image.image) </span>


<span id="b669284d"></span>
## KURTOSIS

KURTOSIS function calculates the kurtosis of the values.

<span id="44f42efd"></span>
### Function syntax


* Syntax format

   ```SQL
   KURTOSIS(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double or bigint data type. |
   

* Return value description

   The return value is of the double type.


<span id="94e13c5b"></span>
### Example


* Scenario

   Calculate the kurtosis of the values of the `status` field.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/636ffa0f1e484415876b542172c01896~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT KURTOSIS(status)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8210225c5c8d4fa190390c2e1a43bb23~tplv-goo7wpa0wc-image.image) </span>


<span id="e052b90f"></span>
## MAP_UNION

The MAP_UNION function is used to merge multiple sets of map data. If there are duplicate keys in multiple groups of maps, only any value of that key is returned.

<span id="1f1947e6"></span>
### Function syntax


* Syntax format

   ```SQL
   MAP_UNION(KEY)
   ```
   

* Parameter description

   
   |parameter |explain |
   |---|---|
   |KEY |A field or an expression. Specify a value of the map type. |
   

* Return value description

   The return value is of the map type.


<span id="b90e8463"></span>
### Example


* scene

   Merges the values of the `result`field and returns one of the merged values at random.

* Log sample

   ```SQL
   result: {
   type:"pattern-discovery"
   stage:"pattern-clustering"
   progress:"100"
   complete:"false"
   }
   ```
   

* Search and parse statements

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The index data type of the <code>result</code>field in this example needs to be text. If the index data type is json, executing the following statement will give an error.   </div>
   

   ```SQL
   * | SELECT
     MAP_UNION(
       TRY_CAST(JSON_PARSE(result) AS map(varchar, varchar))
     )
   ```
   

* Search and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7db957f0eb764e97818106e785cc8a76~tplv-goo7wpa0wc-image.image) </span>


<span id="8d35587f"></span>
## MAX

The MAX function returns the maximum value in a group of values.

<span id="8d649f9c"></span>
### Function syntax


* Syntax format

   ```SQL
   MAX(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   

* Return value description

   The data type of the return value is the same as the type of the parameter value.


<span id="3f4a6480"></span>
### Example


* Scenario

   The function is used to query the longest request duration.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b1b75beb5214918b1dde7f91cf6d3ff~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT MAX(ReqTime) AS max_reqtime
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94882aeb06724d25b629cbd0e2b3eea3~tplv-goo7wpa0wc-image.image) </span>


<span id="c2092292"></span>
## MAX_BY

The MAX_BY function is used to query the KEY1 values associated with the maximum or top N values of KEY2.

<span id="43f94843"></span>
### Function syntax


* Syntax format

   * Query the KEY1 values associated with the maximum value of KEY2.

      ```SQL
      MAX_BY(KEY1, KEY2)
      ```
      

   * Query the KEY1 values associated with the top N values of KEY2, returning the results in array form.

      ```SQL
      MAX_BY(KEY1, KEY2, n)
      ```
      

* Parameter description

   
   |parameter |explain |
   |---|---|
   |KEY1 |A field or an expression. The value can be any data type. |
   |KEY2 |A field or an expression. The value can be any data type. |
   |n |An integer greater than 0, used to specify the top N values of `KEY2` . |
   

* Return value description

   The return value is the same as the data type of the parameter value.


<span id="8ebd6f6d"></span>
### Example


* Example 1

   * Scenario

      Query the maximum request time and the request ID corresponding to that time.

   * Query and analysis statements

      ```SQL
      * | SELECT MAX(ReqTime) AS ReqTime, MAX_BY(ReqID, ReqTime) AS ReqID
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e389eaa3127645e89b28bd39346abeb6~tplv-goo7wpa0wc-image.image) </span>

* Example 2

   * scene

      Query the request ID corresponding to the TOP 10 request time.

   * Query and analysis statements

      ```SQL
      * | SELECT MAX_BY(ReqID, ReqTime, 10) AS ReqID
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0004c7a6b556486cb8127dae6bc14bae~tplv-goo7wpa0wc-image.image) </span>


<span id="0c553082"></span>
## MIN

The MIN function returns the minimum value in a group of values.

<span id="98aac18a"></span>
### Function syntax


* Syntax format

   ```SQL
   MIN(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   

* Return value description

   The data type of the return value is the same as the type of the parameter value.


<span id="9eed4235"></span>
### Example


* Scenario

   The function is used to query the shortest request duration.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b1b75beb5214918b1dde7f91cf6d3ff~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT MIN(ReqTime) AS min_reqtime
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df17ea3b1dec46f4b2832204090b95da~tplv-goo7wpa0wc-image.image) </span>


<span id="c2cd4884"></span>
## SUM

The SUM function returns the sum of a group of values.

<span id="dad80536"></span>
### Function syntax


* Syntax format

   ```SQL
   SUM(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double, bigint, decimal, or real data type. |
   

* Return value description

   The data type of the return value is the same as the type of the parameter value.


<span id="81f67c07"></span>
### Example


* Scenario

   The function is used to calculate the sum of request duration.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b1b75beb5214918b1dde7f91cf6d3ff~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT SUM(ReqTime) AS total
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e5f583e3fe243fc9f1551096c52f53f~tplv-goo7wpa0wc-image.image) </span>

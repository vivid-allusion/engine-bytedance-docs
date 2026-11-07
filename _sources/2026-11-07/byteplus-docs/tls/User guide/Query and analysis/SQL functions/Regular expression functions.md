---
title: "Regular expression functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Regular-expression-functions-2"
---

This topic describes the syntax of regular expression functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="68448967"></span>
## List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>



|Function |Syntax |Description |
|---|---|---|
|REGEXP_EXTRACT_ALL |REGEXP_EXTRACT_ALL(KEY, regular_expression) |Extracts the substrings matched by a sepcified regular expression and returns arrays of all matched substrings. |
||REGEXP_EXTRACT_ALL(KEY, regular_expression, n) |Extracts the substrings matched by the regular expression in a specified string and returns an array of substrings that match the nth capturing group. |
|REGEXP_EXTRACT |REGEXP_EXTRACT(KEY, regular_expression) |Extracts the first substring matched by the regular expression in a specified string and returns the substring. |
||REGEXP_EXTRACT(KEY, regular_expression, n) |Extracts the substrings matched by the regular expression in a specified string and returns the first substring that matches the nth capturing group. |
|REGEXP_LIKE |REGEXP_LIKE(KEY, regular_expression) |Verifies whether the value of a field matches a specified regular expression. |
|REGEXP_REPLACE |REGEXP_REPLACE(KEY, regular_expression) |Removes the substrings matched by the regular expression in a specified string and returns the substrings that remain. |
||REGEXP_REPLACE(KEY, regular_expression, replace_string) |Replaces the substrings matched by the regular expression in a specified string and returns the result string. |
|REGEXP_SPLIT |REGEXP_SPLIT(KEY, regular_expression) |Split a string into an array of substrings based on a regular expression pattern. |


<span id="REGEXP_EXTRACT_ALL"></span>
## REGEXP_EXTRACT_ALL

The REGEXP_EXTRACT_ALL function extracts the substrings that match a specified regular expression.

<span id="bd230baa"></span>
### Function **syntax**


* Syntax format

   * The following format extracts the substrings matched by a specified regular expression and returns arrays of all matched substrings:

      ```SQL
      REGEXP_EXTRACT_ALL(KEY, regular_expression)
      ```
      

   * The following format extracts the substrings matched by a specified regular expression and returns an array of substrings that match the nth capturing group:

      ```SQL
      REGEXP_EXTRACT_ALL(KEY, regular_expression, n)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   |regular_expression |A regular expression that contains capturing groups. For example, `(\d)(\d)(\d)` indicates three capturing groups. |
   |n |The nth capturing group. Here, n is an integer that starts from 1. |
   

* Return value description

   The return value is of the Array type.


<span id="8d26c676"></span>
### Example


* Example 1

   * Scenario

      The statement extracts all digits from the values of the `url_test` field.

   * Sample log

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1203389c42604ab48d57b937dc85b1b6~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

   * Query and analysis statement

      ```SQL
      *| SELECT REGEXP_EXTRACT_ALL(url_test, '\d+')
      ```
      

   * Query and analysis results

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c9b0fa4b8f5490d85bec0dda3678de9~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

* Example 2

   * Scenario

      The statement extracts `age` from the values of the `url_test` field and calculates the number of logs with `age`.

   * Query and analysis statement

      ```SQL
      *| SELECT REGEXP_EXTRACT_ALL(url_test, '(age)',1) AS age, COUNT(*) AS count GROUP BY age
      ```
      

   * Sample log

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b867822066e74af4b3d14666ca5e1133~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4c22850a16647d69066282f8e2ca33d~tplv-goo7wpa0wc-image.image) </span>


<span id="c363061a"></span>
## REGEXP_EXTRACT

The REGEXP_EXTRACT function extracts the first substring that matches a specified regular expression.

<span id="9113db97"></span>
### Function **syntax**


* Syntax format

   * The following format extracts the first substring matched by a specified regular expression:

      ```SQL
      REGEXP_EXTRACT(KEY, regular_expression)
      ```
      

   * The following format extracts the substrings matched by a specified regular expression and returns the first substring that matches the nth capturing group:

      ```SQL
      REGEXP_EXTRACT(KEY, regular_expression, n)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   |regular_expression |A regular expression that contains capturing groups. For example, `(\d)(\d)(\d)` indicates three capturing groups. |
   |n |The nth capturing group. Here, n is an integer that starts from 1. |
   

* Return value description

   The return value is of the Varchar type.


<span id="53b4f859"></span>
### Example


* Example 1

   * Scenario

      The statement extracts the first digits from the values of the `url_test` field.

   * Sample log

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/287fdb47657b4acc8e93b16f6ea5b1c7~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

   * Query and analysis statement

      ```SQL
      *|SELECT REGEXP_EXTRACT(url_test, '\d+')
      ```
      

   * Query and analysis results

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab18b273ec734d3491a48c3fbbf558c2~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

* Example 2

   * Scenario

      The statement extracts the first `age` information from the values of the `url_test` field.

   * Sample log

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53b1fc2ca1b64e6eb54ba98eebbe02f2~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

   * Query and analysis statement

      ```SQL
      * | SELECT REGEXP_EXTRACT(url_test, '.*(age.*)&', 1) AS age, count(*) AS count GROUP BY age
      ```
      

   * Query and analysis results

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3af95cccfda14b3bb0262969473ff7db~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

* Example 3

   * Scenario

      The statement extracts colons ( : ) and digits from the values of the `url_test` field.

   * Sample log

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e97bb1441d24c25921c7137ad2f03a7~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

   * Query and analysis statement

      ```SQL
      * | SELECT REGEXP_EXTRACT(url_test, ':\d+')     
      ```
      

   * Query and analysis results

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d95df41a03b2444180f3815c28ff7c44~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      


<span id="9c2092a0"></span>
## REGEXP_LIKE

The REGEXP_LIKE function verifies whether the values of a field match a specified regular expression.

<span id="6173ded1"></span>
### Function **syntax**


* Syntax format

   ```SQL
   REGEXP_LIKE(KEY, regular_expression)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   |regular_expression |A regular expression. |
   

* Return value description

   The return value is of the Boolean type.


<span id="bd45401a"></span>
### Example


* Scenario

   The statement verifies whether the values of the url_test field contain digits.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aeae5e52088e42c8b244f539e2f437d7~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   *| SELECT REGEXP_LIKE(url_test, '\d+')
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb45ad02c8da4227863ea78026c75cd1~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="00bd4e71"></span>
## REGEXP_REPLACE

The REGEXP_REPLACE function deletes or replaces the substrings that match a specified string.

<span id="559702ce"></span>
### Function **syntax**


* Syntax format

   * Delete the substrings that match the specified regular expression and return the substrings that have not been deleted.

      ```SQL
      REGEXP_REPLACE(KEY, regular_expression)
      ```
      

   * Replace the substrings that match the specified regular expression and return the replaced substrings.

      ```SQL
      REGEXP_REPLACE(KEY, regular_expression, replace_string)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   |regular_expression |A regular expression. |
   |replace_string |The substring for replacement. |
   

* Return value description

   The return value is of the Varchar type.


<span id="f308831f"></span>
### Example


* Scenario

   Delete all the numbers in the value of the `Query` field.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0819231b7fe480f9bff7b574602fb03~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   *| SELECT REGEXP_REPLACE(Query, '\d+')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e432a318aa94d4aaddcfb0c51d8ccdd~tplv-goo7wpa0wc-image.image) </span>


<span id="18328a17"></span>
## REGEXP_SPLIT

REGEXP_SPLIT function is used to split a string into an array of substrings based on a regular expression pattern.

<span id="5c957b4f"></span>
### Function **syntax**


* Syntax format

   ```SQL
   REGEXP_SPLIT(KEY, regular_expression)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   |regular_expression |A regular expression. |
   

* Return value description

   The return value is of the Array type.


<span id="58d65d70"></span>
### Example


* Scenario

   Split the values in the `URL` field using an underscore (`_`) as the delimiter.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0ca141905474896b9cbaa99c87612ad~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   *| SELECT REGEXP_SPLIT(Query, '_')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0d74ad2762740d38545cf93df785f41~tplv-goo7wpa0wc-image.image) </span>

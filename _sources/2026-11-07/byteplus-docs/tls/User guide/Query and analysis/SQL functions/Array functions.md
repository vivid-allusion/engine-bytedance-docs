---
title: "Array functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Array_functions"
---

This topic describes the syntax of array functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="6f05e20e"></span>
## List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>



|Function |Function Syntax |Description |
|---|---|---|
|Subscript operator |[x] |This function returns the x\-th element in an array. |
|ARRAY_AGG |ARRAY_AGG(KEY) |This function returns an array aggregated from all values of a field or expression. |
|ARRAY_DISTINCT |ARRAY_DISTINCT(KEY) |This function removes duplicate elements from an array. |
|ARRAY_EXCEPT |ARRAY_EXCEPT(KEY1, KEY2) |This function removes duplicate elements from two arrays and returns the first array. |
|ARRAY_INTERSECT |ARRAY_INTERSECT(KEY1, KEY2) |This function returns the intersection of two arrays. |
|ARRAY_JOIN |ARRAY_JOIN(KEY, delimiter) |This function concatenates the elements of an array into a string using a specified delimiter. If the array contains a null element, the null element is ignored. |
|ARRAY_JOIN(KEY, delimiter, null_replacement) |ARRAY_JOIN(KEY, delimiter, null_replacement) |This function concatenates the elements of an array into a string using a specified delimiter. If the array contains a null element, the null element is replaced with the specified string. |
|ARRAY_MAX |ARRAY_MAX(KEY) |This function returns the maximum value in an array. |
|ARRAY_MIN |ARRAY_MIN(KEY) |This function returns the minimum value in an array. |
|ARRAY_POSITION |ARRAY_POSITION(KEY, element) |This function returns the position of a specified element, with an element index starting at 1. |
|ARRAY_REMOVE |ARRAY_REMOVE(KEY, element) |This function removes a specified element from an array. |
|ARRAY_SORT |ARRAY_SORT(KEY) |This function sorts an array of elements in ascending order. If the array contains a null element, the null element is placed at the end. |
|ARRAY_TRANSPOSE |ARRAY_TRANSPOSE(KEY) |This function transposes the array, extracting the same index elements in the two\-dimensional array to form a new two\-dimensional array. |
|ARRAY_UNION |ARRAY_UNION(KEY1, KEY2) |This function returns the union of two arrays. |
|CARDINALITY |CARDINALITY(KEY) |This function returns the number of elements in an array. |
|CONCAT |CONCAT(KEY1, KEY2…) |This function concatenates multiple arrays into one array. |
|CONTAINS |CONTAINS(KEY, element) |This function verifies whether an array contains a specified element. |
|ELEMENT_AT |ELEMENT_AT(KEY, index) |This function gets the element at the specified position in the array. |
|FLATTEN |FLATTEN(KEY) |This function converts a two\-dimensional array to a one\-dimensional array. |
|FILTER |FILTER(KEY, lambda_expression) |This function filters elements in an array based on a lambda expression. |
|REDUCE |REDUCE(KEY, lambda_expression) |This function accumulates the individual elements of the array as defined in the lambda expression, and then returns the result of the evaluation. |
|REVERSE |REVERSE(KEY) |This function sorts an array of elements in reverse order. |
|SEQUENCE |SEQUENCE(x, y) |This function generates an array within the specified range, consisting of a continuous and increasing set of values within the range of starting and ending values. Where the increment interval is the default value of 1. |
||SEQUENCE(x, y, step) |This function generates an array within the specified range, consisting of a continuous and increasing set of values within the range of starting and ending values. Where the increment interval is a custom value. |
|SHUFFLE |SHUFFLE(KEY) |This function randomly rearranges the array elements. |
|SLICE |SLICE(KEY, start, length) |This function gets a subset of the array. |
|TRANSFORM |TRANSFORM(KEY, lambda_expression) |This function applies a lambda expression to each element of the array. |
|ZIP |ZIP(KEY1, KEY2...) |This function combines multiple arrays into a two\-dimensional array according to the corresponding positions, and the elements in each array with the same subscript form a new number. |


<span id="265f2ef0"></span>
## Subscript operator

The subscript operator is used to return the x\-th element in an array. It is equivalent to the ELEMENT_AT function.

<span id="d714da47"></span>
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

   The return value is consistent with the data type of the specified element.


<span id="82cbe1c3"></span>
### Example


* Scenario

   Return the first element in the array [5.0, 20.0, 39.0, 1, 7].

* Query and analysis statement

   ```SQL
   * | SELECT array[5.0,20.0,39.0,1,7][1]
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f9157349eb048898cabe474b86e9cc0~tplv-goo7wpa0wc-image.image) </span>


<span id="2c9df0b2"></span>
## ARRAY_AGG

The ARRAY_AGG function aggregates the values of a field and returns the values as an array.

<span id="39751251"></span>
### Function **syntax**


* Syntax format

   ```SQL
   ARRAY_AGG (KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   

* Return value description

   The return value is of the array type.


<span id="8968913f"></span>
### Example


* Scenario

   The statement aggregates the values of the `test_double` field and returns the values as an array.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5be51ee99eed4824977d5efeee009e8f~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT ARRAY_AGG(test_double) AS array
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b58e1f8ac3d4f4a9597fdd8e739ffa9~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="52e7d64b"></span>
## ARRAY_DISTINCT

The ARRAY_DISTINCT function removes duplicate elements from an array.

<span id="7da4d079"></span>
### Function **syntax**


* Syntax format

   ```SQL
   ARRAY_DISTINCT(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   

* Return value description

   The return value is of the array type.


<span id="de81e264"></span>
### Example


* Scenario

   The statement removes duplicate elements from the value of the `test_text` field.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db36a7c96a244f2daf8df1b1c1998a8f~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   *| SELECT ARRAY_DISTINCT(cast(JSON_PARSE(test_text) as array(bigint)))
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c2cfa00187343d39937131745523e29~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="101a718d"></span>
## ARRAY_EXCEPT

The ARRAY_EXCEPT function removes duplicate elements from two arrays, then returns the first array.

<span id="fd551078"></span>
### Function **syntax**


* Syntax format

   ```SQL
   ARRAY_EXCEPT(KEY1, KEY2)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   

* Return value description

   The return value is of the array type.


<span id="0a569af6"></span>
### Example


* Scenario

   The statement removes duplicate elements 2 and 5 from `[10,2,30,14,5]` and `[4,2,5,7]`, then returns the first array `[10,30,14]`.

* Query and analysis statement

   ```SQL
   * | SELECT ARRAY_EXCEPT(array[10,2,30,14,5],array[4,2,5,7])
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8526e731ac849fa9ea03382c5cfeaea~tplv-goo7wpa0wc-image.image) </span>


<span id="4ad8f06d"></span>
## ARRAY_INTERSECT

The ARRAY_INTERSECT function returns the intersection of two arrays.

<span id="d35b5d5b"></span>
### Function **syntax**


* Syntax format

   ```SQL
   ARRAY_INTERSECT(KEY1, KEY2)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   

* Return value description

   The return value is of the array type.


<span id="e4915936"></span>
### Example


* Scenario

   The statement calculates the intersection of the `[10,2,30,14,5]` and `[4,2,5,7]` arrays.

* Query and analysis statement

   ```SQL
   * | SELECT ARRAY_INTERSECT(array[10,2,30,14,5],array[4,2,5,7])
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22799ceb2e2246c793a4b9f490152526~tplv-goo7wpa0wc-image.image) </span>


<span id="674a8086"></span>
## ARRAY_JOIN

The ARRAY_JOIN function concatenates the elements of an array into a string.

<span id="338bae4a"></span>
### Function **syntax**


* Syntax format

   * This format concatenates the elements of an array into a string using a specified delimiter. If the array contains a null element, the null element is ignored.

      ```SQL
      ARRAY_JOIN(KEY, delimiter)
      ```
      

   * This format concatenates the elements of an array into a string using a specified delimiter. If the array contains a null element, the null element is replaced with another string.

      ```SQL
      ARRAY_JOIN(KEY, delimiter,null_replacement)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   |delimiter |The character for connecting elements. It can be a string. |
   |null_replacement |The string to replace a null element. |
   

* Return value description

   The return value is of the varchar type.


<span id="e5db1fff"></span>
### Example


* Scenario

   The statement uses spaces to concatenate the elements of the `[null, 'Hello','World']` array into a string, then replaces the null element with `Replace`.

* Query and analysis statement

   ```SQL
   * | SELECT ARRAY_JOIN(array[null,'Hello','World'],' ','Replace')
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a19a8503bed741d39fa7ed42211b09dc~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="5d79631f"></span>
## ARRAY_MAX

The ARRAY_MAX function returns the maximum value in an array.

<span id="e38bcef2"></span>
### Function **syntax**


* Syntax format

   ```SQL
   ARRAY_MAX(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   

* Return value description

   The data type of the return value is the same as that of the array elements. If an array contains NULL, the function returns NULL.


<span id="19ee16f2"></span>
### Example


* Scenario

   The statement gets the maximum value of the `test_text` field.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16e0816a00574adfbb82922d82c63ac4~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   *| SELECT ARRAY_MAX(TRY_CAST(JSON_PARSE(test_text) as array(bigint))) AS max_number
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0dc2cfa8799b4afb85779251503a74ab~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="16aaadf3"></span>
## ARRAY_MIN

The ARRAY_MIN function returns the minimum value in an array.

<span id="ee67b5b6"></span>
### Function **syntax**


* Syntax format

   ```SQL
   ARRAY_MIN(KEY) 
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   

* Return value description

   The data type of the return value is the same as that of the array elements. If an array contains NULL, the function returns NULL.


<span id="05704576"></span>
### Example


* Scenario

   The function gets the minimum value of the `test_text` field.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/686c3a7d55f44793888c23b7bb02d388~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   *| SELECT ARRAY_MIN(try_cast(JSON_PARSE(test_text) as array(bigint))) AS min_number
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/811bfd8c29524faaa8faa8d56d0f8a61~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="84b79f27"></span>
## ARRAY_POSITION

The ARRAY_POSITION function is used to find the position of a specified element, with an element index starting at 1.

<span id="de2613bd"></span>
### Function **syntax**


* Syntax format

   ```SQL
   ARRAY_POSITION(KEY, element)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   |element |An element in an array. |
   

* Return value description

   The return value is of the bigint type . If the element is null, the result is also null; if the element does not exist, 0 is returned.


<span id="aa07eda1"></span>
### Example


* Scenario

   Find the position of element 18 in the array `[23, 94, 18, 66]`.

* Query and analysis statement

   ```SQL
   * | SELECT ARRAY_POSITION(array[23,94,18,66],18)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3f5025bbc4a4406a399c0f8299ca933~tplv-goo7wpa0wc-image.image) </span>


<span id="479a9a73"></span>
## ARRAY_REMOVE

The ARRAY_REMOVE function removes a specified element from an array.

<span id="54b357be"></span>
### Function **syntax**


* Syntax format

   ```SQL
   ARRAY_REMOVE(KEY, element)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   |*element* |The element to be removed. |
   

* Return value description

   The return value is of the array type. If the element to be removed is null, the function returns null.


<span id="5fcb50c3"></span>
### Example


* Scenario

   The statement removes 45 from the `[49,45,47]` array.

* Query and analysis statement

   ```SQL
   * | SELECT ARRAY_REMOVE(array[49,45,47],45)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b762d7a4e3c0437d979af4e0c07826f5~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="d8655b45"></span>
## ARRAY_SORT

The ARRAY_SORT function sorts the elements in an array in ascending order. If the array contains a null element, the null element is placed at the end.

<span id="8a414673"></span>
### Function **syntax**


* Syntax format

   ```SQL
   ARRAY_SORT(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   

* Return value description

   The return value is of the array type.


<span id="27f5a4e6"></span>
### Example


* Scenario

   The statement sorts the elements in the `['e', 'k', null, 'v', 'y']` array in ascending order.

* Query and analysis statement

   ```SQL
   * | SELECT ARRAY_SORT(ARRAY['e', 'k', null, 'v', 'y'])
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6e0579c1ffb491d86272a2e8aedafe6~tplv-goo7wpa0wc-image.image) </span>


<span id="f752534f"></span>
## ARRAY_TRANSPOSE

The ARRAY_TRANSPOSE function is used to transpose the array, extracting the same index elements in the two\-dimensional array to form a new two\-dimensional array.

<span id="1d8995a9"></span>
### Function syntax


* Syntax format

   ```SQL
   ARRAY_TRANSPOSE(KEY)
   ```
   

* Parameter description

   
   |parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array (double) type. |
   

* Return value description

   The return value is of array (double) type.


<span id="ce78e7fe"></span>
### Example


* Scenario

   Extract the elements 5, 20, 39 in the array `[5, 3, 7, 1]`, `[20, 39, 189, 117]`, `[39, 85, 27]`with indices of 1 to form an array `[5.0, 20.0, 39.0]`; extract the array `[5, 3, 7, 1]`, `[20, 39, 189, 117]`, `[39, 85, 27]`with indices of 2 to form an array `[3.0, 39.0, 85.0]`; and so on to form a new two\-dimensional array.

* Query and analysis statement

   ```SQL
   * | SELECT ARRAY_TRANSPOSE(array[array[5,3,7,1],array[20,39,189,117],array[39,85,27]])
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7043a517cd484600bf7f8fe3ed382d00~tplv-goo7wpa0wc-image.image) </span>


<span id="d745da8e"></span>
## ARRAY_UNION

The ARRAY_UNION function returns the union of two arrays.

<span id="957b94d1"></span>
### Function **syntax**


* Syntax format

   ```SQL
   ARRAY_UNION(KEY1, KEY2)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   

* Return value description

   The return value is of the array type.


<span id="5ac6c567"></span>
### Example


* Scenario

   The statement calculates the union of the `[10,2,30,14,5]` and `[4,2,5,7]` arrays.

* Query and analysis statement

   ```SQL
   * | SELECT ARRAY_UNION(ARRAY[10,2,30,14,5],ARRAY[4,2,5,7])
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f53ea9160b5410bb2974591e538d077~tplv-goo7wpa0wc-image.image) </span>


<span id="c3573ea2"></span>
## CARDINALITY

The CARDINALITY function returns the number of elements in an array.

<span id="15d7efdf"></span>
### Function **syntax**


* Syntax format

   ```SQL
   CARDINALITY(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   

* Return value description

   The return value is of the bigint type.


<span id="68a4ab34"></span>
### Example


* Scenario

   The statement calculates the number of elements of the `test_text` field.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c900eea5a144a9cb64bb5c5ee34c055~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   *| SELECT CARDINALITY(CAST(JSON_PARSE(test_text) as array(bigint)))
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3e23425f74a40dbb34077019fd04c3c~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="26ebdc38"></span>
## CONCAT

The CONCAT function concatenates multiple arrays into one array.

<span id="865fc9ac"></span>
### Function **syntax**


* Syntax format

   ```SQL
   CONCAT(KEY1, KEY2…)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   

* Return value description

   The return value is of the array type.


<span id="ab2027c1"></span>
### Example


* Scenario

   The statement concatenates the `[10,2,30,14,5]` and `[4,2,5,7]` arrays into one array.

* Query and analysis statement

   ```SQL
   * | SELECT CONCAT(ARRAY[10,2,30,14,5],ARRAY[4,2,5,7])
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21f9a9ff8f004ecea040f5e6012c0600~tplv-goo7wpa0wc-image.image) </span>


<span id="543a1866"></span>
## CONTAINS

The CONTAINS function verifies whether an array contains a specified element.

<span id="c757190c"></span>
### Function **syntax**


* Syntax format

   ```SQL
   CONTAINS(KEY, element)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   |element |The element to be verified. |
   

* Return value description

   The return value is of the boolean type. If the array contains the element, the function returns true. Otherwise, the function returns false.


<span id="c592e8d3"></span>
### Example


* Scenario

   The statement verifies whether the value of the `test_text` field contains 50.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea4969dadd304cd389002c5cf8c49856~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   *| SELECT CONTAINS(cast(JSON_PARSE(test_text) as array(bigint)), 50)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d55d63ee97f64be5bbf8a9626bb39d9b~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="cdaba532"></span>
## ELEMENT_AT

ELEMENT_AT function is used to get the element at the specified position in the array.

<span id="0b61151a"></span>
### Function syntax


* Syntax format

   ```SQL
   ELEMENT_AT(KEY, index)
   ```
   

* Parameter description

   
   |parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   |index |Specify the index of the element to be retrieved, starting at 1. The value is of bigint type. |
   

* Return value description

   The return value is of any data type.


<span id="e89af845"></span>
### Example


* Scenario

   Return the third element in the array `[5.0, 20.0, 39.0, 1, 7]`.

* Query and analysis statement

   ```SQL
   * | SELECT ELEMENT_AT(array[5.0,20.0,39.0, 1, 7], 3)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3a313420923457b9de19fc16b9a22d3~tplv-goo7wpa0wc-image.image) </span>


<span id="f88b951b"></span>
## FILTER

The FILTER function filters elements in an array with a Lambda expression.

<span id="7a5aba1f"></span>
### Function **syntax**


* Syntax format

   ```SQL
   FILTER(KEY, lambda_expression)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   |*lambda_expression* |The Lambda expression. |
   

* Return value description

   The return value is of the array type. The returned array only contains elements that meet the Lambda expression.


<span id="72c821e7"></span>
### Example


* Scenario

   The function gets elements that are greater than 0 from the `[10,-1,null,9,-7]` array with the Lambda expression `x -> x > 0`.

* Query and analysis statement

   ```SQL
   * | SELECT FILTER(array[10,-1,null,9,-7],x -> x > 0)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ded760d1fc264ce497e18c931a22ab17~tplv-goo7wpa0wc-image.image) </span>


<span id="db66aeb9"></span>
## FLATTEN

The FLATTEN function is used to convert a two\-dimensional array to a one\-dimensional array.

<span id="dac8d57c"></span>
### Function syntax


* Syntax format

   ```SQL
   FLATTEN(KEY)
   ```
   

* Parameter description

   
   |parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   

* Return value description

   The return value is of the array type.


<span id="3591ea68"></span>
### Example


* Scenario

   Converts the two\-dimensional array `array [array [3, 9, 4, 8, 0], array [9, 9, 7, 4, 1]]`to a one\-dimensional array.

* Query and analysis statement

   ```SQL
   * | SELECT FLATTEN(array[array[3,9,4,8,0],array[9,9,7,4,1]])
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d6d7ac8f64f480dae50d2bc2b9f36b9~tplv-goo7wpa0wc-image.image) </span>


<span id="ed4126d8"></span>
## REDUCE

The REDUCE function accumulates the individual elements of the array as defined in the lambda expression, and then returns the result of the evaluation.

<span id="cd6f162e"></span>
### Function syntax


* Syntax format

   ```SQL
   REDUCE(KEY, lambda_expression)
   ```
   

* Parameter description

   
   |parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   |lambda_expression |The first argument is the initial value, the second argument is the Lambda expression, and the third argument is the processing of the result of the Lambda expression evaluation. |
   

* Return value description

   The return value is of the bigint type .


<span id="2a06cde5"></span>
### Example


* Scenario

   Returns the result of concatenating elements in the array `['hello', 'world ', '!']`.

* Query and analysis statement

   ```SQL
   * | SELECT REDUCE(array['hello', 'world', '!'],'',(s, x) -> s || ' ' || x, s -> s)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f86e4a10ff1a4fb5b5e1989dac17f218~tplv-goo7wpa0wc-image.image) </span>


<span id="fe094fa4"></span>
## REVERSE

The REVERSE function reverses the elements in an array.

<span id="087efe99"></span>
### Function **syntax**


* Syntax format

   ```SQL
   REVERSE(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   

* Return value description

   The return value is of the array type.


<span id="051969ba"></span>
### Example


* Scenario

   The statement reverses the elements in the `[100,500,300,400,200]` array.

* Query and analysis statement

   ```SQL
   * | SELECT REVERSE(array[100,500,300,400,200])
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/379460de94c046b881296e9b959bd1b4~tplv-goo7wpa0wc-image.image) </span>


<span id="6ac55a26"></span>
## SEQUENCE

The SEQUENCE function is used to generate an array within the specified range, whose elements are a set of consecutive and increasing values within the specified range.

<span id="ff2a4db5"></span>
### Function syntax


* Syntax format

   * The increment interval is the default value of 1.

      ```SQL
      SEQUENCE(x, y)
      ```
      

   * Custom increment interval.

      ```SQL
      SEQUENCE(x, y, step)
      ```
      

* Parameter description

   
   |parameter |Description |
   |---|---|
   |x |A field or an expression. The value is of the bigint, timestamp (unix timestamp, date, and time expressions) type. |
   |y |A field or an expression. The value is of the bigint, timestamp (unix timestamp, date, and time expressions) type. |
   |step |Value interval.<br><br>When the argument value is a date and time expression, the step format is as follows:<br><br><br>* `Interval'n'year to month`, indicating an interval of n years.<br><br>* `Interval'n'day to second`, indicating an interval of n days. |
   

* Return value description

   The return value is of the array type.


<span id="3f48427c"></span>
### Example


* Scenario 1: Returns a radix sequence between 1 and 9.

   * Query and analysis statement

      ```SQL
      * | SELECT SEQUENCE(1,9,2)
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e363022517e4820a6b6511a91aea5f7~tplv-goo7wpa0wc-image.image) </span>

* Scenario 2: Generate a date sequence between 2024\-08\-01 and 2024\-08\-25 with an interval of 3 days.

   * Query and analysis statement

      ```SQL
      * | SELECT SEQUENCE (FROM_UNIXTIME(1722441600),FROM_UNIXTIME(1724515200),interval '3' day )
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a0571ef59444477b41ec40dadbfc557~tplv-goo7wpa0wc-image.image) </span>

* Scenario 3: Returns a Unix timestamp between 1722441600 and 1724515200, with an interval of 3 days.

   * Query and analysis statement

      ```SQL
      * | SELECT  sequence(1722441600,1724515200,3 * 24 * 60 * 60)
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb75c59e7a1e4972ac3698a81a2730ff~tplv-goo7wpa0wc-image.image) </span>


<span id="dfca0261"></span>
## SHUFFLE

The SHUFFLE function is used to randomly rearrange array elements.

<span id="ba26f25c"></span>
### Function syntax


* Syntax format

   ```SQL
   SHUFFLE(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   

* Return value description

   The return value is of the array type.


<span id="0d69aaf4"></span>
### Example


* Scenario

   Randomly reorders the elements in the array `[99, 87, 16, 43, 25]`.

* Query and analysis statement

   ```SQL
   *| SELECT SHUFFLE(array[99,87,16,43,25])
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5aaceecb0db0496ca724d8463f6546a2~tplv-goo7wpa0wc-image.image) </span>


<span id="367a506d"></span>
## SLICE

The SLICE function is used to obtain a subset of an array.

<span id="1d03c95c"></span>
### Function syntax


* Syntax format

   ```SQL
   SLICE(KEY, start, length)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   |start |Specifies the starting position of the index.<br><br><br>* If the `start` parameter is a negative number, the function starts to extract elements from the end of the array.<br><br>* If the `start` parameter is a positive number, the function starts to extract elements from the beginning of the array. |
   |length |Specify the number of elements in the subset. |
   

* Return value description

   The return value is of the array type.


<span id="23cfcc83"></span>
### Example


* Scenario

   Return a subset of the array `[99, 87, 16, 43, 25]`, starting from the second element, and the number of subset elements is 3.

* Query and analysis statement

   ```SQL
   * | SELECT SLICE(array[99,87,16,43,25],2,3)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c27efe820851487eb7cb9012aa2bd930~tplv-goo7wpa0wc-image.image) </span>


<span id="d07e1223"></span>
## TRANSFORM

The TRANSFORM function is used to apply a lambda expression to each element of an array.

<span id="dd031c19"></span>
### **Function** syntax


* Syntax format

   ```SQL
   TRANSFORM(KEY, lambda_expression)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   |lambda_expression |Lambda expressions. |
   

* Return value description

   The return value is of the array type.


<span id="25c48373"></span>
### Example


* Scenario

   Multiply the elements of the array `[99, 87, 16, 43, 25]`by 2 and return the result of the calculation.

* Query and analysis statement

   ```SQL
   * | SELECT TRANSFORM(array[99,87,16,43,25],x -> x * 2)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af9238453f3b48508c76a65285363a25~tplv-goo7wpa0wc-image.image) </span>


<span id="96429343"></span>
## ZIP

The ZIP function is used to combine multiple arrays into a two\-dimensional array according to their corresponding positions, and elements with the same index in each array form a new array.

<span id="6a76ce88"></span>
### Function syntax


* Syntax format

   ```SQL
   zip(KEY1, KEY2...) 
   ```
   

* Parameter description

   
   |parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the array type. |
   

* Return value description

   The return value is of the array type.


<span id="8f1d0df2"></span>
### Example


* Scenario

   Combines the arrays `[7, 1, 9]`, `['hello', 'world ','!']`and `[99, 87, 16]` into one two\-dimensional array.

* Query and analysis statement

   ```SQL
   * | SELECT ZIP(array[7,1,9], array['hello','world','!'],array[99,87,16])
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2b683de68a048a28f76736bdfb1cae1~tplv-goo7wpa0wc-image.image) </span>

---
title: "Mathematical calculation functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Mathematical-calculation-functions-2"
---

This topic describes the syntax of mathematical calculation functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="3e72332b"></span>
## List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>



|Function |Function syntax |Description |
|---|---|---|
|ABS |ABS(KEY) |Calculates the absolute value of a number. |
|ACOS |ACOS(KEY) |Calculates the arccosine of a value. |
|ASIN |ASIN(KEY) |Calculates the arcsine of a value. |
|ATAN |ATAN(KEY) |Calculates the arctangent of a value. |
|CBRT |CBRT(KEY) |Calculates the cube root of a value. |
|CEIL |CEIL(KEY) |Rounds values up to the nearest integer. |
|CEILING |CEILING(KEY) |Rounds values up to the nearest integer. |
|COS |COS(KEY) |Calculates the cosine of a value. |
|COSH |COSH(KEY) |Calculates the hyperbolic cosine of a value. |
|COSINE_SIMILARITY |COSINE_SIMILARITY(KEY1, KEY2) |Calculates the cosine similarity between two values. |
|DEGREES |DEGREES |Converts radians to degrees. |
|E |E() |Calculates the value of the natural base e. |
|EXP |EXP(x) |Calculates the natural base e to the power of x. |
|FLOOR |FLOOR(KEY) |Rounds a number down to the nearest integer. |
|FROM_BASE |FROM_BASE(number_str, base) |Converts a numeric string in a given base to its decimal equivalent. |
|IS_NAN |IS_NAN(KEY) |Determines whether the value is NaN. If so, return true. |
|LN |LN(KEY) |Calculates the natural logarithm of a value. |
|LOG |LOG(KEY) |Calculates the natural logarithm of a number. |
|LOG2 |LOG2(KEY) |Calculates the logarithm of the target value to the base 2. |
|LOG10 |LOG10(KEY) |Calculates the base 10 logarithm of a number. |
|MOD |MOD(KEY1, KEY2) |Calculates the remainder after dividing two values. |
|NAN |NAN() |Returns a `NaN`value. |
|PI |PI() |Returns the value of π, accurate to 15 decimal places. |
|POWER |POWER(KEY, y) |Raises a number to the power of y. |
|RADIANS |RADIANS(KEY) |Converts degrees to radians. |
|RAND |RAND() |Returns a random number. |
|RANDOM |RANDOM() |Returns a random number in the range [0,1). |
||RANDOM(0, KEY) |Returns a random number in the range [0,KEY). |
|ROUND |ROUND(KEY) |Rounds a number to the nearest integer. |
||ROUND(KEY,n) |Rounds a number to the nearest decimal with n decimal places. |
|SIGN |SIGN(KEY) |Determines the sign of the target value, indicating the positivity or negativity of the value through 1, 0, and \-1. |
|SIN |SIN(KEY) |Calculates the sine of the target value. |
|SQRT |SQRT(KEY) |Calculates the square root of a number. |
|TAN |TAN(KEY) |Calculates the tangent of the target value. |
|TANH |TANH(KEY) |Calculates the hyperbolic tangent of the target value. |
|TO_BASE |TO_BASE(number, base) |Converts a decimal to a string of the specified base. |
|WIDTH_BUCKET |WIDTH_BUCKET(KEY, bound1, bound2, numBuckets) |Divide a range of values into multiple buckets of the same size, and then return the number of the bucket in which the KEY value resides. |
|WIDTH_BUCKET |WIDTH_BUCKET(KEY, bins) |Use an array to specify the range of buckets, and then return the number of the bucket in which the KEY value resides. |


<span id="ABS"></span>
## ABS

The ABS function calculates the absolute value of a number.

<span id="66845e54"></span>
### Function syntax


* Syntax format

   ```SQL
   ABS(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the smallint, integer, real, tinyint, bigint, double, or decimal type. |
   

* Return value description

   The type of the return value is the same as the type of the parameter value.


<span id="9f6da7fc"></span>
### Example


* Scenario

   The statement is used to calculate the absolute value based on the value of the `RespSize` field.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/925f7bb31d4840e894028741402254b8~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT abs(RespSize)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f14f4eca33149faa2fafc8d1aca4b68~tplv-goo7wpa0wc-image.image) </span>


<span id="711406d1"></span>
## ACOS

The ACOS function is used to calculate the arccosine of a value.

<span id="42f6a9f5"></span>
### Function syntax


* Syntax format

   ```SQL
   ACOS(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. The value range is [\-1, 1].<br><br>If the value is out of the range [\-1, 1], the ACOS function returns NaN. |
   

* Return value description

   The return value is of the double type.


<span id="01afa0b5"></span>
### Example


* Scenario

   Calculate the arccosine of a 45° angle.

* Query and analysis statement

   ```SQL
   * | SELECT ACOS(PI()/4)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df829ab54a5b4105be55d4a59daa091a~tplv-goo7wpa0wc-image.image) </span>


<span id="9728e648"></span>
## ASIN

The ASIN function is used to calculate the arcsine of a value.

<span id="eb0a328a"></span>
### Function syntax


* Syntax format

   ```SQL
   ASIN(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. The value range is [\-1, 1].<br><br>If the value is out of the range [\-1, 1], the ASIN function returns NaN. |
   

* Return value description

   The return value is of the double type.


<span id="5a457f3b"></span>
### Example


* Scenario

   Calculate the arcsine at a 45° angle.

* Query and analysis statement

   ```SQL
   * | SELECT ASIN(PI()/4)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65f350bca5ab4ab8a7398f94d6d65db0~tplv-goo7wpa0wc-image.image) </span>


<span id="bfd55f4c"></span>
## ATAN

The ATAN function is used to calculate the arctangent of a value.

<span id="e4402589"></span>
### Function syntax


* Syntax format

   ```SQL
   ATAN(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="07ca4844"></span>
### Example


* Scenario

   Calculate the arctangent of a 45° angle.

* Query and analysis statement

   ```SQL
   * | SELECT ATAN(PI()/4)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a31f7d2442c4ade853b852ace361249~tplv-goo7wpa0wc-image.image) </span>


<span id="07d8c245"></span>
## CBRT

The CBRT function is used to calculate the cube root of a value.

<span id="742c0204"></span>
### Function syntax


* Syntax format

   ```SQL
   CBRT(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="b6ae5272"></span>
### Example


* Scenario

   Calculate the cube root of 64.

* Query and analysis statement

   ```SQL
   * | SELECT CBRT(64)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de2ad1a481dd4b43addb7875c3ece619~tplv-goo7wpa0wc-image.image) </span>


<span id="d9c40580"></span>
## CEIL

The CEIL function is used to round values up to the nearest integer. The CEIL function is the same as the CEILING function.

<span id="e7c7ebdc"></span>
### Function syntax


* Syntax format

   ```SQL
   CEIL(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the tinyint, smallint, integer, real, bigint, double, or decimal type.<br><br><br>* If the value is positive, the function rounds the value away from 0.<br><br>* If the value is negative, the function rounds the value towards 0. |
   

* Return value description

   The return value is the same type as the parameter value.


<span id="960e7d8e"></span>
### Example


* Scenario

   Round the values of the `ReqTime` field up to the nearest integer.

* Field sample

   ```SQL
   ReqTime:1.7
   ```
   

* Query and analysis statement

   ```SQL
   * | SELECT ceil(ReqTime) AS ReqTime
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0c5efe0cf63412995cb209593417294~tplv-goo7wpa0wc-image.image) </span>


<span id="e0614f79"></span>
## CEILING

The CEILING function is used to round values up to the nearest integer.

<span id="945cb1cc"></span>
### Function syntax


* Syntax format

   ```SQL
   CEILING(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the tinyint, smallint, integer, real, bigint, double, or decimal type.<br><br><br>* If the value is positive, the function rounds the value away from 0.<br><br>* If the value is negative, the function rounds the value towards 0. |
   

* Return value description

   The return value is the same type as the parameter value.


<span id="dbb000f3"></span>
### Example


* Scenario

   Round the values of the `ReqTime` field up to the nearest integer.

* Field Sample

   ```SQL
   ReqTime:1.7
   ```
   

* Query and analysis statement

   ```SQL
   * | SELECT CEILING(ReqTime) AS ReqTime
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0c5efe0cf63412995cb209593417294~tplv-goo7wpa0wc-image.image) </span>


<span id="af1fb6ab"></span>
## COS

The COS function is used to calculate the cosine of a value.

<span id="79ea0d98"></span>
### Function syntax


* Syntax format

   ```SQL
   COS(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="4afbfbb4"></span>
### Example


* Scenario

   Calculate the cosine of a 60° angle.

* Query and analysis statement

   ```SQL
   * | SELECT COS(PI()/3)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8ef7400cfca4056bf27870bfab4362b~tplv-goo7wpa0wc-image.image) </span>


<span id="67ce348d"></span>
## COSH

The COSH function is used to calculate the hyperbolic cosine of a value.

<span id="f6d55653"></span>
### Function syntax


* Syntax format

   ```SQL
   COSH(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="1f6bbe66"></span>
### Example


* Scenario

   Calculate the hyperbolic cosine of a 60° angle.

* Query and analysis statement

   ```SQL
   * | SELECT COSH(PI()/3)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b458d5c8c2d9498298c8d62158164065~tplv-goo7wpa0wc-image.image) </span>


<span id="033fc8f1"></span>
## COSINE_SIMILARITY

COSINE_SIMILARITY function is used to calculate the cosine similarity between two values.

<span id="868e6e72"></span>
### Function syntax


* Syntax format

   ```SQL
   COSINE_SIMILARITY(KEY1, KEY2)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the map(varchar, double) type. |
   

* Return value description

   The return value is of the double type.


<span id="b5773ab3"></span>
### Example


* Scenario

   Calculate the cosine similarity between two vectors.

* Query and analysis statement

   ```SQL
   * | SELECT COSINE_SIMILARITY(MAP(ARRAY['regan'], ARRAY[2.3]), MAP(ARRAY['regan'], ARRAY[3.7]))
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c4b0d9210da48269e1c7f28b3b473bb~tplv-goo7wpa0wc-image.image) </span>


<span id="eac4f0fe"></span>
## DEGREES

The DEGREES function is used to convert radians to degrees.

<span id="46ba21f8"></span>
### Function syntax


* Syntax format

   ```SQL
   DEGREES(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="430582be"></span>
### Example


* Scenario

   Convert the radian value π to degrees.

* Query and analysis statement

   ```SQL
   * | SELECT DEGREES(PI())
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93a1c9bdd378463cb72d2dedb877d4ec~tplv-goo7wpa0wc-image.image) </span>


<span id="b999cea8"></span>
## E

The E function calculates the value of the natural base e.

<span id="e5bcd066"></span>
### Function syntax


* Syntax format

   ```SQL
   E()
   ```
   

* Return value description

   The return value is of the double type.


<span id="0acc8df2"></span>
### Example


* Scenario

   Returns the value of the natural base e.

* Query and analysis statement

   ```SQL
   * | SELECT E()
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3adc9b8b543149a0bd4e60907948cdb4~tplv-goo7wpa0wc-image.image) </span>


<span id="77c53fa9"></span>
## EXP

The EXP function is used to calculate the natural base e to the power of x.

<span id="521a0dc3"></span>
### Function syntax


* Syntax format

   ```SQL
   EXP(x)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |The value is of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="dc6bbfca"></span>
### Example


* Scenario

   Calculate e raised to the power of 4.

* Query and analysis statement

   ```SQL
   * | SELECT EXP(4)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2a8a3baa119467283c403b67e1f30e3~tplv-goo7wpa0wc-image.image) </span>


<span id="59e7214c"></span>
## FLOOR

The FLOOR function rounds a number down to the nearest integer.

<span id="02016fc9"></span>
### Function syntax


* Syntax format

   ```SQL
   FLOOR(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the Tinyint, Smallint, Integer, Real, Bigint, Double, or Decimal type. |
   

* Return value description

   The return value is the largest integer that is less than the specified parameter value. The return value is of the double type.


<span id="237634cd"></span>
### Example


* Scenario

   The statement is used to calculate the square root of the values of the `ReqSize` field and rounds the values down to the nearest integers.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e900bb1b80041688783058e6dbfd89d~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT FLOOR(SQRT(ReqSize))
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efdf452606d24714aacca61af09bb356~tplv-goo7wpa0wc-image.image) </span>


<span id="56f18279"></span>
## FROM_BASE

The FROM_BASE function is used to convert a numeric string in a given base to its decimal equivalent.

<span id="8d9b5eb1"></span>
### Function syntax


* Syntax format

   ```SQL
   FROM_BASE(number_str, base)
   ```
   

* Parameter description

   
   |parameter |Description |
   |---|---|
   |number_str |Numeric string. Specify a value of the Varchar type. |
   |base |The base of `number_str`. It is a value of the Bigint type. The range of values is [2, 36]. |
   

* Return value description

   The return value is of Bigint type.


<span id="f970e0b3"></span>
### Example


* Scenario

   Converts the string 1001100110 to a decimal number.

* Query and analysis statement

   ```SQL
   * | SELECT FROM_BASE('1001100110',2)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c09077a34f034e2e9bfa4fca2b4e0b7b~tplv-goo7wpa0wc-image.image) </span>


<span id="76a9adb2"></span>
## IS_NAN

IS_NAN function is used to determine whether the value is NaN. If so, return true.

<span id="9e4497b3"></span>
### Function syntax


* Syntax format

   ```SQL
   IS_NAN(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. |
   

* Return value description

   The return value is of boolean type.


<span id="6f9f475c"></span>
### Example


* Scenario

   Determines whether the value of the `apply_time`field is NaN.

* Query and analysis statement

   ```SQL
   * | SELECT IS_NAN(apply_time)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe639dd15d354a1db450cc4bbb4cf45b~tplv-goo7wpa0wc-image.image) </span>


<span id="6b03a105"></span>
## LN

The LN function is used to calculate the natural logarithm of a value.

<span id="ae5b4f1e"></span>
### Function syntax


* Syntax format


```SQL
LN(KEY)
```



* Parameter description

   
   |parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. The value must be greater than 0. |
   

* Return value description

   The return value is of the double type.


<span id="5f894187"></span>
### Example


* Scenario

   Calculate the natural logarithm of 5.

* Query and analysis statement

   ```SQL
   * | SELECT LN(5)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3096ae69ade94160b6a8d5bc5f3776e8~tplv-goo7wpa0wc-image.image) </span>


<span id="56ef0c5f"></span>
## LOG

The LOG function calculates the natural logarithm of a number.

<span id="66d0336f"></span>
### Function syntax


* Syntax format

   ```SQL
   LOG(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="d7e42c16"></span>
### Example


* Scenario

   The statement is used to calculate the natural logarithms of the values of the `ReqSize` field.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e900bb1b80041688783058e6dbfd89d~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT LOG(ReqSize)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94a3c2ae4d294e5bb2b763f6163bca4e~tplv-goo7wpa0wc-image.image) </span>


<span id="49a99612"></span>
## LOG2

The LOG2 function is used to calculate the logarithm of the target value to the base 2.

<span id="92734fa5"></span>
### Function syntax


* Syntax format

   ```SQL
   LOG2(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="47e0a652"></span>
### Example


* Scenario

   Calculate the base 2 logarithm of 80.

* Query and analysis statement

   ```SQL
   * | SELECT LOG2(80)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7e1e69aaf7e4c6093f7edefb4ca5152~tplv-goo7wpa0wc-image.image) </span>


<span id="1149af65"></span>
## LOG10

The LOG10 function calculates the base 10 logarithm of a number.

<span id="24dabc25"></span>
### Function syntax


* Syntax format

   ```SQL
   LOG10(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="8c6cbebd"></span>
### Example


* Scenario

   The statement is used to calculate the base 10 logarithms of the values of the `ReqSize` field.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e900bb1b80041688783058e6dbfd89d~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT LOG10(ReqSize)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4113133442824cf0918500b0b07a4c60~tplv-goo7wpa0wc-image.image) </span>


<span id="2c28615a"></span>
## MOD

The MOD function is used to calculate the remainder after dividing two values.

<span id="f41321b4"></span>
### Function syntax


* Syntax format

   ```SQL
   MOD(KEY1, KEY2)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |Field, expression, whose values are of type tinyint, smallint, integer, real, bigint, double, decimal. |
   

* Return value description

   The return value is the same as the data type of the parameter value.


<span id="fd58f04c"></span>
### Example


* Scenario

   Calculate the remainder divided by 97 and 6.

* Query and analysis statement

   ```SQL
   * | SELECT MOD(97,6)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fa3dad0b28440f99cc7eb0028dba43a~tplv-goo7wpa0wc-image.image) </span>


<span id="1185f4c0"></span>
## NAN

The NAN function is used to return a `NaN`value.

<span id="454cf8e3"></span>
### Function syntax


* Syntax format

   ```SQL
   NAN()
   ```
   

* Return value description

   The return value is of the double type.


<span id="fd958dd4"></span>
### Example


* Scenario

   Returns a NaN value.

* Query and analysis statement

   ```SQL
   * | SELECT NAN()
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4cdcaf9f78484f9db0afbca54b0c8d32~tplv-goo7wpa0wc-image.image) </span>


<span id="020b823b"></span>
## PI

The PI function is used to return the value of π, accurate to 15 decimal places.

<span id="3af62755"></span>
### Function syntax


* Syntax format

   ```SQL
   PI()
   ```
   

* Return value description

   The return value is of the double type.


<span id="150a8814"></span>
### Example


* Scenario

   Returns the value of π, accurate to 15 decimal places.

* Query and analysis statement

   ```SQL
   * | SELECT PI()
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf351e9c1dc3495a924ea6cee37903d2~tplv-goo7wpa0wc-image.image) </span>


<span id="b58c2be4"></span>
## POWER

The POWER function raises a number to the power of y.

<span id="f2f6bdd6"></span>
### Function syntax


* Syntax format

   ```SQL
   POWER(KEY, y)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the double type. |
   |y |The value is of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="f4381be8"></span>
### Example


* Scenario

   The statement is used to raise the values of the `ReqSize` field to the power of three.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e900bb1b80041688783058e6dbfd89d~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT POWER(ReqSize, 3)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a20ba8d6dde54699bde9f8c1d6e72af9~tplv-goo7wpa0wc-image.image) </span>


<span id="9cf032f5"></span>
## RADIANS

The RADIANS function is used to convert degrees to radians.

<span id="9cdafb8f"></span>
### Function syntax


* Syntax format

   ```SQL
   RADIANS(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="986b647c"></span>
### Example


* Scenario

   Calculate the radian corresponding to 90°.

* Query and analysis statement

   ```SQL
   * | SELECT RADIANS(90)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52249e435bb44eddbee3da34bd21f369~tplv-goo7wpa0wc-image.image) </span>


<span id="1c20ae81"></span>
## RAND

The RAND function is used to return a random number.

<span id="702a51fc"></span>
### Function **syntax**


* Syntax format

   ```SQL
   RAND()
   ```
   

* Return value description

   The return value is of the double type.


<span id="15b08270"></span>
### Example


* Scenario

   Returns a random number.

* Query and analysis statement

   ```SQL
   * | SELECT RAND()
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7f824e4b4a547858d5ee6e66ba3b14d~tplv-goo7wpa0wc-image.image) </span>


<span id="4ad6905c"></span>
## RANDOM

The RANDOM function returns a random number in the range [0,1) or [0,KEY).

<span id="7bb18b02"></span>
### Function **syntax**


* Syntax format

   * This format returns a random number in the range [0,1).

      ```SQL
      RANDOM()
      ```
      

   * This format returns a random number in the range [0,KEY).

      ```SQL
      RANDOM(KEY)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the Tinyint, Smallint, Integer, or Bigint type. |
   

* Return value description

   The type of the return value is the same as the type of the parameter value.


<span id="108d8203"></span>
### Example


* Scenario

   The statement is used to get a random number in the range `[0,100)`.

* Query and analysis statement

   ```SQL
   * | select RANDOM(100)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa6ead060f2345709bad48afd38c2c7c~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="45304f0c"></span>
## ROUND

The ROUND function rounds a number to the nearest integer.

<span id="feaeb0e2"></span>
### Function syntax


* Syntax format

   * rounds the values of KEY \*\* to the nearest integer.

      ```SQL
      ROUND(KEY)
      ```
      

   * rounds the values of KEY \*\* to the nearest decimal with n decimal places.

      ```SQL
      ROUND(KEY,n)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the Tinyint, Smallint, Integer, or Bigint type. |
   

* Return value description

   The data type of the return value is the same as the type of the parameter value.


<span id="b19acef3"></span>
### Example


* Scenario

   The statement is used to calculate the square root of the values of the `ReqSize` field and rounds the values to the nearest integer.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e900bb1b80041688783058e6dbfd89d~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT ROUND(SQRT(ReqSize))
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e5b728752de43afb4aa337f075e414a~tplv-goo7wpa0wc-image.image) </span>


<span id="2ecbfa8c"></span>
## SIGN

The SIGN function is used to determine the sign of the target value, indicating the positivity or negativity of the value through 1, 0, and \-1.

<span id="34f25aca"></span>
### Function syntax


* Syntax format

   ```SQL
   SIGN(KEY)
   ```
   

* Parameter description

   
   |parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the integer, smallint, tinyint, real, double, bigint, or decimal (p, s) type.<br><br><br>* The value is positive, the function returns 1.<br><br>* The value is 0, the function returns 0.<br><br>* The value is negative, the function returns \-1. |
   

* Return value description

   The return value is the same as the data type of the parameter value.


<span id="294cdd17"></span>
### Example


* Scenario

   Confirm the symbol for the number \-3.

* Query and analysis statement

   ```SQL
   * | SELECT SIGN(-3)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78f65c4562a140f7bfd2ce6430fbfa90~tplv-goo7wpa0wc-image.image) </span>


<span id="d51d554d"></span>
## SIN

The SIN function is used to calculate the sine of the target value.

<span id="477696de"></span>
### Function syntax


* Syntax format

   ```SQL
   SIN(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="24fa5749"></span>
### Example


* Scenario

   Calculate the sine of a 60° angle.

* Query and analysis statement

   ```SQL
   * | SELECT SIN(PI()/3)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03da74669edd48b7b826837a090862fe~tplv-goo7wpa0wc-image.image) </span>


<span id="a237c98e"></span>
## SQRT

The SQRT function calculates the square root of a number.

<span id="167cfb6c"></span>
### Function syntax


* Syntax format

   ```SQL
   SQRT(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="df68044e"></span>
### Example


* Scenario

   The statement is used to calculate the square root of the values of the `ReqSize` field.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e900bb1b80041688783058e6dbfd89d~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT SQRT(ReqSize)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b46958cc39ca4c70833bcb3b9f0fcfea~tplv-goo7wpa0wc-image.image) </span>


<span id="8ff2bad2"></span>
## TAN

The TAN function is used to calculate the tangent of the target value.

<span id="7cbc0e7e"></span>
### Function syntax


* Syntax format

   ```SQL
   TAN(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="60273594"></span>
### Example


* Scenario

   Calculate the tangent of the tan60° angle.

* Query and analysis statement

   ```SQL
   * | SELECT TAN(PI()/3)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da83f2bfe6fc4b108dec9c656ababf2f~tplv-goo7wpa0wc-image.image) </span>


<span id="4adea205"></span>
## TANH

The TANH function is used to calculate the hyperbolic tangent of the target value.

<span id="b6559484"></span>
### Function syntax


* Syntax format

   ```SQL
   TANH(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="9ddb1a62"></span>
### Example


* Scenario

   Calculate the hyperbolic tangent of 60 degrees.

* Query and analysis statement

   ```SQL
   * | SELECT TANH(PI()/3)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75d8ea6795e74130a516ba7faa80fef4~tplv-goo7wpa0wc-image.image) </span>


<span id="99ee1dc1"></span>
## TO_BASE

TO_BASE function converts a decimal to a string of the specified base.

<span id="bcbca39e"></span>
### Function syntax


* Syntax format

   ```SQL
   TO_BASE(number, base)
   ```
   

* Parameter description

   
   |parameter |Description |
   |---|---|
   |number |The value is of Bigint type . |
   |base |Specify the base for the Bigint type. The valid range of values is [2, 36]. |
   

* Return value description

   The return value is of Varchar type.


<span id="583450c5"></span>
### Example


* Scenario

   Converts 116 to a binary string.

* Query and analysis statement

   ```SQL
   * | SELECT TO_BASE(116, 2)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb62b3cdf19c470a9a864bd187d0433f~tplv-goo7wpa0wc-image.image) </span>


<span id="9f7e2de2"></span>
## WIDTH_BUCKET

WIDTH_BUCKET function returns the number of the bucket in which the target value resides.

<span id="602822b7"></span>
### Function syntax


* Syntax format

   * Divide a range of values into multiple buckets of the same size, and then return the number of the bucket in which the KEY value resides.

      ```SQL
      WIDTH_BUCKET(KEY, bound1, bound2, numBuckets)
      ```
      

   * Use an array to specify the range of buckets, and then return the number of the bucket in which the KEY value resides.

      ```SQL
      WIDTH_BUCKET(KEY, bins)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. |
   |bound1 |Specify the lower limit of the numerical range. |
   |bound2 |Specify the upper limit of the numerical range. |
   |numBuckets |Specify the number of buckets.<br><br>The value must be an integer greater than 0. |
   |bins |Use an array to specify the range of the bucket. The value is an array of double type. |
   

* Return value description

   The return value is of type Bigint.

   * When the KEY value is within the specified range, the return value is the number of the bucket in which the KEY value resides.

   * Outside the lower limit of the KEY value, the return value is 0.

   * Outside the upper limit of the KEY value range, the return value is `numBuckets`+ 1.


<span id="324beb5a"></span>
### Example


* Scenario 1

   * example

      Divide the [0, 50) range into 5 buckets, and then return the number of the buckets where each `ReqTime`field value is located.

   * Query and analysis statement

      ```SQL
      * | SELECT ReqTime, WIDTH_BUCKET(ReqTime, 0, 50, 5) AS num
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1555e1ce122a4ffeaedb12babc1a91bb~tplv-goo7wpa0wc-image.image) </span>

* Scenario 2

   * example

      Use an array to specify a range of 5 buckets, and then return the number of buckets in which each `ReqTime`field value resides.

   * Query and analysis statement

      ```SQL
      * | SELECT ReqTime, WIDTH_BUCKET(ReqTime, array[10,20,30,40,50]) AS num
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f10c3b9a788c4fa385a0cb793887dfbb~tplv-goo7wpa0wc-image.image) </span>

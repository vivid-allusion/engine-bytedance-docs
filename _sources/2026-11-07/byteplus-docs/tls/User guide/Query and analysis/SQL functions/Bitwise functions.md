---
title: "Bitwise functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Bitwise-functions"
---

This topic describes the syntax of bitwise functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="41161186"></span>
### List of functions


|Function |Syntax |Description |
|---|---|---|
|BIT_COUNT |BIT_COUNT(x, bits) |Counts the number of 1 in the binary representation of x. |
|BITWISE_AND |BITWISE_AND(x, y) |Returns the result of the bitwise AND operation on x and y. |
|BITWISE_NOT |BITWISE_NOT(x) |Returns the result of the bitwise NOT operation on x. |
|BITWISE_OR |BITWISE_OR(x, y) |Returns the result of the bitwise OR operation on x and y. |
|BITWISE_XOR |BITWISE_XOR(x, y) |Returns the result of the bitwise XOR operation on x and y. |


<span id="26f40e78"></span>
### BIT_COUNT

The BIT_COUNT function is used to count the number of 1 in the binary representation of x.

<span id="ed7f18d5"></span>
#### Function **syntax**


* Syntax format

   ```SQL
   BIT_COUNT(x, bits)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |*x* |The value is of the Bigint type. |
   |bits |Specify the number of binary digits, for example, 8 bits. |
   

* Number of return results

   The return value is of the Bigint type.


<span id="9164e617"></span>
#### Example


* Scenario

   Calculate the binary number of 2 (00000010), and return the number of 1 in its binary representation.

* Query and analysis statement

   ```SQL
   * | SELECT bit_count(2, 8)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb5fc093f29943b7b52555a1cf665cb6~tplv-goo7wpa0wc-image.image) </span>


<span id="11b1c695"></span>
### BITWISE_AND

The BITWISE_AND function returns the result of the bitwise AND operation on x and y.

<span id="38aa85ac"></span>
#### Function **syntax**


* Syntax format

   ```SQL
   BITWISE_AND(x, y)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |*x* |The value is of the Bigint type. |
   |y |The value is of the Bigint type. |
   

* Number of return results

   The return value is of the Bigint type.


<span id="d2e838c1"></span>
#### Example


* Scenario

   Perform a bitwise AND operation on 3 and 5.

* Query and analysis statement

   ```SQL
   * | SELECT BITWISE_AND(3, 5)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b737164aa23403b994e84792b9b12f5~tplv-goo7wpa0wc-image.image) </span>


<span id="19d71cee"></span>
### BITWISE_NOT

The BITWISE_NOT function returns the result of the bitwise NOT operation on x \*\*.

<span id="6d917ad5"></span>
#### Function **syntax**


* Syntax format

   ```SQL
   BITWISE_NOT(x)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |*x* |The value is of the Bigint type. |
   

* Number of return results

   The return value is of the Bigint type.


<span id="827941dd"></span>
#### Example


* Scenario

   Perform a bitwise NOT operation on 4.

* Query and analysis statement

   ```SQL
   * | SELECT BITWISE_NOT(4)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3dce8e0059c43d6a8bd81bdbb8c16f3~tplv-goo7wpa0wc-image.image) </span>


<span id="a54634db"></span>
### BITWISE_OR

The BITWISE_OR function returns the result of the bitwise OR operation on x and y.

<span id="90ebe878"></span>
#### Function **syntax**


* Syntax format

   ```SQL
   BITWISE_OR(x, y)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |*x* |The value is of the Bigint type. |
   |y |The value is of the Bigint type. |
   

* Number of return results

   The return value is of the Bigint type.


<span id="0c3481eb"></span>
#### Example


* Scenario

   Perform a bitwise OR operation on 3 and 5.

* Query and analysis statement

   ```SQL
   * | SELECT BITWISE_OR(3, 5)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18624d5b8aec4442924112df84350d1a~tplv-goo7wpa0wc-image.image) </span>


<span id="e0ca9925"></span>
### BITWISE_XOR

The BITWISE_XOR function returns the result of the bitwise XOR operation on x and y.

<span id="ffc196cd"></span>
#### Function **syntax**


* Syntax format

   ```SQL
   BITWISE_XOR(x, y)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |*x* |The value is of the Bigint type. |
   |y |The value is of the Bigint type. |
   

* Number of return results

   The return value is of the Bigint type.


<span id="965af172"></span>
#### Example


* Scenario

   Perform a bitwise XOR operation on 3 and 5.

* Query and analysis statement

   ```SQL
   * | SELECT BITWISE_XOR(3, 5)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ffbce5fec6247a981236c8a9c67ceb1~tplv-goo7wpa0wc-image.image) </span>

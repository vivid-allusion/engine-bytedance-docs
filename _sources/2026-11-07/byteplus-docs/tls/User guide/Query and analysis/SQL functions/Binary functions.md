---
title: "Binary functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Binary-functions"
---

This topic describes the syntax of binary functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="4852b6f2"></span>
### List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>



|Function |Function Syntax |Description |
|---|---|---|
|FROM_BASE64 |FROM_BASE64(KEY) |Converts a Base64\-encoded string to a binary string. |
|FROM_BASE64URL |FROM_BASE64URL(KEY) |Converts a Base64\-encoded string to a binary string using URL\-safe characters. |
|FROM_HEX |FROM_HEX(KEY) |Converts a hexadecimal string to a binary string. |
|LENGTH |LENGTH(KEY) |Computes the length of a binary string. |
|MD5 |MD5(KEY) |Computes the MD5 hash value for a binary string. |
|TO_BASE64 |TO_BASE64(KEY) |Converts a binary string to a Base64\-encoded string. |
|TO_BASE64URL |TO_BASE64URL(KEY) |Converts a binary string to a Base64\-encoded string using URL\-safe characters. |
|TO_HEX |TO_HEX(KEY) |Converts a binary string to a hexadecimal string. |
|SHA1 |SHA1(KEY) |Computes the SHA\-1 hash value for a binary string. |
|SHA256 |SHA256(KEY) |Computes the SHA\-256 hash value for a binary string. |
|SHA512 |SHA512(KEY) |Computes the SHA\-512 hash value for a binary string. |
|XXHASH64 |XXHASH64(KEY) |Computes the XXHASH64 hash value for a binary string. |


<span id="04a769ce"></span>
## FROM_BASE64

The FROM_BASE64 function converts a Base64\-encoded string to a binary string.

<span id="25d61867"></span>
### Function **syntax**


* Syntax format

   ```SQL
   FROM_BASE64(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Binary type. |
   

* Return value description

   The return value is of the Varbinary type.


<span id="1a21414c"></span>
### Example


* Scenario

   Convert a Base64\-encoded string to a binary string, then convert the binary string to a hexadecimal string.

* Query and analysis statement

   ```SQL
   * | SELECT TO_HEX(FROM_BASE64('c2xz'))
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6564f191f194b65adcdf0d2db08b073~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="991691a5"></span>
## FROM_BASE64URL

The FROM_BASE64URL function converts a Base64\-encoded string to a binary string using URL\-safe characters.

<span id="df1df0d7"></span>
### Function **syntax**


* Syntax format

   ```SQL
   FROM_BASE64URL(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Binary type. |
   

* Return value description

   The return value is of the Varbinary type.


<span id="3b8437f1"></span>
### Example


* Scenario

   Converts a Base64\-encoded string to a binary string using URL\-safe characters.

* Query and analysis statement

   ```SQL
   * | SELECT TO_HEX(FROM_BASE64URL('c2xz'))
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c9b8e6320f741c288843ccaf845e968~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="1983530a"></span>
## FROM_HEX

The FROM_HEX function converts a hexadecimal string to a binary string.

<span id="fbf193a8"></span>
### Function **syntax**


* Syntax format

   ```SQL
   FROM_HEX(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Binary type. |
   

* Return value description

   The return value is of the Varbinary type.


<span id="4a654f38"></span>
### Example


* Scenario

   Convert the hexadecimal string D74D to a binary string.

* Query and analysis statement

   ```SQL
   * | SELECT FROM_HEX('D74D')
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20a640ce721b45fc8e144d35d1f307bb~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="a434db73"></span>
## LENGTH

The LENGTH function calculates the length of a binary string.

<span id="715e5ba6"></span>
### Function **syntax**


* Syntax format

   ```SQL
   LENGTH(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Binary type. |
   

* Return value description

   The return value is of the Binary type.


<span id="b526cdb5"></span>
### Example


* Scenario

   Calculate the length of `'00101000'`.

* Query and analysis statement

   ```SQL
   * | SELECT LENGTH('00101000')
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1bf76b579fe422abc285bf22bba728d~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="397822e1"></span>
## MD5

The MD5 function computes the MD5 hash value for a binary string.

<span id="d436b00c"></span>
### Function **syntax**


* Syntax format

   ```SQL
   MD5(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varbinary type. |
   

* Return value description

   The return value is of the Varbinary type.


<span id="e5662f0c"></span>
### Example


* Scenario

   Compute the MD5 hash value for the binary string 1101.

* Query and analysis statement

   ```SQL
   * | SELECT MD5(FROM_BASE64('1101')) AS MD5
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1dcf6a9bdaa14b49b82081dfd6f0d8cc~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="f954b4a7"></span>
## TO_BASE64

The TO_BASE64 function converts a binary string to a Base64\-encoded string.

<span id="bb6e0a0c"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_BASE64(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Binary type. |
   

* Return value description

   The return value is of the Varchar type.


<span id="df0789ae"></span>
### Example


* Scenario

   Convert the binary string 10 to a Base64\-encoded string.

* Query and analysis statement

   ```SQL
   * | SELECT  TO_BASE64(FROM_BASE64('10')) AS base64
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20d100f887154c5aa31665f566ab6483~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="f38b2630"></span>
## TO_BASE64URL

The TO_BASE64URL function converts a binary string to a Base64\-encoded string using URL\-safe characters.

<span id="4836c1ff"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_BASE64URL(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Binary type. |
   

* Return value description

   The return value is of the Varchar type.


<span id="e61971eb"></span>
### Example


* Scenario

   Convert the binary string 100 to a Base64\-encoded string using URL\-safe characters.

* Query and analysis statement

   ```SQL
   * | SELECT  TO_BASE64URL(FROM_BASE64('100'))
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b2bceab17684b19aa1e70723ce36b9a~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="373f8ac7"></span>
## TO_HEX

The TO_HEX function converts a binary string to a hexadecimal string.

<span id="0ff893e0"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_HEX(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Binary type. |
   

* Return value description

   The return value is of the Varchar type.


<span id="ec85b413"></span>
### Example


* Scenario

   Convert the binary string 100 to a hexadecimal string.

* Query and analysis statement

   ```SQL
   * | SELECT TO_HEX(FROM_BASE64('100'))
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f90eb4b873124c2baca5e87eb5af8da2~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="d6a74a78"></span>
## SHA1

The SHA1 function computes the SHA\-1 hash value for a binary string.

<span id="f8df07f3"></span>
### Function **syntax**


* Syntax format

   ```SQL
   SHA1(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Binary type. |
   

* Return value description

   The return value is of the Varbinary type.


<span id="0d341647"></span>
### Example


* Scenario

   Compute the SHA\-1 hash value for the binary string 1101.

* Query and analysis statement

   ```SQL
   * | SELECT SHA1(FROM_BASE64('1101')) AS SHA1
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2da5873a3a174a95942620dfcca124d0~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="117bfc9b"></span>
## SHA256

The SHA256 function computes the SHA\-256 hash value for a binary string.

<span id="38ced23e"></span>
### Function **syntax**


* Syntax format

   ```SQL
   SHA256(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Binary type. |
   

* Return value description

   The return value is of the Varbinary type.


<span id="c2205e26"></span>
### Example


* Scenario

   Compute the SHA\-256 hash value for the binary string 1101.

* Query and analysis statement

   ```SQL
   * | SELECT SHA256(FROM_BASE64('1101')) AS SHA256
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be98a9ea9f994cb0a891564ca444bb34~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="97947b9f"></span>
## SHA512

The SHA512 function computes the SHA\-512 hash value for a binary string.

<span id="88df73f6"></span>
### Function **syntax**


* Syntax format

   ```SQL
   SHA512(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Binary type. |
   

* Return value description

   The return value is of the Varbinary type.


<span id="31e699e6"></span>
### Example


* Scenario

   Compute the SHA\-512 hash value for the binary string 1101.

* Query and analysis statement

   ```SQL
   * | SELECT SHA512(FROM_BASE64('1101')) AS SHA512
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9beb753dcc334a56aeeea36ac5a1ce74~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="7367a063"></span>
## XXHASH64

The XXHASH64 function is used to compute the XXHASH64 hash value for a binary string.

<span id="061d7187"></span>
### Function **syntax**


* Syntax format

   ```SQL
   XXHASH64(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the binary type. |
   

* Return value description

   The return value is of the varbinary type.


<span id="80f8d590"></span>
### Example


* Scenario

   Compute the XXHASH64 hash value for a binary string 1101.

* Query and analysis statement

   ```SQL
   * | SELECT XXHASH64(FROM_BASE64('1101')) AS XXHASH64
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38b8cfc751b24a65b513bd7abc0453ee~tplv-goo7wpa0wc-image.image) </span>

---
title: "String functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/String-functions-2"
---

This topic describes the syntax of string functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="e65a23d6"></span>
## List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>



|Function |Function Syntax |Description |
|---|---|---|
|CHR |CHR(KEY) |This function converts an ASCII code to ASCII characters. |
|CODEPOINT |CODEPOINT (KEY) |This function converts ASCII characters to an ASCII code. |
|CONCAT |CONCAT(KEY1, KEY2...) |This function concatenates multiple strings into one string. |
|FROM_UTF8 |FROM_UTF8(KEY) |This function decodes a binary string into a UTF\-8 encoded string. Invalid UTF\-8 sequences are replaced with the default replacement character U+FFFD. |
||FROM_UTF8(KEY, replace_string) |This function decodes a binary string into a UTF\-8 encoded string. Invalid UTF\-8 sequences are replaced with a custom string. |
|LENGTH |LENGTH(KEY) |This function returns the length of a string. |
|LEVENSHTEIN_DISTANCE |LEVENSHTEIN_DISTANCE(KEY1, KEY2) |This function returns the minimum edit distance between two strings. |
|LOWER |LOWER(KEY) |This function converts the characters in a string to lowercase letters. |
|LPAD |LPAD(KEY, length, lpad_string) |This function pads the beginning of a specified string with characters until it reaches a specified length, and then returns the resulting string. |
|LTRIM |LTRIM(KEY) |This function removes spaces from the beginning of a string. |
|NORMALIZE |NORMALIZE(KEY) |This function transforms a string using normalization form C (NFC). |
|POSITION |POSITION(sub_string in KEY) |This function returns the position of a specified substring in a string. |
|REPLACE |REPLACE(KEY, sub_string ) |This function removes a specified substring. |
||REPLACE (KEY, sub_string, replace_string) |This function replaces a specified substring with another string. |
|REVERSE |REVERSE(KEY) |This function returns a string in reverse order. |
|RTRIM |RTRIM(KEY) |This function removes spaces from the end of a string. |
|SPLIT |SPLIT(KEY, delimeter) |This function splits a string using a specified delimiter and returns a set of substrings. |
||SPLIT(KEY, delimeter, limit) |This function splits a string using a specified delimiter and returns a set of substrings. The number of substrings that can be generated is specified by limit. |
|SPLIT_PART |SPLIT_PART(KEY,delimeter,index) |This function splits a string using a specified delimiter and returns the substring at the position specified by index. |
|SPLIT_TO_MAP |SPLIT_TO_MAP(KEY, delimiter01, delimiter02) |This function splits a string using a specified first delimiter and then splits the resulting substrings using a specified second delimiter to key\-value pairs. |
|STRPOS |STRPOS(KEY, sub_string) |This function is used to find the position of the first occurrence of a substring within a specified string. The position count starts at 1. If the substring is not found in the specified string, the function returns 0. |
|SUBSTR |SUBSTR(KEY, start) |This function returns the substring at a specified position in a string. |
||SUBSTR(KEY, start, length) |This function returns the substring at a specified position in a string. The length of the substring is specified. |
|TO_UTF8 |TO_UTF8(KEY) |This function converts a string to a UTF\-8 representation. |
|TRIM |TRIM(KEY) |This function removes spaces from the beginning and end of a string. |
|UPPER |UPPER(KEY) |This function converts the characters in a string to uppercase letters. |


<span id="CHR"></span>
## CHR

The CHR function converts an ASCII code to an ASCII character.

<span id="1be553ad"></span>
### Function **syntax**


* Syntax format

   ```SQL
   CHR(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an ASCII code. |
   

* Return value description

   The return value is of the Varchar type.


<span id="64a19190"></span>
### Example


* Scenario

   The statement is used to verify whether the values of the `url_test` field start with ASCII code 104, which is represented by lowercase letter h. Then, it is used to group the results.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56df6c5a6d794a7a8f21304bde4a46b3~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT SUBSTR(url_test, 1, 1)=CHR(104), COUNT(1) GROUP BY 1
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62a224c1db39473eb89a9611faa93a0d~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="41f9e73f"></span>
## CODEPOINT

The CODEPOINT function converts an ASCII character to an ASCII code.

<span id="a99e8f69"></span>
### Function **syntax**


* Syntax format

   ```SQL
   CODEPOINT(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an ASCII character. |
   

* Return value description

   An ASCII code is returned. The return value is of the Integer data type.


<span id="5cd8d003"></span>
### Example


* Scenario

   The statement is used to verify whether the values of the `url_test` field start with lowercase letter h, which is represented by ASCII code 104. Then, the statement is used to group the results.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5adea3100e3d433b814461ce93b44752~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT CODEPOINT(CAST (SUBSTR(url_test, 1, 1) AS CHAR(1))) =104, COUNT(1) GROUP BY 1
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d01466ff7bf94b5dadc15d7c237a1805~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="cf3f23fe"></span>
## CONCAT

The CONCAT function concatenates multiple strings into one string.

<span id="250d018b"></span>
### Function **syntax**


* Syntax format

   ```SQL
   CONCAT(KEY1, KEY2...)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Varchar type.


<span id="ab22aa83"></span>
### Example


* Scenario

   The function is used to concatenate the values of the `timestamp_str` and `url_test` fields into one string.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef95240eebbc465fb8fd3e0a95b857dc~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT CONCAT(timestamp_str,'-',url_test)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d04f8150b0f5486a829cd19763b5e404~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="0f515fc0"></span>
## FROM_UTF8

The FROM_UTF8 function decodes a binary string into a UTF\-8 encoded string.

<span id="4e1ce518"></span>
### Function **syntax**


* Syntax format

   * If invalid UTF\-8 sequences are returned, this format replaces them with the default replacement character U+FFFD.

      ```SQL
      from_utf8(string)
      ```
      

   * If invalid UTF\-8 sequences are returned, this format replaces them with custom strings.

      ```SQL
      from_utf8(string,replace_string)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |string |Data type: Binary. |
   |replace_string |The string to replace invalid sequences. The string can be a single character or space. |
   

* Return value description

   The return value is of the Varchar type.


<span id="1ac80746"></span>
### Example


* Scenario

   The statement is used to decode `0x40` into a UTF\-8 encoded string and replace invalid UTF\-8 sequences in the result with the default replacement character U+FFFD. U+FFFD is displayed as �.

* Query and analysis statement

   ```SQL
   * | SELECT FROM_UTF8(FROM_BASE64('0x40'))
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7f5a9a8cdd743e987ba582110f69f1f~tplv-goo7wpa0wc-image.image) </span>


<span id="b5e9d10b"></span>
## LENGTH

The LENGTH function calculates the length of a string.

<span id="f55babd0"></span>
### Function **syntax**


* Syntax format

   ```SQL
   LENGTH(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Bigint type.


<span id="b84dcbbc"></span>
### Example


* Scenario

   The statement is used to calculate the length of the values of the `url_test` field. Then, it is used to group the results.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5341a08f638944779cf2904716842a24~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT LENGTH(url_test),COUNT(1) GROUP BY 1
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c1f3d6cf194419496a6fa393b1c19c6~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="0eb902a7"></span>
## LEVENSHTEIN_DISTANCE

LEVENSHTEIN_DISTANCE function returns the minimum edit distance between two strings.

<span id="ccf6b22c"></span>
### Function syntax


* Syntax format

   ```SQL
   LEVENSHTEIN_DISTANCE(KEY1, KEY2)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Bigint type.


<span id="7de4554a"></span>
### Example


* Scenario

   Query the minimum edit distance between the value of the `Action` field and the value of the `Method` field.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1450a0a324c4225a6a530d44d202149~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT LEVENSHTEIN_DISTANCE(Action, Method)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfa5c02e45364bf48e34514398951205~tplv-goo7wpa0wc-image.image) </span>


<span id="858998dc"></span>
## LOWER

The LOWER function converts the characters in a string to lowercase letters.

<span id="260e6f3e"></span>
### Function **syntax**


* Syntax format

   ```SQL
   LOWER(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Varchar type.


<span id="c90c4c0b"></span>
### Example


* Scenario

   The statement is used to convert the values of the `up_eng_string` field to lowercase letters. Then, it is used to group the results.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9b65dac634b471aa99e2c758faf7492~tplv-goo7wpa0wc-image.image" width="1284px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT LOWER(up_eng_string), COUNT(1) GROUP BY 1
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82f268ce4ab84ebeb136d82cc84e94b2~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="7a7f46ce"></span>
## LPAD

The LPAD function is used to pad the beginning of a specified string with characters until it reaches a specified length, and then returns the resulting string.

<span id="bffdc304"></span>
### Function syntax


* Syntax format

   ```SQL
   LPAD(KEY, length, lpad_string)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   |length |The length of the result string.<br><br><br>* If the length of a string is less than the value of the **length** parameter, the string is padded by using the specified character from the start of the string.<br><br>* If the length of a string is greater than the value of the **length** parameter, only the **length** characters in the string are returned. |
   |lpad_string |The character that you want to use to pad a string. |
   

* Return value description

   The return value is of the Varchar type.


<span id="3684c230"></span>
### Example


* Scenario

   To pad the beginning of the `Method` field value with the string `abc` until the total length is 8 characters.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e13db73da76447c9967989f3a8878fa5~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT LPAD(Method,8,'abc')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b764374d6724424d9b5248e9f3bc17bf~tplv-goo7wpa0wc-image.image) </span>


<span id="1862eab5"></span>
## LTRIM

The LTRIM function removes spaces from the start of a string.

<span id="29efdc65"></span>
### Function **syntax**


* Syntax format

   ```SQL
   LTRIM(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Varchar type.


<span id="933809de"></span>
### Example


* Scenario

   The statement is used to remove spaces from the start of the values of the `fixed_10_bit_string_has_space` field.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7704bf171474bd5963327206f478c3b~tplv-goo7wpa0wc-image.image" width="1284px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT LTRIM(fixed_10_bit_string_has_space)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c8fe3484eda4f6980f4c280d27626a1~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="26906113"></span>
## NORMALIZE

The NORMALIZE function formats a string using NFC.

<span id="8063cbc2"></span>
### Function **syntax**


* Syntax format

   ```SQL
   NORMALIZE(string)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |string |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Varchar type.


<span id="fc1612f7"></span>
### Example


* Scenario

   The statement is used to format the value of the `Method` field using NFC.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e460f7f018744831be76171fe63cc44f~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT NORMALIZE(Method)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa267aaaddc7477d9f6bf10a80529e1c~tplv-goo7wpa0wc-image.image) </span>


<span id="4883dc10"></span>
## POSITION

The POSITION function returns the position of a specified substring in a string.

<span id="a7f669e2"></span>
### Function **syntax**


* Syntax format

   ```SQL
   POSITION(sub_string in KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |sub_string |The substring whose position you want to query. |
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   Data type: Int. Valid values start from 1. If the field values do not contain the specified substring, 0 is returned.


<span id="0dec9955"></span>
### Example


* Scenario

   The statement is used to query the positions of the `age` substring in the values of the `url_test` field. Then, the statement is used to group the results.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9b30ea552d940e29cc8622ed276acaf~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT POSITION('age' in url_test),count(1) group by 1
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2cf348288f6843ef892b01d8eb1f437d~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="df748f40"></span>
## REPLACE

The REPLACE function removes a specified substring or replaces a specified substring with another string.

<span id="aed9b641"></span>
### Function **syntax**


* Syntax format

   * Removes a specified substring.

      ```SQL
      REPLACE(KEY, sub_string)
      ```
      

   * Replaces a specified substring with another string.

      ```SQL
      REPLACE(KEY, sub_string, replace_string)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   |sub_string |The target substring. |
   |replace_string |The string to replace invalid sequences. |
   

* Return value description

   The return value is of the Varchar type.


<span id="ed43299d"></span>
### Example


* Example 1

   * Scenario

      The statement is used to replace `xxx` in the values of the `url_test` field with `regan`.

   * Sample log

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6b1ae1618894c65bc3e9d81a60c32d1~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

   * Query and analysis statement

      ```SQL
      * | SELECT REPLACE(url_test,'xxx','regan')
      ```
      

   * Query and analysis results

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0a0c41a194141f5a79aa0c8ab3a7b1b~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

* Example 2

   * Scenario

      The statement is used to remove `age=18&` from the values of the `url_test` field.

   * Sample log

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b30f91b7c1d4630bf33c32296889ca0~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

   * Query and analysis statement

      ```SQL
      * | SELECT REPLACE(url_test,'age=18&')
      ```
      

   * Query and analysis results

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f7f413ccbf1415fb334f49ec160cd66~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      


<span id="e0404357"></span>
## REVERSE

The REVERSE function returns a string in reverse order.

<span id="346e479f"></span>
### Function **syntax**


* Syntax format

   ```SQL
   REVERSE(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Varchar type.


<span id="fb44a37a"></span>
### Example


* Scenario

   The statement is used to reverse the values of the `url_test` field.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de5f4963905e4c26987833f39009beec~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT REVERSE(url_test)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/715098fb254546049c39dcbff8819e4e~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="581942f1"></span>
## RPAD

RPAD function is used to pad the right side of a string with a specified character, up to a specified length.

<span id="d118dd62"></span>
### Function syntax


* Syntax format

   ```SQL
   RPAD(KEY, length, rpad_string)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   |length |The length of the result string.<br><br><br>* If the length of a string is less than the value of the **length** parameter, the string is padded by using the specified character from the end of the string.<br><br>* If the length of a string is greater than the value of the **length** parameter, only the `length` characters in the string are returned. |
   |rpad_string |The character that you want to use to pad a string. |
   

* Return value description

   The return value is of the Varchar type.


<span id="d5a3f8e0"></span>
### Example


* Scenario

   Pad the `Method` field values with the string `abc` at the end until the total length is 8 characters.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee6c87f3b84749f19b5b241b37a469db~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT RPAD(Method,8,'abc')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5128da14dee246d6a146b9561df36474~tplv-goo7wpa0wc-image.image) </span>


<span id="c3595ea0"></span>
## RTRIM

The RTRIM function removes spaces from the end of a string.

<span id="9d650ecf"></span>
### Function **syntax**


* Syntax format

   ```SQL
   RTRIM(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Varchar type.


<span id="638ac2e3"></span>
### Example


* Scenario

   The statement is used to remove spaces from the end of the values of the `fixed_10_bit_string_has_space` field.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47c8e21aa6284ce29aef046c76503e08~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT RTRIM(fixed_10_bit_string_has_space)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f44060c4e844b5ca9c7465685280a86~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="0be92238"></span>
## SPLIT

The SPLIT function splits a string using a specified delimiter and returns a set of substrings.

<span id="65733676"></span>
### Function **syntax**


* Syntax format

   * This format splits a string using a specified delimiter and returns a set of substrings.

      ```SQL
      SPLIT(KEY, delimeter)
      ```
      

   * This syntax splits a string using a specified delimiter and returns a set of substrings. The number of substrings that can be generated is specified by limit.

      ```SQL
      SPLIT(KEY,delimeter,limit)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   |delimeter |The delimiter. |
   |limit |The number of substrings that can be generated. Specify a positive integer. |
   

* Return value description

   The return value is of the Array type.


<span id="d77c968c"></span>
### Example


* Example 1

   * Scenario

      The statement uses a period ( . ) to split the values of the `__source__` field into multiple substrings and gets a set of the substrings.

   * Sample log

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f36452cc58c45b4a5276cbdf12c025b~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

   * Query and analysis statement

      ```SQL
      * | SELECT SPLIT(__source__,'.') 
      ```
      

   * Query and analysis results

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f5526c0f9e54707a6a12ab6c3b12e95~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

* Example 2

   * Scenario

      The statement uses a period ( . ) to split the values of the `__source__` field into three substrings and gets a set of the substrings.

   * Sample log

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8076ccabbffd4227972001b64f5a6faf~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

   * Query and analysis statement

      ```SQL
      * | SELECT SPLIT(__source__,'.', 3)
      ```
      

   * Query and analysis results

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be9322c8764648398db134b914d7570b~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      


<span id="cffb3fda"></span>
## SPLIT_PART

The SPLIT_PART function splits a string using a specified delimiter and returns the substring at the position specified by index.

<span id="b8e5a863"></span>
### Function **syntax**


* Syntax format

   ```SQL
   SPLIT_PART(KEY,delimeter,index)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |*x* |A field or an expression. The value is of the Varchar type. |
   |delimeter |The delimiter. |
   |index |A positive integer. |
   

* Return value description

   The return value is of the Varchar type.


<span id="8346137c"></span>
### Example


* Scenario

   The statement uses a period ( . ) to split the values of the `__source__` field into multiple substrings and returns the substring at position 2.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c3a898b44914dc88d52629c75328b2d~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT SPLIT_PART(__source__,'.', 2) 
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61a23c62ff73470896cc826111ca6f54~tplv-goo7wpa0wc-image.image) </span>


<span id="4c7efae9"></span>
## SPLIT_TO_MAP

The `SPLIT_TO_MAP` function splits a string using a specified first delimiter and then splits the resulting substrings using a specified second delimiter to key\-value pairs.

<span id="03e54a01"></span>
### Function syntax


* Syntax format

   ```SQL
   SPLIT_TO_MAP(KEY, delimiter01, delimiter02)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   |delimeter |The delimiter that you want to use. |
   

* Return value description

   The return value is of the Map type.


<span id="8bb809c4"></span>
### Example


* Scenario

   To split the values of `URL` field into multiple substrings using a half\-width question mark (`?`) and an underscore (`_`).

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7781ff2386b64c1a998d38c151a8bdd8~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT SPLIT_TO_MAP(URL, '?', '_')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/709d5a380b264c5492f131389efe11b5~tplv-goo7wpa0wc-image.image) </span>


<span id="275fc241"></span>
## STRPOS

The STRPOS function is used to find the position of the first occurrence of a substring within a specified string. The position count starts at 1. If the substring is not found in the specified string, the function returns 0.

<span id="2675371e"></span>
### Function syntax


* Syntax format

   ```SQL
   STRPOS(KEY, sub_string)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   |sub_string |The substring whose position you want to query. |
   

* Return value description

   The return value is of the Int type.


<span id="c6cdd3b2"></span>
### Example


* Scenario

   Find the position of the substring "OS" in the `Method` field.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82a15de4513244dcb146cd7c90a7f7f7~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT STRPOS(Method, 'OS')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3dd0eec14cd941fd8bf860b683f825d5~tplv-goo7wpa0wc-image.image) </span>


<span id="eaa0aac3"></span>
## SUBSTR

SUBSTR function returns the substring at a specified position in a string.

<span id="a73df316"></span>
### Function syntax


* Syntax format

   * Returns the substring at a specified position in a string.

      ```SQL
      SUBSTR(KEY, start)
      ```
      

   * Returns the substring at a specified position in a string. The length of the substring is specified.

      ```SQL
      SUBSTR(KEY, start, length)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   |start |The start position from which you want to extract a substring. Valid values start from 1. |
   |length |The length of the substring. |
   

* Return value description

   The return value is of the Varchar type.


<span id="7c54c8d9"></span>
### Example


* Example 1

   * Scenario

      Extract the substring from the `Method` field starting from position 2.

   * Sample log

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82a15de4513244dcb146cd7c90a7f7f7~tplv-goo7wpa0wc-image.image) </span>

   * Query and analysis statement

      ```SQL
      * | SELECT SUBSTR(Method, 2)
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/faec2a17849049368e48ed60e461fcb4~tplv-goo7wpa0wc-image.image) </span>

* Example 2

   * Scenario

      Extract a substring from the `Method` field starting at position 2 with a length of 2 characters.

   * Sample log

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82a15de4513244dcb146cd7c90a7f7f7~tplv-goo7wpa0wc-image.image) </span>

   * Query and analysis statement

      ```SQL
      * | SELECT SUBSTR(Method, 2, 2)
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71a55086302c48dab58e8b2cd118b476~tplv-goo7wpa0wc-image.image) </span>


<span id="fcdccfab"></span>
## TO_UTF8

The TO_UTF8 function converts a string to a UTF\-8 representation.

<span id="2637beb6"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_UTF8(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Varbinary type.


<span id="b360fe6e"></span>
### Example


* Scenario

   The statement is used to convert the `log` string to a UTF\-8 representation.

* Query and analysis statement

   ```SQL
   * | SELECT TO_UTF8('log')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/844c6ed26f07492f9719de1b93f071b3~tplv-goo7wpa0wc-image.image) </span>


<span id="44061cb7"></span>
## TRIM

The TRIM function removes spaces from the start and end of a string.

<span id="df0cb2f2"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TRIM(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Varchar type.


<span id="ac1375ee"></span>
### Example


* Scenario

   The statement is used to remove spaces from the start and end of the values of the `fixed_10_bit_string_has_space` field.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6c9a3d2b5a34b29aad26eef85ac6d0f~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT TRIM(fixed_10_bit_string_has_space)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bbb47eaa1c54413b9743ecd864e5051c~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="ee16b43b"></span>
## UPPER

The UPPER function converts the characters in a string to uppercase letters.

<span id="db68d238"></span>
### Function **syntax**


* Syntax format

   ```SQL
   UPPER(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Varchar type.


<span id="0a1d5b85"></span>
### Example


* Scenario

   The statement is used to convert the values of the `url_test` field to uppercase letters.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1e7cf3fe1a64795a27bf3468e1656c3~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT upper(url_test)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cebcdf0e04f744c09c390b3c13e109b5~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>

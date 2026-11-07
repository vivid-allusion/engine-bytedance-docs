---
title: "Unit conversion functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Unit-conversion-functions"
---

This topic describes the syntax of unit conversion functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="74589eeb"></span>
## List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>



|Category |Function |Syntax |Description |
|---|---|---|---|
|Measurement unit conversion |CONVERT_DATA_SIZE |CONVERT_DATA_SIZE(KEY) |Converts a measurement from the current unit to the optimal unit determined by the system. |
|||CONVERT_DATA_SIZE(KEY, unit) |Converts a measurement from the current unit to a specified unit. |
||FORMAT_DATA_SIZE |FORMAT_DATA_SIZE(KEY, unit) |Converts a measurement in bytes to a measurement in a specified unit. |
||PARSE_DATA_SIZE |PARSE_DATA_SIZE(KEY) |Converts a measurement from the current unit to a measurement in bytes. |
||TO_DATA_SIZE_B |TO_DATA_SIZE_B(KEY) |Converts a measurement from the current unit to a measurement in bytes. The return value is of the Double type. |
||TO_DATA_SIZE_KB |TO_DATA_SIZE_KB(KEY) |Converts a measurement from the current unit to a measurement in KB. |
||TO_DATA_SIZE_MB |TO_DATA_SIZE_MB(KEY) |Converts a measurement from the current unit to a measurement in MB. |
||TO_DATA_SIZE_GB |TO_DATA_SIZE_GB(KEY) |Converts a measurement from the current unit to a measurement in GB. |
||TO_DATA_SIZE_TB |TO_DATA_SIZE_TB(KEY) |Converts a measurement from the current unit to a measurement in TB. |
||TO_DATA_SIZE_PB |TO_DATA_SIZE_PB(KEY) |Converts a measurement from the current unit to a measurement in PB. |
|Time interval unit conversion |FORMAT_DURATION |FORMAT_DURATION(KEY) |Converts a time interval in seconds to a time interval in`xx weeks, xx days, xx hours, xx minutes, xx seconds` format. |
||PARSE_DURATION |PARSE_DURATION(KEY) |Converts a time interval to a time interval in `0 00:00:00.000` format. |
||TO_DAYS |TO_DAYS(KEY) |Converts a time interval to a time interval in days. |
||TO_MILLISECONDS |TO_MILLISECONDS(KEY) |Converts a time interval to a time interval in milliseconds. |
||TO_MINUTES |TO_MINUTES(KEY) |Converts a time interval to a time interval in minutes. |
||TO_MOST_SUCCINCT_TIME_UNIT |TO_MOST_SUCCINCT_TIME_UNIT(KEY) |Converts a time interval from the current unit to the optimal unit determined by the system. |
||TO_SECONDS |TO_SECONDS(KEY) |Converts a time interval to a time interval in seconds. |
||TO_NANOSECONDS |TO_NANOSECONDS(KEY) |Converts a time interval to a time interval in nanoseconds. |
||TO_MICROSECONDS |TO_MICROSECONDS(KEY) |Converts a time interval to a time interval in microseconds. |
||TO_HOURS |TO_HOURS(KEY) |Converts a time interval to a time interval in hours. |


<span id="56222144"></span>
## CONVERT_DATA_SIZE

The CONVERT_DATA_SIZE function converts a measurement from the current unit to another unit.

<span id="460c2632"></span>
### Function **syntax**


* Syntax format

   * Converts a measurement from the current unit to the optimal unit determined by the system.

      ```SQL
      CONVERT_DATA_SIZE(KEY)
      ```
      

   * Converts a measurement from the current unit to a specified unit.

      ```SQL
      CONVERT_DATA_SIZE(KEY, unit)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the String type. |
   |unit |The unit of stored data. Valid values: KB, MB, GB, PB, TB, EB, ZB, and YB. |
   

* Return value description

   The return value is of the String type.


<span id="ecb125d5"></span>
### Example


* Example 1

   * Scenario

      Convert 100,000 KB to a measurement in the optimal unit determined by the system.

   * Query and analysis statement

      ```SQL
      * | SELECT CONVERT_DATA_SIZE('100000KB')
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/202203987aff4331954a8885f5acd6d2~tplv-goo7wpa0wc-image.image) </span>

* Example 2

   * Scenario

      Convert 100,000 KB to a measurement in GB.

   * Query and analysis statement

      ```SQL
      * | SELECT CONVERT_DATA_SIZE('100000KB', 'GB')
      ```
      

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa0605b5feb247bb97e9b5e6cf8d988d~tplv-goo7wpa0wc-image.image" width="1277px" />   </div>
   


<span id="ea36ec73"></span>
## FORMAT_DATA_SIZE

The FORMAT_DATA_SIZE function converts a measurement in bytes to a measurement in a specified unit.

<span id="30f1ffe4"></span>
### Function **syntax**


* Syntax format

   ```SQL
   FORMAT_DATA_SIZE(KEY, unit)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A log field or an expression. The value is of the Bigint type in bytes. |
   |*unit* |The unit of stored data. Valid values: KB, MB, GB, PB, TB, EB, ZB, and YB. |
   

* Return value description

   The return value is of the String type.


<span id="2c1379b1"></span>
### Example


* Scenario

   Use the FORMAT_DATA_SIZE function to convert the value of the `ReqSize` field in bytes to a measurement in KB.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73ab1c68e5014b52bb9e1d260a8e1167~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT FORMAT_DATA_SIZE(4096, 'KB')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f3556ddce934bd0ad5395396146b962~tplv-goo7wpa0wc-image.image) </span>


<span id="0ae87aaf"></span>
## PARSE_DATA_SIZE

The PARSE_DATA_SIZE function converts the current measurement to a measurement in bytes.

<span id="567a20f3"></span>
### Function **syntax**


* Syntax format

   ```SQL
   PARSE_DATA_SIZE(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the String type. |
   

* Return value description

   The return value is of the Decimal type.


<span id="f02e7cb8"></span>
### Example


* Scenario

   Convert 1 KB to a measurement in bytes.

* Query and analysis statement

   ```SQL
   *| SELECT PARSE_DATA_SIZE('1KB')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84dba0dbd1a543a783c29027dfcd39a2~tplv-goo7wpa0wc-image.image) </span>


<span id="47db5aa3"></span>
## TO_DATA_SIZE_B

The TO_DATA_SIZE_B function converts the current measurement to a measurement in bytes.

<span id="3af376a6"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_DATA_SIZE_B(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the String type. |
   

* Return value description

   The return value is of the Double type.


<span id="901fe46a"></span>
### Example


* Scenario

   Convert 1 KB to a measurement in bytes.

* Query and analysis statement

   ```SQL
   * | SELECT TO_DATA_SIZE_B('1KB')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84dba0dbd1a543a783c29027dfcd39a2~tplv-goo7wpa0wc-image.image) </span>


<span id="64f7ff2f"></span>
## TO_DATA_SIZE_KB

The TO_DATA_SIZE_KB function converts the current measurement to a measurement in KB.

<span id="88f13628"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_DATA_SIZE_KB(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the String type. |
   

* Return value description

   The return value is of the Double type.


<span id="0208426e"></span>
### Example


* Scenario

   Convert 2,048 MB to a measurement in KB.

* Query and analysis statement

   ```SQL
   * | SELECT TO_DATA_SIZE_KB('2048MB')
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47fd7e396d354066912372bc517087e3~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="a2fec5be"></span>
## TO_DATA_SIZE_MB

The TO_DATA_SIZE_MB function converts the current measurement to a measurement in MB.

<span id="bb836c31"></span>
### **Syntax**


* Syntax format

   ```SQL
   TO_DATA_SIZE_MB(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the String type. |
   

* Return value description

   The return value is of the Double type.


<span id="08ea5de4"></span>
### Example


* Scenario

   Convert 1,024 GB to a measurement in MB.

* Query and analysis statement

   ```SQL
   * | SELECT TO_DATA_SIZE_MB('1024GB')
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b789d69216441cf85679d1f253a7962~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="1cb66614"></span>
## TO_DATA_SIZE_GB

The TO_DATA_SIZE_GB function converts the current measurement to a measurement in GB.

<span id="1dff38ea"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_DATA_SIZE_GB(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the String type. |
   

* Return value description

   The return value is of the Double type.


<span id="a1481ded"></span>
### Example


* Scenario

   Convert 1,024 TB to a measurement in GB.

* Query and analysis statement

   ```SQL
   * | SELECT TO_DATA_SIZE_GB('1024TB')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11c42007bfc54fb68b11b22a9168ca2a~tplv-goo7wpa0wc-image.image) </span>


<span id="f15cce63"></span>
## TO_DATA_SIZE_TB

The TO_DATA_SIZE_TB function converts the current measurement to a measurement in TB.

<span id="0af18c6e"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_DATA_SIZE_TB(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the String type. |
   

* Return value description

   The return value is of the Double type.


<span id="6053ced6"></span>
### Example


* Scenario

   Convert 1,024 PB to a measurement in TB.

* Query and analysis statement

   ```SQL
   * | SELECT TO_DATA_SIZE_TB('1024PB')
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2f608484be64411a6ab8d848ea18b70~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="30465b7b"></span>
## TO_DATA_SIZE_PB

The TO_DATA_SIZE_PB function converts the current measurement to a measurement in PB.

<span id="24e6a6b4"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_DATA_SIZE_PB(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the String type. |
   

* Return value description

   The return value is of the Double type.


<span id="5e23127f"></span>
### Example


* Scenario

   Convert 1,048,576 TB to a measurement in PB.

* Query and analysis statement

   ```SQL
   * | SELECT TO_DATA_SIZE_PB('1048576TB')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84dba0dbd1a543a783c29027dfcd39a2~tplv-goo7wpa0wc-image.image) </span>


<span id="de361d5a"></span>
## FORMAT_DURATION

The FORMAT_DURATION function converts a time interval in seconds to a time interval in `xx weeks, xx days, xx hours, xx minutes, xx seconds` format.

<span id="5f270ac7"></span>
### Function **syntax**


* Syntax format

   ```SQL
   FORMAT_DURATION(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Double type. |
   

* Return value description

   The return value is of the String type.


<span id="a2a660a2"></span>
### Example


* Scenario

   Format a time interval of 4,200,000 seconds.

* Query and analysis statement

   ```SQL
   * | SELECT FORMAT_DURATION(4200000)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c9a9482a34d41a89042429500bcded6~tplv-goo7wpa0wc-image.image) </span>


<span id="71c51cfd"></span>
## PARSE_DURATION

The PARSE_DURATION function converts a time interval to a time interval in `0 00:00:00.000` format.

<span id="6e2db47e"></span>
### Function **syntax**


* Syntax format

   ```SQL
   PARSE_DURATION(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the String type. |
   

* Return value description

   The return value is of the String type.


<span id="4683b811"></span>
### Example


* Scenario

   Convert 120,000 seconds to a time interval in `1 09:20:00.000` format.

* Query and analysis statement

   ```SQL
   * | SELECT PARSE_DURATION('120000s')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/324a326c339b4a089d589fcbf79ae998~tplv-goo7wpa0wc-image.image) </span>


<span id="0badcab4"></span>
## TO_DAYS

The TO_DAYS function converts a time interval to a time interval in days.

<span id="f169fe09"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_DAYS(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Double type.


<span id="09f4d7a3"></span>
### Example


* Scenario

   Convert 360,000 seconds to a time interval in days.

* Query and analysis statement

   ```SQL
   *| SELECT TO_DAYS('360000s')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9dc0539f4d5d4c4f9d90fe30cc77a7d1~tplv-goo7wpa0wc-image.image) </span>


<span id="e16fcd37"></span>
## TO_MILLISECONDS

The TO_MILLISECONDS function converts a time interval to a time interval in milliseconds.

<span id="86c9a4fc"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_MILLISECONDS(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Double type.


<span id="13a3677d"></span>
### Example


* Scenario

   Convert 10 seconds to a time interval in milliseconds.

* Query and analysis statement

   ```SQL
   * | SELECT TO_MILLISECONDS('10s')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/064a2071a15a437b9b5a5b1dbf4e74dd~tplv-goo7wpa0wc-image.image) </span>


<span id="6083fbca"></span>
## TO_MINUTES

The TO_MINUTES function converts a time interval to a time interval in minutes.

<span id="0bdbbe1c"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_MINUTES(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Double type.


Example


* Scenario

   Convert 10 hours to a time interval in minutes.

* Query and analysis statement

   ```SQL
   * | SELECT TO_MINUTES('10h')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a2967e2c0ae4374b95d05de22e267ff~tplv-goo7wpa0wc-image.image) </span>


<span id="7aebd3f9"></span>
## TO_MOST_SUCCINCT_TIME_UNIT

The TO_MOST_SUCCINCT_TIME_UNIT function converts a time interval from the current unit to the optimal unit determined by the system.

<span id="b73cdfe0"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_MOST_SUCCINCT_TIME_UNIT(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Varchar type.


<span id="475c2101"></span>
### Example


* Scenario

   Convert 1,340 milliseconds to a time interval in seconds.

* Query and analysis statement

   ```SQL
   * | SELECT TO_MOST_SUCCINCT_TIME_UNIT('1340ms')
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e9cf2cd6d554702820761875f7cb11d~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="0ce29143"></span>
## TO_SECONDS

The TO_SECONDS function converts a time interval to a time interval in seconds.

<span id="4b64add1"></span>
#### Function **syntax**


* Syntax format

   ```SQL
   TO_SECONDS(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Double type.


<span id="736ba94d"></span>
### Example


* Scenario

   Convert 1,340 milliseconds to a time interval in seconds.

* Query and analysis statement

   ```SQL
   * | SELECT TO_SECONDS('1340ms')
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84467ff80e9e44d1af0b4319565602ce~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="29ae1054"></span>
## TO_NANOSECONDS

The TO_NANOSECONDS function converts a time interval to a time interval in nanoseconds.

<span id="227b1e15"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_NANOSECONDS(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Double type.


<span id="b1643e0e"></span>
### Example


* Scenario

   Convert 125 milliseconds to a time interval in nanoseconds.

* Query and analysis statement

   ```SQL
   * | SELECT TO_NANOSECONDS('125ms')
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87a5f18676694205b2a84aed8d354e99~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="f23093ce"></span>
## TO_MICROSECONDS

The TO_MICROSECONDS function converts a time interval to a time interval in microseconds.

<span id="08ff990c"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_MICROSECONDS(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Double type.


<span id="ade904d1"></span>
### Example


* Scenario

   Convert 3,600 nanoseconds to a time interval in microseconds.

* Query and analysis statement

   ```SQL
   * | SELECT TO_MICROSECONDS('3600ns')
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7af6c1a48284a1ca92c02b51a21e6bb~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="f88ff4cc"></span>
## TO_HOURS

The TO_HOURS function converts a time interval to a time interval in hours.

<span id="fe695d40"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_HOURS(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Varchar type. |
   

* Return value description

   The return value is of the Double type.


<span id="a83879c6"></span>
### Example


* Scenario

   Convert 1.2 days to a time interval in hours.

* Query and analysis statement

   ```SQL
   * | SELECT TO_HOURS('1.2d')
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5a3afad77034db9b8d6980ee5c33c35~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>

---
title: "Approximate functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Approximate-functions-2"
---

This topic describes the syntax of approximate functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="b9260938"></span>
## List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>



|Function |Function Syntax |Description |
|---|---|---|
|APPROX_PERCENTILE |APPROX_PERCENTILE(KEY, percentage) |Sorts a set of values in ascending order and returns the KEY value that is approximately at the percentage position. |
||APPROX_PERCENTILE(KEY, array[percentage01, percentage02...]) |Sorts a set of values in ascending order and returns the KEY values that are approximately at the percentage01 and percentage02 positions. |
||APPROX_PERCENTILE(KEY, weight, percentage) |Sorts a set of values multiplied by a weight in ascending order and returns the KEY value that is approximately at the percentage position. |
||APPROX_PERCENTILE(KEY, weight, array[percentage01, percentage02...]) |Sorts a set of values multiplied by a weight in ascending order and returns the KEY values that are approximately at the percentage01 and percentage02 positions. |
||APPROX_PERCENTILE(KEY, weight, percentage, accuracy) |Sorts a set of values multiplied by a weight in ascending order and returns the value that is approximately at the percentage position. The accuracy can be specified. |


<span id="APPROX_PERCENTILE"></span>
## APPROX_PERCENTILE

The APPROX_PERCENTILE function sorts a set of values in ascending order and returns the KEY value that is approximately at the percentage position.

<span id="86313e32"></span>
### Function **syntax**


* Syntax format

   * Sorts a set of values in ascending order and returns the KEY value that is approximately at the specified percentage position.

      ```SQL
      APPROX_PERCENTILE(KEY, percentage)
      ```
      

   * Sorts a set of values in ascending order and returns the KEY values that are approximately at the percentage01 and percentage02 positions. The return value is of the Array type.

      ```SQL
      APPROX_PERCENTILE(KEY, array[percentage01, percentage02...])
      ```
      

   * Sorts a set of values multiplied by a weight in ascending order and returns the KEY value that is approximately at the specified percentage position.

      ```SQL
      APPROX_PERCENTILE(KEY, weight, percentage)
      ```
      

   * Sorts a set of values multiplied by a weight in ascending order and returns the KEY values that are approximately at the percentage01 and percentage02 positions. The return value is of the Array type.

      ```SQL
      APPROX_PERCENTILE(KEY, weight, array[percentage01, percentage02...])
      ```
      

   * Sorts a set of values multiplied by a weight in ascending order and returns the KEY value that is approximately at the percentage position. The return value is of the Double type. The accuracy can be specified.

      ```SQL
      APPROX_PERCENTILE(KEY, weight, percentage, accuracy)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Double type. |
   |percentage |The percentage. Value range: [0,1]. |
   |accuracy |The accuracy. Value range: (0,1). |
   |weight |The weight, which is an integer greater than 1.<br><br>After you set the weight, the system sorts the values based on the KEY value multiplied by the weight. |
   

* Return value description

   The return value is of the Double or Array(double) type.


<span id="9809a4cb"></span>
### Example


* Example 1

   * Scenario

      Sort the values of the `test_double` field, and return the value that is approximately at the 50% position in the `test_double` field.

   * Sample log

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca09114002bd4a5b84e1e5585cc1c50b~tplv-goo7wpa0wc-image.image) </span>

   * Query and analysis statement

      ```SQL
      *| SELECT APPROX_PERCENTILE(test_double,0.5)
      ```
      

   * Query and analysis results

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f75a22b6382441ecb831e618fc35d4ac~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

* Example 2

   * Scenario

      Sort the values of the `test_double` field, and return the values that are approximately at the 10%, 20%, and 70% positions in the `test_double` field.

   * Sample log

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ed403d7798c41378031a89070e5f94f~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

   * Query and analysis statement

      ```SQL
      *| SELECT APPROX_PERCENTILE(test_double,array[0.1,0.2,0.7])
      ```
      

   * Query and analysis results

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0fb55abaf8004b1db0a28ca3ee368911~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

* Example 3

   * Scenario

      Sort the values of the `test_double` field based on the `test_double` field values multiplied by the weight, and return the value that is approximately at the 50% position in the `test_double` field. If the value of the `test_double` field is less than 1.5, the weight is 100. Otherwise, the weight is 10.

   * Query and analysis statement

      ```SQL
      * |
      SELECT
        APPROX_PERCENTILE(
          test_double,case when test_double < 1.5 then 100 else 10 end,
          0.5
        )
      ```
      

   * Sample log

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bbcd1162428745dc881d4a79adad8c4c~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

   * Query and analysis results

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6b426fdef774eb1b934837b23be14b1~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

* Example 4

   * Scenario

      Sort the values of the `test_double` field based on the `test_double` field values multiplied by the weight, and return the values that are approximately at the 50% and 90% positions in the `test_double` field. If the value of the `test_double` field is less than 1.5, the weight is 100. Otherwise, the weight is 10.

   * Sample log

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfe77ffe9d524c408ae7dd257c4fff28~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

   * Query and analysis statement

      ```SQL
      * |
      SELECT
        APPROX_PERCENTILE(
          test_double,case when test_double < 1.5 then 100 else 10 end,
          array [0.5,0.9]
        )
      ```
      

   * Query and analysis results

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/780f02d21c9f47d99aae2c60be3a671b~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

* Example 5

   * Scenario

      Sort the values of the `test_double` field based on the `test_double` field values multiplied by the weight, and return the value that is approximately at the 50% position in the `test_double` field. The accuracy is 0.2. If the value of the `test_double` field is less than 1.5, the weight is 100. Otherwise, the weight is 10.

   * Sample log

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06170156e41045adba1fc33a3266d01d~tplv-goo7wpa0wc-image.image) </span>

   * Query and analysis statement

      ```SQL
      * |
      SELECT
        APPROX_PERCENTILE(
          test_double,case when test_double < 1.5 then 100 else 10 end,
          0.5,
          0.2
        )
      ```
      

   * Query and analysis results

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f008919cf8804d67b6e2074cc28cc76c~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      


&nbsp;

---
title: "Period-over-period comparison functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Period-over-period-comparison-functions"
---

This topic describes the syntax of period\-over\-period comparison functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="b3055f90"></span>
## List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>


* <div data-tips="true" data-tips-type="tip">When you use the COMPARE function, the time based on which data is compared must be the same. For example, you can use the COMPARE function to compare the data of the current hour with that of the same time period on the previous day. However, you cannot use the COMPARE function to compare the data of the current hour with that of the previous hour.</div>


* <div data-tips="true" data-tips-type="tip">The query and analysis results of the TS_COMPARE function must be grouped by the time column using the GROUP BY clause.</div>




|Function |Syntax |Description |
|---|---|---|
|COMPARE |COMPARE(KEY, n) |This function compares the calculation result of the current time period with the calculation result of a time period n seconds before. |
||COMPARE(KEY, n1, n2, n3...) |This function compares the calculation result of the current time period with the calculation results of time periods n1, n2, and n3 seconds before. |
|TS_COMPARE |TS_COMPARE(KEY, n) |This function compares the calculation result of the current time period with the calculation result of a time period n seconds before. |
||TS_COMPARE(KEY, n1, n2, n3...) |This function compares the calculation result of the current time period with the calculation results of time periods n1, n2, and n3 seconds before. |


<span id="COMPARE"></span>
## COMPARE

The COMPARE function compares the calculation result of the current time period with the calculation result of a time period n seconds before.

<span id="964b366f"></span>
### Function **syntax**


* Syntax format

   * Compares the calculation result of the current time period with the calculation result of a time period n seconds before.

      ```SQL
      COMPARE(KEY, n)
      ```
      

   * Compares the calculation result of the current time period with the calculation results of time periods n1, n2, and n3 seconds before.

      ```SQL
      COMPARE(KEY, n1, n2, n3...)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the Double or Long type. |
   |n |The time window. Unit: seconds. For example, 86400, which indicates 1 day. |
   

* Return value description

   The return value is of the Array type. Format: `[Calculation result of the current time period, Calculation result of a time period n seconds before, Ratio of the calculation result of the current time period to the calculation result of a time period n seconds before]`.


<span id="03bc5133"></span>
### Example


* Scenario

   Calculate the ratio of the orders of the current hour to the orders of the same time period on the previous day.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0263b0e19a5b4b08a1cf2b2e52e61e9f~tplv-goo7wpa0wc-image.image) </span>

* Results in array format

   * Query and analysis statement

      Set the time range to **Last 1 hour(On the hour)**  and execute the following query and analysis statement:

      ```SQL
      * |SELECT
        COMPARE(PV, 86400)
      FROM  (
          SELECT COUNT(*) AS PV
        )
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8dbb92333884482a915dd2133091f2f~tplv-goo7wpa0wc-image.image) </span>

      * **1631.0** indicates the number of orders in the current hour, for example, from 10:00:00 to 11:00:00 on September 27, 2023.

      * **1983.0** indicates the number of orders in the same time period on the previous day, for example, from 10:00:00 to 11:00:00 on September 26, 2023.

      * **0.8224911749873929** indicates the ratio of the orders of the current hour to the orders of the same time period on the previous day.

* Results in column format

   * Query and analysis statement

      Set the time range to **Last 1 hour(On the hour)**  and execute the following query and analysis statement. The result of the COMPARE function is an array. In the preceding query and analysis statement, **diff** specifies the alias for the result, and **diff [1]**  specifies the first value in the array.

      ```SQL
      * |SELECT
        diff [1] AS today,
        diff [2] AS yesterday,
        diff [3] AS ratio
      FROM  (
          SELECT
            COMPARE(PV, 86400) AS diff
          FROM 
          (
            SELECT COUNT(*) AS PV
           )
        )
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbb8d6d0b26c4d41a8fb4c65b1b4c841~tplv-goo7wpa0wc-image.image) </span>

      * **1757** indicates the number of orders in the current hour, for example, from 12:00:00 to 13:00:00 on September 27, 2023.

      * **1783** indicates the number of orders in the same time period on the previous day, for example, from 12:00:00 to 13:00:00 on September 26, 2023.

      * **0.9854178351093662** indicates the ratio of the orders of the current hour to the orders of the same time period on the previous day.


<span id="5ec61cfe"></span>
## TS_COMPARE

The TS_COMPARE function compares the calculation result of the current time period with the calculation result of a time period n seconds before.

<span id="20dae650"></span>
### **Function Syntax**


* Syntax format

   * Compares the calculation result of the current time period with the calculation result of a time period n seconds before.

      ```SQL
      TS_COMPARE(KEY, n)
      ```
      

   * Compares the calculation result of the current time period with the calculation results of time periods n1, n2, and n3 seconds before.

      ```SQL
      TS_COMPARE(KEY, n1, n2, n3...)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |A field or an expression. The value is of the Double or Long type. |
   |n |The time window. Unit: seconds. For example, 86400, which indicates 1 day. |
   

* Return value description

   The return value is of the Array type. Format: `[Calculation result of the current time period, Calculation result of a time period n seconds before, Ratio of the calculation result of the current time period to the calculation result of a time period n seconds before, UNIX timestamp of a time period n seconds before]`.


<span id="069bdc2f"></span>
### Example


* Scenario

   Calculate the ratio of the orders of every hour today to the orders of the same time period on the previous day and two days before.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c04bfa9bc8694b66b5caaec61e48a8e4~tplv-goo7wpa0wc-image.image) </span>

* Results in array format

   * Query and analysis statement

      Set the time range to **Today** and execute the following query and analysis statement:

      ```SQL
      *|SELECT 
        time,
        TS_COMPARE(PV, 86400, 172800) AS diff
      FROM  (
          SELECT 
              COUNT(*) AS PV,
              DATE_TRUNC('hour', __time__) AS time
          GROUP BY time
        )
      GROUP BY time ORDER BY time
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b6c645fc59e4c40bf7f723d69a2cf21~tplv-goo7wpa0wc-image.image) </span>

      * **375.0** indicates the number of orders in the current time period, for example, from 03:00 to 04:00 on September 26, 2023.

      * **347.0** indicates the number of orders in the same time period on the previous day, for example, from 03:00 to 04:00 on September 25, 2023.

      * **258.0** indicates the number of orders in the same time period two days before, for example, from 03:00 to 04:00 on September 24, 2023.

      * **1.080691642651297** indicates the ratio of the orders of the current time period to the orders of the same time period on the previous day.

      * **1.4534883720930232** indicates the ratio of the orders of the current time period to the orders of the same time period two days before.

* Results in column format

   * Query and analysis statement

      ```SQL
      * |SELECT time,
        diff [1] AS day1,
        diff [2] AS day2,
        diff [3] AS day3,
        diff [4] AS ratio1,
        diff [5] AS ratio2
      FROM  (
          SELECT time,
            TS_COMPARE(PV, 86400, 172800) AS diff
          FROM      (
              SELECT
                  COUNT(*) AS PV,
                  DATE_TRUNC('hour', __time__) AS time
              GROUP BY time
            )
          GROUP BY time
          ORDER BY time
        )
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66f067d6d0df4b54be03ddfe13c9615e~tplv-goo7wpa0wc-image.image) </span>

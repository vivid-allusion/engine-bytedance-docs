---
title: "Window functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Window-functions"
---

This topic describes the syntax of window functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

Window functions are used for aggregation, sorting, and other operations, and they include three core elements: partitioning, ordering, and framing. Unlike regular aggregate functions, window functions generate a result for each row of data.

<span id="f75abab9"></span>
## List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>



|Function |Syntax |Description |
|---|---|---|
|Aggregate functions |/ |Supports the use of aggregate functions in window functions. Please refer to [Aggregate functions](https://docs.byteplus.com/docs/tls/Aggregate-functions-2) for the list of aggregate functions. |
|CUME_DIST |CUME_DIST() |Calculates the cumulative distribution of a row within its window partition, computed as the ratio of the number of rows that are preceding or peer with the current row to the total number of rows in the window partition. |
|DENSE_RANK |DENSE_RANK() |Ranks values within a window partition. |
|FIRST_VALUE |FIRST_VALUE(KEY) |Returns the value of the first row in each window partition. |
|LAG |LAG(KEY, offset, default_value) |Returns the value located `offset` rows above the current row within the partition. |
|LAST_VALUE |LAST_VALUE(KEY) |Returns the value of the last row in each window partition. |
|LEAD |LEAD(KEY, offset, default_value) |Returns the value located `offset` rows below the current row within the partition. |
|NTILE |NTILE(n) |Divides the rows within each window partition into an ordered and approximately equal number of groups, and it returns the group number for each row, starting from 1. |
|NTH_VALUE |NTH_VALUE(KEY, offset) |Returns the KEY value of the row at the specified offset within each window partition. |
|PERCENT_RANK |PERCENT_RANK() |Calculates the relative position of each row within each window partition, expressed as a percentage. |
|RANK |RANK() |Calculates the rank of each data row in each window partition. The same value in the same partition will receive the same ranking, and the ranking of the next value will skip these duplicate ranking values. F |
|ROW_NUMBER |ROW_NUMBER() |Calculates the rank of each data row in each window partition. Each value has a unique sequence number, starting with 1. |


<span id="7fbf0209"></span>
## Aggregate functions

Support the use of aggregate functions in window functions. This topic takes the AVERAGE function as an example.

<span id="8a0c0b95"></span>
### Function syntax


* Syntax format

   ```SQL
   AVG(KEY) OVER (
       [PARTITION BY partition_expression]
       [ORDER BY order_expression]
       [frame]
   )
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |AVG(KEY) |Aggregate functions, please refer to [Aggregate functions](https://docs.byteplus.com/docs/tls/Aggregate-functions-2). |
   |partition_expression |Specify the partition expression of the window, and the system will divide the data into different partitions according to the partition expression. |
   |order_expression |Specify the sorting expression of the window, and the system will sort the data in each partition according to the sorting expression. |
   |frame |The window frame is used to further refine the scope of the window.<br><br>For example, `RANGE BETWEEN unbounded preceding AND unbounded following` represents all rows in the current window partition. |
   

* Return value description

   The return value is of the double type.


<span id="59d8355f"></span>
### Example


* Scenario

   Perform window partitioning according to the request method, and calculate the average request time within each partition.

* Query and analysis statement

   ```SQL
   * |
   SELECT
     Method,
     ReqID,
     ReqTime,
     AVG(ReqTime) OVER(
       PARTITION BY Method
     ) AS avg_time
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f11f59c3c4b8423fad84fc8c1bd9113f~tplv-goo7wpa0wc-image.image) </span>


<span id="1a27572e"></span>
## CUME_DIST

CUME_DIST function is used to calculate the cumulative distribution of a row within its window partition, computed as the ratio of the number of rows that are preceding or peer with the current row to the total number of rows in the window partition.

<span id="b564f34a"></span>
### Function syntax


* Syntax format

   ```SQL
   CUME_DIST() OVER (
       [PARTITION BY partition_expression]
       [ORDER BY order_expression]
   )
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |partition_expression |Specify the partition expression of the window, and the system will divide the data into different partitions according to the partition expression. |
   |order_expression |Specify the sorting expression of the window, and the system will sort the data in each partition according to the sorting expression. |
   

* Return value description

   The return value is of the double type.


<span id="19f58704"></span>
### Example


* Scenario

   Partition the data based on the request method and calculate the cumulative distribution ratio for each request within their respective partitions.

* Query and analysis statement

   ```SQL
   * |
   SELECT
     Method,
     ReqID,
     ReqTime,
     CUME_DIST() OVER(
       PARTITION BY Method
       ORDER BY
         ReqTime DESC
     ) AS cume
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f92eb126c4664944810e440773c2e7cd~tplv-goo7wpa0wc-image.image) </span>


<span id="6cae9781"></span>
## DENSE_RANK

DENSE_RANK function is used to rank values within a window partition.

<span id="90da1740"></span>
### Function syntax


* Syntax format

   ```SQL
   DENSE_RANK() OVER (
       [PARTITION BY partition_expression]
       [ORDER BY order_expression]
   )
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |partition_expression |Specify the partition expression of the window, and the system will divide the data into different partitions according to the partition expression. |
   |order_expression |Specify the sorting expression of the window, and the system will sort the data in each partition according to the sorting expression. |
   

* Return value description

   The return value is of the bigint type.


<span id="c86199ed"></span>
### Example


* Scenario

   Partition the data based on the request method and sort the requests by their request times within each respective partition.

* Query and analysis statement

   ```SQL
   * |
   SELECT
     Method,
     ReqID,
     ReqTime,
     DENSE_RANK() OVER(
       PARTITION BY Method
       ORDER BY
         ReqTime DESC
     ) AS rank
   ORDER BY
     Method,
     rank
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0592e4f34dfe4a9ba75e1a04c696700a~tplv-goo7wpa0wc-image.image) </span>


<span id="bf28d797"></span>
## FIRST_VALUE

FIRST_VALUE function returns the value of the first row in each window partition.

<span id="d96f4e58"></span>
### Function syntax


* Syntax format

   ```SQL
   FIRST_VALUE(KEY) OVER(
       [PARTITION BY partition_expression]
       [ORDER BY order_expression]
       [frame]
   )
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   |partition_expression |Specify the partition expression of the window, and the system will divide the data into different partitions according to the partition expression. |
   |order_expression |Specify the sorting expression of the window, and the system will sort the data in each partition according to the sorting expression. |
   |frame |The window frame is used to further refine the scope of the window.<br><br>For example, `RANGE BETWEEN unbounded preceding AND unbounded following` represents all rows in the current window partition. |
   

* Return value description

   The return value is the same as the data type of the key.


<span id="c82a41be"></span>
### Example


* Scenario

   Partition the data based on the request method and calculate the minimum request time within each partition.

* Query and analysis statement

   ```SQL
   * |
   SELECT
     Method,
     ReqID,
     ReqTime,
     FIRST_VALUE(ReqTime) OVER(
       PARTITION BY Method
       ORDER BY
         ReqTime
     ) AS firstvalue
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed523586c37c483ca99f836f1002aac8~tplv-goo7wpa0wc-image.image) </span>


<span id="73e974fc"></span>
## LAG

LAG function returns the value located `offset` rows above the current row within the partition.

<span id="1859ed0f"></span>
### **Function Syntax**


* Syntax format

   ```SQL
   LAG(KEY, offset, default_value) over (
       [partition by partition_expression]
       [order by order_expression]
       [frame]
   )
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   |offset |Specify the offset. If the value of the **offset** parameter is 0, the value of the specified field in the current row is returned. |
   |default_value |Specify the default value. If no row exists at the specified offset after the current row, the default value is returned. |
   |partition by<br><br>partition_expression |The window function divides the rows of data into different partitions based on the partition_expression. |
   |order by<br><br>order_expression |The window function sorts the rows within each partition based on the ordering expression. |
   |frame |A window frame. |
   

* Return value description

   The data type of the return value is the same as the type of the parameter value.


<span id="b9d93415"></span>
### Example


* Scenario

   Calculate the number of requests per hour and the ratio of the number of requests within one hour to the previous hour.

* Query and analysis statement

   ```Plain
   * |
   SELECT
     hour,
     total,
     total * 1.00000 /(LAG(total, 1, 1) over(ORDER BY hour)) AS ratio 
   FROM  (
       SELECT
         COUNT(Action) AS total,
         DATE_TRUNC('hour', __time__) AS hour
       GROUP BY
         hour
     )
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66c95337766f46049977ab09563c9019~tplv-goo7wpa0wc-image.image) </span>


<span id="84a16aa1"></span>
## LAST_VALUE

LAST_VALUE function returns the value of the last row in each window partition.

<span id="108b8652"></span>
### Function syntax


* Syntax format

   ```SQL
   LAST_VALUE(KEY) OVER(
       [PARTITION BY partition_expression]
       [ORDER BY order_expression]
       [frame]
   )
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   |partition_expression |Specify the partition expression of the window, and the system will divide the data into different partitions according to the partition expression. |
   |order_expression |Specify the sorting expression of the window, and the system will sort the data in each partition according to the sorting expression. |
   |frame |The window frame is used to further refine the scope of the window.<br><br>For example, `RANGE BETWEEN unbounded preceding AND unbounded following` represents all rows in the current window partition.<br><br>If no frame is specified, the window ranges from the first line in the current window to the current line. |
   

* Return value description

   The return value is the same as the data type of the key.


<span id="4157e60b"></span>
### Example


* Scenario

   Partition the data based on the request method and calculate the maximum request time within each partition.

* Query and analysis statement

   ```SQL
   * |
   SELECT
     Method,
     ReqID,
     ReqTime,
     LAST_VALUE(ReqTime) OVER(
       PARTITION BY Method
       ORDER BY
         ReqTime
       RANGE BETWEEN unbounded preceding AND unbounded following
     ) AS lastvalue
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec31869db05041128633ed395a9c8386~tplv-goo7wpa0wc-image.image) </span>


<span id="967623fc"></span>
## LEAD

LEAD function returns the value located `offset` rows below the current row within the partition.

<span id="f72e73c6"></span>
### **Function Syntax**


* Syntax format

   ```SQL
    LEAD(KEY, offset, default_value) over (
       [partition by partition_expression]
       [order by order_expression]
       [frame]
   )
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   |offset |Specify the offset. If the value of the **offset** parameter is 0, the value of the specified field in the current row is returned. |
   |default_value |Specify the default value. If no row exists at the specified offset after the current row, the default value is returned. |
   |partition by<br><br>partition_expression |The window function divides the rows of data into different partitions based on the partition_expression. |
   |order by<br><br>order_expression |The window function sorts the rows within each partition based on the ordering expression. |
   |frame |A window frame. |
   

* Return value description

   The data type of the return value is the same as the type of the parameter value.


<span id="1275c45f"></span>
### Example


* Scenario

   Calculate the number of requests per hour and the ratio of the number of requests within one hour to the next hour.

* Query and analysis statement

   ```SQL
   * |
   SELECT
     hour,
     total,
     total * 1.00000 /(LEAD(total, 1, 1) over(ORDER BY hour)) AS ratio 
   FROM  (
       SELECT
         COUNT(Action) AS total,
         DATE_TRUNC('hour', __time__) AS hour
       GROUP BY
         hour
     )
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7f90e5c0ab741b687afeeb09faa9c9c~tplv-goo7wpa0wc-image.image) </span>


<span id="2e20c139"></span>
## NTILE

The NTILE function is used to divide the rows within each window partition into an ordered and approximately equal number of groups, and it returns the group number for each row, starting from 1.

<span id="da81c700"></span>
### Function syntax


* Syntax format

   ```SQL
   NTILE(n) OVER(
       [PARTITION BY partition_expression]
       [ORDER BY order_expression]
   )
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |n |Specify the number of packets.<br><br>NTILE function divides the rows in the partition into n groups as evenly as possible. |
   |partition_expression |Specify the partition expression of the window, and the system will divide the data into different partitions according to the partition expression. |
   |order_expression |Specify the sorting expression of the window, and the system will sort the data in each partition according to the sorting expression. |
   

* Return value description

   The return value is of the bigint type.


<span id="5f4ec301"></span>
### Example


* Scenario

   Partition the data based on the request method and divide the rows within each partition into 3 groups.

* Query and analysis statement

   ```SQL
   * |
   SELECT
     Method,
     ReqID,
     ReqTime,
     NTILE(3) OVER(
       PARTITION BY Method
       ORDER BY
         ReqTime
     ) AS ntile
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ffddb7247bf4a78863640248aa29eb7~tplv-goo7wpa0wc-image.image) </span>


<span id="5745f4ee"></span>
## NTH_VALUE

NTH_VALUE function is used to return the KEY value of the row at the specified offset within each window partition.

<span id="6e20de9d"></span>
### Function syntax


* Syntax format

   ```SQL
   NTH_VALUE(KEY, offset) OVER(
       [PARTITION BY partition_expression]
       [ORDER BY order_expression]
       [frame]
   )
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value can be any data type. |
   |offset |The offset is counted from the first row within the window partition.<br><br>If there are not enough rows to satisfy the offset, null is returned. |
   |partition_expression |Specify the partition expression of the window, and the system will divide the data into different partitions according to the partition expression. |
   |order_expression |Specify the sorting expression of the window, and the system will sort the data in each partition according to the sorting expression. |
   |frame |The window frame is used to further refine the scope of the window.<br><br>For example, `RANGE BETWEEN unbounded preceding AND unbounded following` represents all rows in the current window partition. |
   

* Return value description

   The return value is the same as the data type of the key.


<span id="f29ec1ee"></span>
### Example


* Scenario

   Partition the data based on the request method and return the request ID with the third highest request time within each partition.

* Query and analysis statement

   ```SQL
   * |
   SELECT
     Method,
     ReqID,
     ReqTime,
     NTH_VALUE(ReqID, 3) OVER(
       PARTITION BY Method
       ORDER BY
         ReqTime DESC
       RANGE BETWEEN unbounded preceding AND unbounded following
     ) AS value
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ad2c2a68bd340d7914c57bf98b39ec4~tplv-goo7wpa0wc-image.image) </span>


<span id="18c17100"></span>
## PERCENT_RANK

PERCENT_RANK function is used to calculate the relative position of each row within each window partition, expressed as a percentage. The formula is `(rank - 1)/(total_rows - 1)`, `rank`is the rank of the current row, and `total_rows`is the total number of rows in the current window partition.

<span id="f760fccd"></span>
### Function syntax


* Syntax format

   ```SQL
   PERCENT_RANK() OVER(
       [PARTITION BY partition_expression]
       [ORDER BY order_expression]
   )
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |partition_expression |Specify the partition expression of the window, and the system will divide the data into different partitions according to the partition expression. |
   |order_expression |Specify the sorting expression of the window, and the system will sort the data in each partition according to the sorting expression. |
   

* Return value description

   The return value is of double type.


<span id="de5fdb39"></span>
### Example


* Scenario

   Partition the data based on the request method and return the relative rank (in percentage form) of each request time within each partition.

* Query and analysis statement

   ```SQL
   * |
   SELECT
     Method,
     ReqID,
     ReqTime,
     PERCENT_RANK() OVER(
       PARTITION BY Method
       ORDER BY
         ReqTime DESC
     ) AS timerank
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5687adb97874b5eb4b0106f9b196686~tplv-goo7wpa0wc-image.image) </span>


<span id="4cda8b59"></span>
## RANK

The RANK function is used to calculate the rank of each data row in each window partition. The same value in the same partition will receive the same ranking, and the ranking of the next value will skip these duplicate ranking values. For example, if the ranking of two identical values is 1, then the ranking of the next value will be 3.

<span id="020aa70e"></span>
### Function syntax


* Syntax format

   ```SQL
   RANK()  OVER(
       [PARTITION BY partition_expression]
       [ORDER BY order_expression]
   )
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |partition_expression |Specify the partition expression of the window, and the system will divide the data into different partitions according to the partition expression. |
   |order_expression |Specify the sorting expression of the window, and the system will sort the data in each partition according to the sorting expression. |
   

* Return value description

   The return value is of bigint type.


<span id="de4932e8"></span>
### Example


* Scenario

   Partition the data based on the request method and return the rank of each request time within each partition.

* Query and analysis statement

   ```SQL
   * |
   SELECT
     Method,
     ReqID,
     ReqTime,
     RANK() OVER(
       PARTITION BY Method
       ORDER BY
         ReqTime
     ) AS timerank
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8cf8ea3729542848c4c1f7936917493~tplv-goo7wpa0wc-image.image) </span>


<span id="596ea496"></span>
## ROW_NUMBER

ROW_NUMBER function is used to calculate the rank of each data row in each window partition. Each value has a unique sequence number, starting with 1.

<span id="1a54c0fb"></span>
### Function syntax


* Syntax format

   ```SQL
   ROW_NUMBER() OVER(
       [PARTITION BY partition_expression]
       [ORDER BY order_expression]
   )
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |partition_expression |Specify the partition expression of the window, and the system will divide the data into different partitions according to the partition expression. |
   |order_expression |Specify the sorting expression of the window, and the system will sort the data in each partition according to the sorting expression. |
   

* Return value description

   The return value is of bigint type.


<span id="16c61082"></span>
### Example


* Scenario

   Partition the data based on the request method and return the rank of the request times within each partition.

* Query and analysis statement

   ```SQL
   * |
   SELECT
     Method,
     ReqID,
     ReqTime,
     ROW_NUMBER() OVER(
       PARTITION BY Method
       ORDER BY
         ReqTime
     ) AS timerank
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54f66279a95d49158af74ba6285d52c3~tplv-goo7wpa0wc-image.image) </span>

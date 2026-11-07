---
title: "LIMIT syntax"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/LIMIT-syntax-2"
---

By default, 100 rows of data are returned in the log query and analysis results. You can specify the number of rows to be returned using the LIMIT syntax. The value ranges from 1 through 1,000,000. The LIMIT syntax limits the number of rows returned by a SELECT statement.

<span id="Syntax format"></span>
## Syntax format

The LIMIT syntax format is as follows:


|SQL syntax format |Description |
|---|---|
|`limit n` |Returns the first n rows of data in the result. |
|`offset s limit n` |Returns n rows of data starting from the s+1 row in the result. |



|Parameter |Description |
|---|---|
|n |The number of rows of data to be returned. The default value of `n` is 100. Value range: 1–1,000,000. |
|s |Reads data starting from the s+1 row. The default value of `s` is 0. Value range: 0–999,999. It means that data is read from the first row by default. Data can be read from the 1,000,000th row at most.<br><br>The sum of s and n cannot exceed 1,000,000. |


<span id="Examples"></span>
## Examples

<span id="bee60155"></span>
### Example 1


* Scenario

   Count the number of requests corresponding to different status codes and return the top 3.

* Query and analysis statement

   ```SQL
   * | SELECT status, COUNT(*) as PV GROUP BY status ORDER BY PV DESC LIMIT 3
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6c6c058c4a243fe8a96b54de5a553c7~tplv-goo7wpa0wc-image.image) </span>


<span id="868af145"></span>
### Example 2


* Scenario

   Count the number of requests corresponding to different users, and return the data from the 5th row to the 9th row, with a total of 5 rows of results.

* Query and analysis statement

   ```SQL
   * | SELECT UID, COUNT(*) AS PV GROUP BY UID OFFSET 4 LIMIT 5
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a171f799e678445fbebcf880108efe93~tplv-goo7wpa0wc-image.image) </span>

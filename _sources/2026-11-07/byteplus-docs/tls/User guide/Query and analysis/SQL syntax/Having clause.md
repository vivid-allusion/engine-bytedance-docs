---
title: "Having clause"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Having-clause-2"
---

The HAVING clause is used to filter out group results that meet specific conditions.

<span id="6f834caf"></span>
## **Syntax description**

The syntax format of the HAVING clause is as follows:

```SQL
HAVING bool_expression
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The HAVING clause is used to filter group results and can be used with aggregate functions (SUM, AVG, etc.). The WHERE clause is used to filter raw data before grouping and does not support aggregate functions (SUM, AVG, etc.).</div>


* <div data-tips="true" data-tips-type="tip">The filtering operation of the HAVING clause occurs after grouping but before sorting.</div>



Parameter description


|Parameter |Description |
|---|---|
|bool_expression |The boolean expressions are used to filter grouped results. |


<span id="c8e2c314"></span>
## **Examples**

Query the request URLs with an average request body size greater than 1000 bytes along with their average request body size.


* Query and analysis statement

   ```SQL
   * |
   SELECT
     AVG(ReqSize) AS Size,
     URL
   GROUP BY
     URL
   HAVING
     Size > 1000
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d568748fe1041279c6f6e121b816de8~tplv-goo7wpa0wc-image.image) </span>

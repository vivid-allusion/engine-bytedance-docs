---
title: "GROUP BY syntax"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/GROUP-BY-syntax-2"
---

The GROUP BY clause works with an aggregate function to group the query and analysis results based on one or more fields.

<span id="Syntax format"></span>
## Syntax format

The GROUP BY syntax format is as follows:

```SQL
* | SELECT Key, AGGREGATE_FUNCTION GROUP BY [ Key | Alias | number ]
```


Parameter description:


|Parameter |Description |
|---|---|
|Key |The name of a log field or the calculation result column of the aggregate function. You can specify one or more columns. |
|Alias |The alias of the field or column. The query and analysis results are grouped based on the alias of the field or the calculation result column of the aggregate function. |
|number |The ordinal number of a field in the SELECT statement. The number starts from 1. |
|AGGREGATE_FUNCTION |Normally, you can use the GROUP BY syntax together with multiple aggregate functions, such as MIN, MAX, AVG, SUM, and COUNT. |


In Torch Log Service (TLS), if you use the GROUP BY syntax in a SELECT statement, select a column or aggregate function included in the GROUP BY syntax when you execute the SELECT statement. For example, when you group results by status, you cannot use the query statement `* | SELECT status, request_method, COUNT(*) AS PV GROUP BY status` as `request_method` is not a column included in the GROUP BY clause.

<span id="Examples"></span>
## Examples

<span id="f8579f44"></span>
### Example 1


* Scenario

   Count the number of requests corresponding to different request methods.

* Query and analysis statement

   ```SQL
   * | SELECT method, count(*) AS PV GROUP BY method
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd358b51b4ae474ba4828594a1a4a629~tplv-goo7wpa0wc-image.image) </span>


<span id="0b3e2a54"></span>
### Example 2


* Scenario

   Count the number of requests initiated by each user using different request methods.

* Query and analysis statement

   ```SQL
   * | SELECT UID, 
   Method, 
   COUNT(*) AS total 
   GROUP BY UID, Method
   ORDER BY UID ASC, Method Desc Limit 1000
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/587a3ec61cc248c7b26854b670f01ad5~tplv-goo7wpa0wc-image.image) </span>

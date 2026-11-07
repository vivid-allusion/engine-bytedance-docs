---
title: "ORDER BY syntax"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/ORDER-BY-syntax-2"
---

The ORDER BY syntax sorts the query and analysis results based on the field name specified by the Key parameter.

<span id="Syntax format"></span>
## Syntax format

The ORDER BY syntax format is as follows:

```SQL
ORDER BY Key [DESC | ASC]
```


Parameter description


|Parameter |Description |
|---|---|
|Key |The name of a log field or the calculation result column of the aggregate function. The results are sorted based on the column you specify.<br><br>You can specify multiple fields to sort results by each field in different orders, such as `ORDER BY Key1 ASC, Key2 DESC`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the specified field for result sorting has duplicate values, the sorted results may vary each time. To ensure that the sorted results are consistent, specify multiple fields to sort results.</div><br> |
|DESC |The sort order. By default, the results are sorted in ascending order. Specify DESC to sort results in descending order as needed. |
|ASC |The default sort order. ASC indicates the ascending order.<br><br>By default, query and analysis results are sorted in ascending order, so you do not have to specify the keyword DESC or ASC. To sort results in descending order, specify the keyword DESC. |


<span id="Examples"></span>
## Examples

<span id="170c33d6"></span>
### Example 1


* Scenario

   Count the number of requests corresponding to different request methods and sort them in ascending order based on the number of requests.

* Query and analysis statement

   ```SQL
   * | SELECT method, count(*) AS PV GROUP BY method ORDER BY PV
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/251f5ef3caf1431a86b50c1e741b8939~tplv-goo7wpa0wc-image.image) </span>


<span id="9997cf6c"></span>
### Example 2


* Scenario

   Count the average request time of each remote address and sort them in descending order according to the request time.

* Query and analysis statement

   ```SQL
   * | SELECT RemoteAddr, avg(ReqTime) as RT GROUP BY RemoteAddr order by RT DESC LIMIT 1000
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e78e4d4e1a2846968dedd28a52037609~tplv-goo7wpa0wc-image.image) </span>

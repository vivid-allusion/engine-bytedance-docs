---
title: "Subqueries"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Subqueries-2"
---

A subquery is a SELECT statement nested inside another SELECT statement. For a main query and the nested subquery, the system conducts statistical analysis on raw data, then conducts another statistical analysis on the analysis result. Subqueries are suitable in complex analysis scenarios.

<span id="dd1f5b7f"></span>
## Syntax format

Subquery syntax format:

```SQL
* | SELECT key FROM (sub_query)
```


For a main query that nests a subquery, specify a FROM clause for the SELECT statement.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">TLS subquery syntax supports more than one nested SELECT statement.</div>


* <div data-tips="true" data-tips-type="tip">In a subquery statement, you are not required to specify the keyword <code>FROM</code>. By default, this statement analyzes the log data in the current topic.</div>


* <div data-tips="true" data-tips-type="tip">The <code>LIMIT</code> clause is not supported in subqueries.</div>



Parameter description:


|Parameter |Description |
|---|---|
|key |The fields to be obtained from the subquery for another statistical analysis. |
|subquery |The subquery statement. Enclose the statement in parentheses `()`. |


<span id="db1b2874"></span>
## Examples


* Scenario

   Count the number of users for each version of the client based on access logs.

* Query and analysis statement

   ```SQL
   * | SELECT Client,COUNT(*) AS UserNum 
   FROM (SELECT Client,account_id GROUP BY Client,account_id) 
   GROUP BY Client 
   ORDER BY Client
   ```
   

   * The first layer statement `SELECT Client,account_id GROUP BY Client,account_id` means grouping and deduplicating by `Client` and `account_id`.

   * The second layer statement `SELECT Client, count(*) AS UserNum FROM` means performing a grouped count on the result of the first layer query to get the number of users corresponding to each client version.

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8494c559ffa44ab4ae6187f5211a77ca~tplv-goo7wpa0wc-image.image) </span>

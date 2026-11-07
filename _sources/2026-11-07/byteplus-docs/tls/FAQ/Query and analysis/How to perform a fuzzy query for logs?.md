---
title: "How to perform a fuzzy query for logs?"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/How-to-perform-a-fuzzy-query-for-logs"
---

When the Torch Log Service executes a fuzzy query statement, it recognizes the first 100 words that match the fuzzy keywords and returns a log containing any of those 100 words. You can perform a fuzzy query in the following ways.


<Tabs>
<Tab zoneid="XQ2BGwlCZo" title="Basic fuzzy query">
<TabTitle>Basic fuzzy query</TabTitle>

* Example 1: Query logs containing keywords starting with `erro`.

   ```Bash
   erro*
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cbf5f58e2304ef8a1dca644f26f8796~tplv-goo7wpa0wc-image.image) </span>

* Example 2: Query the logs whose `Action` field value starts with `put`.

   ```SQL
   Action:put*
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4d31b5403244e179d801b354a024241~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="nPdUnn03lt" title="Based on SQL LIKE syntax">
<TabTitle>Based on SQL LIKE syntax</TabTitle>

The SQL LIKE syntax is used to specify query conditions in the WHERE clause, enabling precise querying of logs. In LIKE syntax, the percent sign (%) represents matching any number of characters, including 0; the underscore (_) represents matching a single character.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When using LIKE syntax, the target field (such as <code>tag</code>) must have key\-value index enabled and statistics enabled. For more information, please refer to <a href="https://docs.byteplus.com/docs/tls/getting_started_configure_indexes#e3e54d2b">Configure key\-value indexes</a>.</div>



* Example 1: Query the logs whose `ReqID` field value starts with `8f60`.

   ```SQL
   * | SELECT * WHERE ReqID LIKE '8f60%'
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcbc0d65b8d9455da213c669873aeae8~tplv-goo7wpa0wc-image.image) </span>

* Example 2: The query `region`field value does not contain logs for `Shanghai`.

   ```SQL
   * | SELECT * WHERE region NOT LIKE '%shanghai%'
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0fe455aa2534ade8da3473474981049~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>

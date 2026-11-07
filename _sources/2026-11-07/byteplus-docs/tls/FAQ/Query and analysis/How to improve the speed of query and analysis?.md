---
title: "How to improve the speed of query and analysis?"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/How-to-improve-the-speed-of-query-and-analysis"
---

This topic introduces methods to improve the speed of log query and analysis.

<span id="af7a53cf"></span>
## Increase the number of shards

Increasing the number of shards can enhance the read and write capabilities of Torch Log Service(TLS), but it only takes effect on newly written data. A shard represents computing resources. The more shards there are, the faster the computing will be. You can appropriately increase the number of shards by splitting shards. For specific operations, please refer to [Split a shard](https://docs.byteplus.com/docs/tls/Managing_shards#%E5%88%86%E8%A3%82%E5%88%86%E5%8C%BA).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Increasing the number of shards will incur more charges, please increase them as needed. For the billing information, please refer to <a href="https://docs.byteplus.com/docs/tls/billable_items">Billable items</a>.</div>


<span id="ce11972b"></span>
## Narrow down the time range or the data amount


* The larger the query time range, the slower the query speed. It is recommended to appropriately narrow the query time range to improve the query speed.

* The larger the amount of query data, the slower the query speed. It is recommended to reduce the amount of query data appropriately to improve the query speed.


<span id="abdcd241"></span>
## Repeatedly execute the query operation.

When the query results are not accurate, you can try to repeatedly execute the retrieval operation multiple times. Each time during query, the underlying acceleration mechanism of TLS will conduct query based on the existing results. Therefore, repeated queries can improve the accuracy of the retrieval results. For more information, please refer to [What can I do if the query results are inaccurate?](https://docs.byteplus.com/docs/tls/troubleshooting_query_and_analysis).

<span id="54688e63"></span>
## Optimize query statement

Statements with a long query time have the following characteristics.


* There are many query conditions.

* The amount of data scanned during query is large.


You can optimize the query and analysis statement by doing the following.


* Remove unnecessary query conditions

   For example, when using multi\-condition queries, if the logs that meet condition A must also meet condition B, then query condition B can be removed. The example is as follows:

   * Query statements (fast)

      ```Plain
      log_msg: "INFO| write logs sucessful"
      ```
      

   * Query statements (slow)

      ```Plain
      log_msg: "INFO| write logs sucessful" AND log_level:INFO
      ```
      

* Merge query conditions within the same key range.

   When using range query, if it is necessary to limit the start and end range of the query, use the double range operator to replace the single range operator. Examples are as follows:

   * Query statements (fast)

      ```Plain
      log_status: [1000 TO 2000}
      ```
      

   * Query statements (slow)

      ```Plain
      log_status: >= 1000 AND log_status: < 2000
      ```
      

* Put filtering conditions with a high hit rate into the SQL statement.

   In the scenario where query and analysis are used in combination, the conditions with a high hit rate can be placed in the SQL part to improve the query speed. For example, in the following example, if the ratio of the number of logs that meet `log_level:INFO` to the total number of logs exceeds 50%, then putting this condition into the SQL statement for filtering will be faster.

   * Query and analysis statement (fast)

      ```SQL
      * | select count(*) as cnt where log_level = 'INFO'
      ```
      

   * Query and analysis statement (slow)

      ```SQL
      log_level:INFO | select count(*) as cnt
      ```
      

* Specify the columns to be queried in the SQL analysis statements to avoid reading all columns.

   If you need to query all columns, please use the query syntax. Examples are as follows:

   * Query and analysis statement (fast)

      ```SQL
      * | select a, b, c
      ```
      

   * Query and analysis statement (slow)

      ```Plain
      * | select *
      ```

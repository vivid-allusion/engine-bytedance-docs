---
title: "Query and analysis process"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Query-and-analysis-process"
---

This topic introduces the basic process of querying and analyzing logs.

<span id="dbaecae2"></span>
## 1 Configuration index

Indexes are an important data storage structure that helps you quickly find critical information in massive logs. The index configuration determines how the query is performed and the accuracy of the results. To obtain the best query results, configure the corresponding index based on the logs you collect and your query analysis needs.

Before performing a query and analysis operations, it is necessary to configure the indexes first. Torch Log Service(TLS) supports full\-text indexes, key\-value indexes, and reserved field indexes.


* [Configure full-text indexes](https://docs.byteplus.com/docs/tls/Configure-indexes-2#ddc9245c)

   After enabling full\-text indexes, TLS will split the logs into multiple text\-type terms based on delimiters, allowing you to perform full\-text queryes by entering keywords.

* [Configure key-value indexes](https://docs.byteplus.com/docs/tls/Configure-indexes-2#73e527a0)

   After enabling key\-value indexes, TLS will first split the logs according to field names, then split the field values within each field based on delimiters. You can set the index data types for each field, including text, long, double, and json. For explanations of index data types, please refer to [Index data types](https://docs.byteplus.com/docs/tls/Index-data-types-2).

* [Configure indexes for reserved fields](https://docs.byteplus.com/docs/tls/Configure-indexes-2#0be3542b)

   TLS defaults to enabling key\-value indexes for some internal reserved fields.


<span id="24606740"></span>
## 2 Select the query method

You can choose between full\-text query or key\-value query, depending on your index configuration and query requirements. For detailed instructions, please refer to [Query method](https://docs.byteplus.com/docs/tls/Log-query-syntax-2#1e3dcb53).


* Full\-text query

   When setting up a query statement, enter keywords directly without specifying a specific log field name. Full\-text query is good for quickly finding logs containing a specified keyword, without having to worry about which field the keyword is in, such as querying for keyword `error`.

* Key\-value query

   When setting up a query statement, you need to specify the field name and field value. Key\-value query is useful for precise queries on known field values, such as `username: joe` or all requests made by this user.


<span id="55596b35"></span>
## 3 Select query accuracy

Depending on your query requirements, choose between an exact query or a fuzzy query. For detailed instructions, please refer to [Accuracy](https://docs.byteplus.com/docs/tls/Log-query-syntax-2#57d90d06).


* Exact query

   When querying, specify the complete keyword, that is, match by the complete keyword.

* Fuzzy query

   Specify only some of the characters of the keyword in the query criteria, add a wild\-card asterisk ( `*`) or a question mark ( `?`) in between or at the end, TLS will match the 100 words that meet the criteria and return the log that meets the query criteria and contains the 100 words. When you want to match a set of similar keywords, you can use a fuzzy query. For example, `cn *` indicates that the query contains logs with words beginning with `cn`.


<span id="c7c09adf"></span>
## 4 Constructing query analysis statements

The query and analysis statement consists of a query statement and an analysis statement, which are divided by an English vertical line ( `|`) to represent the analysis and calculation in the log filtered by the query conditions. For more information, please refer to [Log analysis](https://docs.byteplus.com/docs/tls/Analysis-overview#15fde56f).


* Query statement: You can specify query criteria (time range, request type, etc.) in the query statement to filter out the target log. For a detailed description of the query syntax, please refer to [Log query syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2).

* Analysis statement: The analysis statement uses the standard SQL 92 syntax, which is used for filtering, statistics, aggregation, and other operations on logs. Analysis statements must be used together based on query statements. For a detailed description of parsing syntax, please refer to [Analysis syntax](https://docs.byteplus.com/docs/tls/Analysis-overview#e88849cb).


<span id="55ad0905"></span>
## 5 Perform query analysis operations

On the query and analysis page to which the target log belongs, select the appropriate query time range, and then enter the query analysis statement to perform the relevant operations. For specific operation, please refer to [Query logs](https://docs.byteplus.com/docs/tls/Query-logs-2) and [Analyze logs](https://docs.byteplus.com/docs/tls/Analyze-logs-2).

<span id="75b21009"></span>
## 6 View query and analysis results

After performing a query and analysis operation, you can view the results at the bottom of the query and analysis page.


* Query results: After you filter the logs by the query statement, you can check the filtered log contents under the **Original Log** page. For detailed instructions, please refer to [View query results](https://docs.byteplus.com/docs/tls/Query-logs-2#f93ce84f).

* Query and analysis results: After performing query and analysis, you can check the **Statistical Charts** page to view the visual query analysis results. TLS provides tables, line charts, statistical charts and other rich chart types for displaying query analysis results. For detailed instructions, please refer to [View analysis results](https://docs.byteplus.com/docs/tls/Analyze-logs-2#48099bdd).

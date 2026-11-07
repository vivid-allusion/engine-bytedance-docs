---
title: "What can I do if the query results are inaccurate?"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/troubleshooting_query_and_analysis"
---

If TLS prompts that the query results are inaccurate when you query the analysis logs, refer to this document for troubleshooting.

<span id="93df8829"></span>
### Problem description

When you query and analyze logs, if the TLS console prompts that the query results are inaccurate, it means that TLS failed to scan all logs, and the query and analysis results returned are not accurate results based on all logs.

<span id="3078d36c"></span>
### Possible reasons

Possible reasons for inaccurate query results are as follows:


* The query time range is too large (for example, the query time range is 3 months), and TLS cannot scan all logs in this time period in one retrieval. To return results quickly, return partially inaccurate results first.

* The search conditions are too complex (for example, 30 search conditions are set simultaneously), and TLS cannot read all the search results at once.

* The amount of data calculated by SQL is too large. If you set multiple fields in a single SQL statement, and the amount of data in these fields is too large to be read by the shard (each shard can only read 1GiB of data), the returned results are inaccurate.


<span id="b6b6b7e8"></span>
### Solution

Take appropriate actions based on possible causes, such as narrowing the search time range, simplifying the search analysis statement, or executing the search analysis statement multiple times (up to 10 times).

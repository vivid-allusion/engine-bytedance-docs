---
title: "Transaction write backlog"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Transaction_write_backlog"
---

<span id="177119a1"></span>
## Use cases


* Assess the degree of backlog through transaction monitoring ([StarRocks](https://grafana.bytedance.net/d/04l9wttNz/emr-serverless-starrocks?editPanel=62&orgId=1&refresh=1m&from=now-12h&to=now&var-ResourceId=cdw-5cj8p73aqz47g09ddivx&var-ENV=EMR-Serverless-Guangzhou&var-AccountId=2100584735)) or the results of the following commands (the default maximum runningTxn limit is 1000).

* If the error message “current running txns on db xxx is xx, larger than limit xx” appears, it means the limit has been reached and the upper limit must be adjusted immediately to prevent further loss.


<span id="b310f460"></span>
## Applicable versions


|**Product form** |**Engine** |**Deployment method** |**Applicable versions** |
|---|---|---|---|
|Serverless instance<br><br>(Fully managed) |StarRocks |Decoupled storage and compute |Only supported in version 3.2.12 |
|||Integrated storage and compute |Only supported in version 3.2.11 |


<span id="3e8ae797"></span>
## Procedure


1. Current transaction status for each db


```SQL
-- Doris/StarRocks
show proc '/transactions';
show proc '/transactions/${db_id}' -- View the status of each db
show proc '/transcations/${db_id}/finished' -- View completed import transactions, locate failed transactions, and check the reasons
```



2. Dynamically increase the transaction limit to allow transactions to proceed, alleviate upstream write task latency, and then investigate further.


```SQL
-- StarRocks engine
-- Adjust FE configuration
admin set frontend config ("max_running_txn_num_per_db" = "xxx")  -- Default 1000
```

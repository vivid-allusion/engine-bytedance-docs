---
title: "Large query defense"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/si_doris_large_query_defense"
---

<span id="7b902107"></span>
## Use cases

In production environments, it is necessary to allocate resource usage for business modules to prevent large queries or business bugs from causing cluster resource overload and affecting other services. The engine of EMR Serverless Doris provides multiple resource isolation or query circuit breaking methods.

<span id="f2650a69"></span>
## Applicable versions


|**Product form** |**Engine** |**Deployment method** |**Applicable versions** |
|---|---|---|---|
|Serverless instance<br><br>(fully managed) |Doris |Unified storage and compute |Version 2.1.x and above |


<span id="fc5ad137"></span>
## Procedure

<span id="0f357d31"></span>
### Unified storage and compute, and decoupled storage and compute (lakehouse edition)

There are typically two methods for large query defense.


* Method 1:[Add SQL blocklist](https://docs.byteplus.com/docs/E-MapReduce/109163#74f210d1)

* Method 2:[Add large query circuit breaking resource group](https://docs.byteplus.com/docs/E-MapReduce/109163#6afb3fce)


Select the appropriate method based on actual business requirements.

<span id="74f210d1"></span>
#### **Add SQL blocklist**

```SQL
-- 1. Create block rule
CREATE SQL_BLOCK_RULE rule_001
PROPERTIES (
  "SQL" = "select \\* from t",  -- SQL content (Important: escape characters)
  "cardinality" = "1000",       -- Data scanned
  "partition_num" = "30",      -- Number of partitions scanned
  "tablet_num" = "10",          -- Number of buckets scanned
  "global" = "true",          -- If false, effective at user level
  "enable" = "true"
);

-- 2. If a user-level rule is created, bind the user
set property for 'root' 'SQL_block_rules' = 'rule_001';
```


<span id="6afb3fce"></span>
#### **Add large query circuit breaking resource group**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The values in this example are for reference only. Please refer to business usage patterns and the metrics of <code>__internal_schema.audit_log</code>, and it is recommended to perform comprehensive testing before execution to avoid affecting existing online queries.</div>


```SQL
-- 1. Create large query circuit breaking workload group
create workload Policy test_cancel_Policy
Conditions(query_time > 1000)
Actions(cancel_query) 
properties('enabled'='true'); 

-- 2. View all resource groups
SHOW WORKLOAD POLICY;
```


<span id="72475882"></span>
### Decoupled storage and compute (multi\-warehouse edition)

In the decoupled storage and compute (multi\-warehouse edition) scenario, you can use the SQL blocklist and large query circuit breaking resource group features to achieve user\-level isolation within a single compute warehouse, or achieve resource isolation by binding different compute warehouses.

---
title: "Large query defense"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/si_large_query_defense"
---

<span id="80f91302"></span>
## Use cases

In production environments, resources must be allocated for business modules to prevent cluster resource overload caused by large queries or business bugs, which may impact other business operations. The EMR Serverless StarRocks engine offers various resource isolation and query circuit breaking methods.

<span id="a210649e"></span>
## Applicable versions


|**Product form** |**Engine** |**Deployment method** |**Applicable versions** |
|---|---|---|---|
|Serverless instance<br><br>(fully managed) |StarRocks |Separated storage and compute |Version 3.2.x and above |
|||Unified storage and compute |Version 3.2.x and above |


<span id="12d089c6"></span>
## Procedure

<span id="036a0992"></span>
### Unified storage and compute and separated storage and compute (lakehouse edition)

There are typically two methods for large query defense.


* Method 1: [Add a blocklist based on SQL rules](https://www.volcengine.com/docs/6491/1927133#fc6b7a54)

* Method 2: [Add a large query circuit breaking resource group](https://www.volcengine.com/docs/6491/1927133#d78b2d8b)


Select the appropriate method based on actual business requirements. The following are usage examples. For details, refer to [Large query defense](https://docs.byteplus.com/docs/E-MapReduce/109153)for configuration adjustments.

<span id="fc6b7a54"></span>
#### **Add an SQL blocklist**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The SQL blocklist feature in StarRocks is disabled by default.</div>


* <div data-tips="true" data-tips-type="warning">The SQL blocklist in StarRocks applies to all users.</div>


* <div data-tips="true" data-tips-type="warning">Both Insert SQL and Select SQL can be intercepted by the blocklist.</div>


1. Enable the SQL blocklist feature.


```SQL
-- 1. Check whether the SQL blocklist is enabled. If not, proceed to the next step
admin show frontend config like '%enable_sql_blacklist%';

-- 2. Dynamically enable the SQL blocklist
admin set frontend config ('enable_sql_blacklist' = 'true');
```



2. Add a blocklist. Only regular expressions are supported for blocklists.


```SQL
-- 1. Create a block rule, for example: ADD SQLBLACKLIST "select count(\*) from .+";
ADD SQLBLACKLIST "<sql_reg_expr>";

-- 2. View the ID and content of the SQL blocklist
SHOW SQLBLACKLIST;

-- 3. Delete the SQL blocklist
DELETE SQLBLACKLIST <sql_index_number>;
```


<span id="d78b2d8b"></span>
#### **Add a large query circuit breaking resource group**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The values in this sample are for reference only. Please refer to your business usage patterns and the metrics of <code>starrocks_audit_db__</code> for reference. It is recommended to conduct comprehensive testing before execution to avoid impacting existing online queries.</div>


```SQL
-- 1. Create a resource group for circuit breaking large queries
CREATE RESOURCE GROUP bigQueryRG
TO 
    (user='rg1_user2', query_type in ('select')),
    (db='db1')
WITH (
    'big_query_cpu_second_limit' = '100',  -- CPU time (seconds) used by the query
    'big_query_scan_rows_limit' = '100000', -- Number of rows scanned by the query
    'big_query_mem_limit' = '1073741824' -- Amount of memory consumed by the query
);

-- 2. View all resource groups
SHOW RESOURCE GROUPS ALL;
```


If a query reaches the resource group limit and returns the error `exceed big query scan_rows limit`, it means the query has been successfully interrupted.

<span id="e186c0dc"></span>
### Separated storage and compute (multi\-warehouse edition)

In the separated storage and compute (multi\-warehouse edition) scenario, the above SQL blocklist and large query circuit breaking resource group features can be used to achieve user\-level isolation within a single compute warehouse, or resource isolation can be achieved by binding different compute warehouses. For details, see: [StarRocks Multi-Warehouse (multi-warehouse) best practices](https://www.volcengine.com/docs/6491/1504734).

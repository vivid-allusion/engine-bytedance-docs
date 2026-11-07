---
title: "workloads"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/workloads"
---

This table displays detailed information about all workloads in the system—that is, query tasks that match resource group rules—including the user associated with the query, the associated resource group, query type, and more. This helps administrators trace the binding relationship between queries and resource groups and troubleshoot abnormal resource usage.

<span id="e93ac108"></span>
## Column name


|Field name |Data types |Explanation of field meanings |
|---|---|---|
|id |UInt64 |It indicates the order of the workload in the system, which is determined by the lexicographical order of the workload name. If a query matches the conditions of multiple workloads, the workload with the smallest id will be selected. |
|name |String |The workload name typically corresponds to the name of the 'select case' rule in the resource group rules, which defines the logic for matching workloads. For example, in the example, 'case_0' is used to associate the workload with the resource group matching rule. |
|resource_group |String |The resource group name used by this workload is directly linked to the `resource_groups` table's `name` field, reflecting the actual resource group assigned to the query task and making it easier to trace the source of resource usage. |
|user |String |The username that triggers the workload (that is, initiates a query) is typically the user's account identifier, such as an email address or username. It is used to locate specific user query behavior and resource usage. |
|query_id |String |Regular expression for the query_id of workload matching queries. |
|query_type |String |For the query type corresponding to the workload, the system outputs the corresponding value based on the type of query you execute:<br><br><br>* DDL: create/drop/alter column<br><br>* DATA: insert/delete/alter partition<br><br>* SELECT: Select type<br><br>* OTHER |
|role |String |Name of the role group to which the user matched to the workload belongs. If a user belongs to multiple roles, or if a role group matches multiple workloads, the system will select according to workload priority, from highest to lowest. |


<span id="21188533"></span>
## Example

```SQL
SELECT * FROM system.workloads; 
```


```SQL
Query id: 339xxxxx-7xxx-4xxx-8xxx-d5xxxxxxxxxx

   ┌─id─┬─name───┬─resource_group─┬─user──────────────────────────────┬─query_id─┬─query_type─┬─role─┐
1. │  1 │ case_0 │ doc_demo       │ xxxxxxxxxxxxx.xxxxx@xxxxxxxxx.com │          │            │      │
   └────┴────────┴────────────────┴───────────────────────────────────┴──────────┴────────────┴──────┘
```

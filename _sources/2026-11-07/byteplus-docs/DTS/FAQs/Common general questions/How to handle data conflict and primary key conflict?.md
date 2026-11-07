---
title: "How to handle data conflict and primary key conflict?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/What_if_a_data_conflict_occurs"
---

This topic mainly applies to DTS (data transmission service) scenarios for troubleshooting and handling data conflicts between the source end and destination during data migration or synchronization tasks. Common conflict manifestations include: data with the same primary key already exists on the destination, simultaneous writes of the same data on both sides in a bidirectional synchronization architecture, or task pause due to primary key conflict caused by task configuration set to "abort on conflict".


<Tabs>
<Tab zoneid="ZElATq5GMu" title="How should I handle a data conflict?">
<TabTitle>How should I handle a data conflict?</TabTitle>

It is recommended to choose strategy based on business requirements for data consistency and task continuity.

In most cases, overwrite on conflict is recommended, allowing the source end data to overwrite the destination data. If ignore on conflict is chosen, both ends retain their own data, which easily leads to data inconsistency and is therefore not recommended for production scenarios. If abort on conflict is chosen, the task will pause upon conflict and requires manual handling, which is more suitable for testing environments or scenarios needing strict manual confirmation. The specific scenarios are shown in the following table:


|**Policy name** |**Recommendation level** |**Description** |
|---|---|---|
|Conflict overwrite |Recommended first<br><br> |When data conflicts occur between the source end and destination, source end data overwrites destination data.<br><br>This meets business expectations in most scenarios but requires careful evaluation of write order in special cases like bidirectional synchronization. |
|Ignore on conflict |Not recommended |Ignore conflicts on conflict, the source end and the destination retain their written data respectively.<br><br>This often causes inconsistent data between the source end and the destination, not recommended for production environments. |
|Abort on conflict |Recommended only in the test environment |The task pauses and reports an error when a conflict occurs, requiring manual intervention to modify the conflicting data before continuing.<br><br>This feature is available on an allowlist basis. to use it, submit tickets. It ensures data consistency but interrupts task continuity. |



* **Why is overwrite on conflict preferred?** 

   In most migration or synchronization scenarios, the source end is usually regarded as the primary source of business data. When a conflict occurs, allowing the source end data to overwrite the destination data generally aligns better with business expectations and ensures the task continues.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Exercise caution when using in bidirectional synchronization scenarios. For example, in the bidirectional synchronization scenario of A and B, if the time A writes data is t1, and the time B writes data is t2 (t1 is later than t2), in the reverse link scenario of A, when the data of B is transmitted to A, it will overwrite the data written by A after t1. Therefore, in bidirectional synchronization scenarios, a comprehensive evaluation combining write order and business rules is required.</div>



* **Why is ignore on conflict not recommended?** 


Ignore on conflict directly skips processing when a conflict occurs, letting both ends retain their respective data. If business requires strict consistency of data on both ends after migration or synchronization, this strategy is not recommended. It can only be considered when business explicitly allows data differences on both ends and the impact of these differences has been fully evaluated.


* **When can abort on conflict be used?** 


This strategy suits scenarios that require manual confirmation of conflicting data and wish to pause the task upon conflict occurrence. After selecting this strategy, DTS will pause the task and abort on conflict. You need to manually resolve conflicting data and manually restart the task once the business verification passes.

The abort on conflict strategy helps detect and block inconsistent data from being written further, but it will also pause migration or synchronization tasks. If conflicts occur frequently during peak business times or critical links, subsequent data transmission may stop, affecting task continuity. Therefore, unless the business explicitly requires manual handling of every conflict, this strategy is not recommended as the priority in production scenarios. Instead, evaluate whether the overwrite on conflict strategy meets business expectations first.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The current abort on conflict strategy is a whitelist feature. To use it, submit tickets for approval.</div>



</Tab>
<Tab zoneid="SgN0k9ydki" title="How should I handle a primary key conflict error?">
<TabTitle>How should I handle a primary key conflict error?</TabTitle>

If the abort on conflict strategy is selected, DTS pauses the task and aborts on conflict when a primary key conflict occurs during execution. At this point, you need to manually resolve conflicting data, complete business verification, and then manually restart the task. A primary key conflict usually indicates the destination already contains data with the same primary key as the source, or that changes writing to the same primary key occurred in the synchronization link. When resolving, first confirm which side's data should be finally retained, then modify according to the business outcome.


</Tab>
</Tabs>

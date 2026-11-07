---
title: "Read/Write separation"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Read_Write_separation_faq"
---

<span id="存在复制延迟的情况，如何保证查询的一致性？"></span>
### How to ensure query consistency in the presence of replication lag?

You can select an appropriate consistency level for the connected endpoint address. NDB for MySQL offers three consistency levels in decreasing order of strictness: global consistency, session consistency and eventual consistency. For details, refer to [Consistency levels](https://www.byteplus.com/en/docs/NDB_for_MySQL/Consistency_levels).

<span id="为什么读取不到刚插入的数据？"></span>
### Why is newly inserted data not immediately available for reads?

This behavior is caused by your endpoint's configured consistency level. NDB for MySQL provides these three consistency level options.


* Eventual consistency: It can not guarantee immediate read access to the latest data, but ensures eventual availability of all updates.

* Session consistency: It provides read\-after\-write guarantees within the same session.

* Global consistency: It guarantees read\-after\-write consistency both within and across sessions.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Higher consistency levels impose greater load on the primary node and degrade performance. Choose with caution.</div>

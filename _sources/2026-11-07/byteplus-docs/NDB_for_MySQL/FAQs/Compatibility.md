---
title: "Compatibility"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Compatibility_faq"
---

<span id=".dmVkYi1teXNxbC3mmK_lkKblhbzlrrnnpL7ljLrniYgtbXlzcWzvvJ8="></span>
### Is NDB for MySQL compatible with MySQL community edition?

NDB for MySQL delivers 100% compatibility with MySQL community edition.

<span id=".5piv5ZCm5pSv5oyBLXBlcmNvbmEt5bel5YW36ZuG77yf"></span>
### Is Percona Toolkit supported?

Yes, but Online DDL is recommended. 

<span id=".5piv5ZCm5pSv5oyBLWdoLW9zdO-8nw=="></span>
### Is gh\-ost supported?

Yes, but Online DDL is recommended. 

<span id=".dmVkYi1teXNxbC3nmoQtcm8t6IqC54K55aaC5L2V5aSE55CGLWRkbC3kuovliqHvvJ8="></span>
### How do RO nodes of NDB for MySQL handle DDL transactions?

When the RW node successfully completes a DDL statement, RO nodes will immediately kill all connections conflicting with DDL MDL locks (typically long\-running queries and large transactions accessing the table) to prevent replication lag from increasing due to MDL lock conflicts. Retry the transaction or query if this error occurs.

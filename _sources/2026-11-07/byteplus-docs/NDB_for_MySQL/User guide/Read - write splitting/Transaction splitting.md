---
title: "Transaction splitting"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Transaction_splitting"
---

By default, the NDB for MySQL database agent sends all requests within a transaction to the primary node to ensure the correctness of the transaction. However, during business development, we sometimes rely on certain frameworks that encapsulate requests into non\-auto\-committed transactions, causing excessive load on the primary node. To solve this problem, NDB for MySQL supports enabling or disabling transaction splitting by editing the read/write endpoint.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Transaction splitting only works for read/write endpoints.</div>


* <div data-tips="true" data-tips-type="tip">The transaction splitting feature is supported only for sessions with the Read Committed transaction isolation level.</div>


* <div data-tips="true" data-tips-type="tip">Only read requests before writes within a transaction can be split out, and <code>select ... for update</code> is also considered a write.</div>


* <div data-tips="true" data-tips-type="tip">Enabling or disabling the transaction splitting function is only effective for new connections. Existing connections retain their original configuration. For operation steps, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Editing_connection_endpoints">Editing connection endpoints</a>.</div>


* <div data-tips="true" data-tips-type="tip">Transaction splitting is not suitable for scenarios with global consistency requirements.</div>



After transaction splitting is enabled, uncommitted transactions are not visible in read\-only nodes according to consistency requirements and isolation levels. Therefore, the database proxy will send all read requests before the first write request in the transaction to the read\-only node, and send the first write request and all subsequent requests to the primary node, thereby reducing the pressure on the primary node.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2b3cf76d5b5eb9356aaf8355e71cfcdf.jpeg) </span>

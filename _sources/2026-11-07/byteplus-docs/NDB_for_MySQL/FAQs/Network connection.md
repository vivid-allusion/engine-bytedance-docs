---
title: "Network connection"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Network_connection_faq"
---

<span id=".5Li65LuA5LmI5peg5rOV6L-e5o6l5pWw5o2u5bqT77yf"></span>
### Why is the database connection failing?

If you encounter database connection failures, verify the following.


* Verify whether the instance status is **Running**.

* Verify whether [Create account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts) operation is completed for the instance?

* Verify whether the [IP allowlist](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_allowlist) is configured.

* For private network connections, ensure the ECS instance and database instance reside with the same VPC.


If the instance remains inaccessible after troubleshooting, [Submit a support ticket](https://console.byteplus.com/workorder/create) for technical assistance.

<span id=".5ZyoLWVjcy3kuK3kvb_nlKgtbXlzcWwt5a6i5oi356uv6L-e5o6lLXZlZGItbXlzcWwt5a6e5L6L5pe25pS25Yiw6ZSZ6K-v5o-Q56S6LWFjY2Vzcy1kZW5pZWTjgII="></span>
### Receiving `Access denied` error when connecting from ECS to NDB for MySQL instances using MySQL client.

If encountering this error when connecting via MySQL client from ECS, first check whether the ECS IP is in the database allowlist. For more information on allowlist creation, refer to [Creating allowlists](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_allowlist).

```sql
ERROR 1045 (28000): Access denied for user 'example'@'192.168.xxx.xxx' (using password: IP NOT IN white List)
```


&nbsp;

<span id=".ZWNzLeWSjC12ZWRiLW15c3FsLeWunuS-i-S4jeWcqOWQjOS4gOS4qi12cGPvvIjnp4HmnInnvZHnu5zvvInlhoXvvIzlj6_ku6Xot6gtdnBjLeiuv-mXruWQl--8nw=="></span>
### If ECS and instances are not in the same VPC (private network), is cross\-VPC access supported?

Yes. To enable private connectivity between VPCs, first configure Cloud Enterprise Network. For steps, refer to [Quick start](https://docs.byteplus.com/en/docs/cen/Quick-Start).

<span id="XYQVBZ0M"></span>
### How to automatically kill long\-running sessions?

Currently, NDB for MySQL offer two solutions for automatically killing long\-running sessions:


1. By modifying the `kill_idle_transaction` parameter, you can control the execution time of idle transactions. For more information, refer to [Modifying parameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_parameters).

2. DBW supports continuously killing requests that exceed the threshold. For more information, refer to [Session management](https://docs.byteplus.com/en/docs/DBW/Session_information_management).

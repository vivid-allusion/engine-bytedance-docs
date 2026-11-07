---
title: "Security"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Security_faq"
---

<span id="vedb-mysql-实例必须设置白名单吗？"></span>
### Is an allowlist required for instances?

Yes. New instances have no allowlist associations by default, blocking all IP access.

<span id="单个实例最多可以绑定多少个白名单？"></span>
### What is the maximum number of allowlists a single instance can be associated with?

Each instance supports a maximum of 100 allowlists and 1,000 IP addresses or IP address segments in total.

<span id="每个白名单最多包含多少个-ip-或者-ip-段？"></span>
### What is the maximum number of IP addresses or IP address segments allowed in a single allowlist?

A single allowlist can contain up to 300 IP addresses or IP address segments.

<span id="一个白名单支持绑定到多个实例吗？"></span>
### Can a single allowlist be associated with multiple instances?

Yes. A single allowlist can be associated with up to 50 instances maximum.

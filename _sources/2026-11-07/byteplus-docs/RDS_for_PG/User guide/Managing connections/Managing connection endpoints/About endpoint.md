---
title: "About endpoint"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/about_connection_endpoints"
---

The connection endpoint is a network proxy service located between the database and the application. It handles all requests when the application accesses the database, featuring high availability, high performance, manageability, and ease of use, and supports advanced functions such as read/write separation and load balancing. RDS for PostgreSQL provides two types: the default endpoint and customized read\-only endpoints. For more details about endpoints, refer to the table below.


|Endpoint type |Creation method |Read/Write type |Note |
|---|---|---|---|
|Default endpoint |Created by default when creating instance, manual creation is not allowed |Read/Write |Connect all nodes except the standby node. If Read/Write separation is disabled, the Default endpoint connects to the Primary node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Read/Write function of the Default endpoint is disabled by default. To enable it, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_or_disabling_read-write_splitting">Enabling Read/Write separation</a>.</div><br> |
|Customized Read\-only node |Manual creation |Read\-only |Connects only to read\-only nodes; creation is not allowed if no read\-only nodes exist. A customized read\-only endpoint can bind to only one read\-only node and does not support re\-binding to other read\-only nodes after binding. One read\-only node can be associated with multiple customized read\-only endpoints. You can create a maximum of 10 customized endpoints on an instance. Without creating a customized Read/Write endpoint, you can create up to 10 customized read\-only endpoints. |
|Customized Read/Write node |Manual creation |Read/Write |An instance supports creating only one customized read/write endpoint at most. The customized read/write endpoint currently connects only to the primary node. |

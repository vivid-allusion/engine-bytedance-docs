---
title: "About connection endpoints"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/about_connection_endpoints"
---

A connection endpoint is a network proxy service provided by RDS for MySQL, which is located between the database and applications. Based on their functions, connection endpoints are divided into two types: proxy endpoints and direct endpoints. Connections via proxy endpoints pass through a proxy, enabling features such as Read/Write separation, load balancing, wait_timeout, and multi\-statements mode. Connections via direct endpoints connect directly to the corresponding node and cannot use proxy\-related features.

Connection endpoints are classified as default endpoints and customized endpoints based on their creation time. The default endpoint is a connection endpoint in Read/Write mode that is automatically created during instance creation. Users can create a customized endpoint after the instance is created to customize its Read/Write mode and other functions for their business needs.

The functional differences between proxy endpoints and direct endpoints are shown in the table below.

| |Proxy endpoint |Direct endpoint |
|---|---|---|
|Supported quantity |10 (including the default endpoint) |10 (including the default endpoint) |
|Supported Read/Write mode |Read/Write mode and read\-only mode |Read/Write mode and read\-only mode |
|Associated nodes |* Read/Write proxy endpoint: Can be associated with only the primary node or with the primary node and up to 10 read\-only nodes.<br><br>* Read\-only proxy endpoint: Can only be associated with a minimum of 1 and a maximum of 10 read\-only nodes. |* Read/Write direct endpoint: Can only be associated with the primary node.<br><br>* Read\-only direct endpoint: Can only be associated with one read\-only node. |
|Private network access |Support |Support |
|Public network resolution |Support |Support |
|Public network access |Support |Support |
|Connection pool |Transaction\-level connection pool and direct connection modes. |Not support |
|Wait_timeout |Support |Not support |
|Automatically add new nodes |Support |Not support |
|Read/Write separation |Support |Not support |
|Multi\-Statements mode |Support |Not support |
|Overload protection |Support |Not support |
|Read request scheduling policy |Support |Not support |
|Weight allocation policy |Support |Not support |
|Read\-only latency threshold |Support |Not support |
|Transaction splitting |Support |Not support |
|Connection persistence |Support |Not support |
|SQL forwarding |Support |Not support |

> **warning**

* > Multi\-node instances automatically create three proxy endpoints during instance creation: the default endpoint, the Write endpoint, and the Read\-only endpoint. The default endpoint is associated with all nodes of the instance. The Write endpoint is associated only with the primary node. The Read\-only endpoint is associated with all secondary nodes by default, and it can be associated with a minimum of one and a maximum of all secondary nodes. The default endpoint and the write endpoint do not support adjusting associated nodes.

* > The default endpoint, write endpoint, and read\-only endpoint cannot be deleted. The type, Read/Write mode, automatically add new nodes, and read request scheduling policy for these three endpoints cannot be adjusted. The "Automatically add new nodes" feature is enabled by default for the default endpoint and read\-only endpoint, and disabled for the write endpoint. The default read request scheduling policy is round robin scheduling, where the system distributes new connections to associated nodes based on their configured weights.

* > Use the default endpoint for Read/Write separation services, the write endpoint for write services, and the read\-only endpoint for read\-only services.

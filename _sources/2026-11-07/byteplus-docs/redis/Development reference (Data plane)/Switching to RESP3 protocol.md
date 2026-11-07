---
title: "Switching to RESP3 protocol"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/switch-RESP3-protocol"
---

By default, Cache for Redis instances use the RESP2 protocol after creation. You can switch to the RESP3 protocol using the HELLO command.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

The Redis serialization protocol (RESP) is a protocol for communication between Redis clients and Redis databases. It has the characteristics of easy recognition, simple implementation process, and strong parsing performance. It can serialize different data types such as integers, strings, and arrays, and has specific types for errors. The client sends requests to the Redis server in the form of a string array. The array content includes commands to be executed by the server and corresponding parameters. The data type returned by the server is determined by the specific command. RESP is binary\-safe, using prefix lengths to transmit bulk data without processing bulk data transferred between processes. For more details about the Redis serialization protocol, refer to [Redis serialization protocol specification](https://redis.io/docs/latest/develop/reference/protocol-spec/).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* To switch to the RESP3 protocol, your Redis instance version must meet the following requirements:

   * The database version must be Redis 6.0 or 7.0.

   * The minor version of proxy must be greater than or equal to `1.502.0`.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view the instance's database version and minor version information under the <strong>Summary</strong> tab. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/redis/view-instance">Viewing instance information</a>.   </div>
   

* Redis clients need to support the RESP3 protocol.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Switching to the RESP3 protocol using the HELLO command only takes effect on the current connection. New connections still use the RESP2 protocol by default.

<span id=".6YCa6L-HLWhlbGxvLeWRveS7pOWIh-aNoi1yZXNwMy3ljY_orq4="></span>
## Switching to RESP3 protocol using HELLO command

In the client command that has successfully connected to the Redis instance, enter the following command to switch the communication protocol to RESP3.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can select a suitable tool to connect to the Redis instance according to the business scenario. For specific procedure, refer to:</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/redis/connect-instances-through-redis-cli">Connecting to instance via Redis\-cli</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/redis/connect-instance-via-client">Connecting to instance via client application</a></div>



```Bash
Hello 3
```


When you see `"proto" => (integer) 3` in the returned result, it indicates that the current connection has been successfully switched to the RESP3 protocol. For more details about returned results, refer to [Client handshake](https://redis.io/docs/latest/develop/reference/protocol-spec/#client-handshake).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_95b6edd2e97aef42ec4c8516b08e64d5.png) </span>

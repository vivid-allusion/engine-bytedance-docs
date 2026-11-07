---
title: "List of modifiable parameters"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/List_of_modifiable_parameters"
---

Table Storage for HBase supports custom values for some parameters. This topic describes the customizable parameters for HBase instances.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Modifying some parameters causes the instance to restart automatically. The new parameter values take effect after the instance restarts. Instance restart will cause connection interruption. It is recommended to modify relevant parameters during off\-peak business hours and ensure that the business has a reconnection mechanism. To modify parameter values, see [Modifying parameters](https://docs.byteplus.com/en/docs/HBase/Modifying_parameters).

<span id=".5Y-C5pWw5pSv5oyB6KGo"></span>
## Parameter support


|Parameter |Default value |Value range |Unit |Need to restart |Description |
|---|---|---|---|---|---|
|`hbase.client.keyvalue.maxsize` |10485760 |10485760~52428800 |Byte |No |Set the maximum number of KeyValue bytes supported by the client. |
|`hbase.server.keyvalue.maxsize` |10485760 |10485760~52428800 |Byte |No |Set the maximum number of KeyValue bytes supported by the server. |
|`hbase.hregion.majorcompaction` |604800000 |0~604800000 |ms |Yes |Set the execution period of major compaction. |

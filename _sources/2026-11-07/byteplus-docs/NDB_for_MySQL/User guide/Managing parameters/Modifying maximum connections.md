---
title: "Modifying maximum connections"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_maximum_connections"
---

For a system with high concurrent business needs, a sufficient number of connections are required to ensure that users can access the database. Therefore, it is supported to modify the maximum number of connections through the console and API to meet the scenario of increasing the number of connections. This topic describes how to modify the max connections for instance.

<span id="注意事项"></span>
## Precautions


* Supported versions: MySQL 5.7, MySQL 8.0.

* The default max connections value varies with different instance specifications, so the max connections value changes when you modify primary/read\-only node specifications. However, if the max connections have been previously modified, the value will not change in the event of a subsequent specification modification to the instance. At this time, you need to manually modify the max connections to a reasonable value. If the max connections value is not modified, it will likely be too high if you downgrade an instance, which can cause memory overflow.


<span id="变更影响"></span>
## Change impact

Database connections use memory and CPU resources, and the more connections there are, the more resources are exhausted. When setting max connections, you need to consider the availability of database resources and set it carefully. If `max_connections` is set too high, it will likely cause memory overflow. Therefore, we recommend you use the default maximum connections of instances, so as to avoid database performance degradation caused by unreasonable connection configurations and the impact on the stability of instance operations.

<span id="参数说明"></span>
## Parameter description


|Parameter |Description |Need to restart |
|---|---|---|
|**max_connections** |The maximum connections for the entire database, that is, the sum of all database account connections, with no distinction made between users. The value range is [100\-100000]. The default maximum number of connections varies for instances of different specifications. For more information, see [Product specifications](https://www.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications). If the total connections exceed the maximum number, the system reports an error, and new connections cannot be established. |No |
|**max_user_connections** |Maximum number of connections for a single database user. Value range [0\-4294967295], the default value is`0`, which means there is no limit. If the connections from the same account exceed the maximum value, the system reports an error, and new connections cannot be established. |No |


<span id="修改方式"></span>
## Modification method


* **Modify via console**

   Log in to the [console](https://console.byteplus.com/db/vedb-mysql) and modify the maximum number of connections on the **Parameters** tab. Refer to [Modifying parameters](https://www.byteplus.com/en/docs/NDB_for_MySQL/Modifying_parameters) for specific instructions.

* **Modify by calling the API**

   Call the API to modify the maximum number of connections. For details, see [ModifyDBInstanceParameters](https://www.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceParameters).


After the modification is complete, you can check whether the modified maximum connection parameter value has taken effect in the **Parameter modification history** subtab. For details, see [Viewing parameter modification history](https://www.byteplus.com/en/docs/NDB_for_MySQL/Viewing_parameter_modification_history).

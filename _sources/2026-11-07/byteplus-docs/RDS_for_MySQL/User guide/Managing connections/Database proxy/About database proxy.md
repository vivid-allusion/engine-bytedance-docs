---
title: "About database proxy"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/about_database_proxy"
---

<span id="function-description"></span>
## Function Description

Database agent is a network proxy service provided by RDS for MySQL that is located between the database server and the application server. It is used to proxy all requests from the application server to access the database. The Database agent function provided by RDS for MySQL supports [read-write separation](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_or_disabling_global_read-only), [multiple connection endpoints](https://docs.byteplus.com/en/docs/RDS_for_MySQL/managing_connection_endpoints), [connection pool](https://docs.byteplus.com/en/docs/RDS_for_MySQL/about_connection_pool_mode) and other functions, after turning on the database agent function, it can effectively reduce the load of the primary node, making the instance have the functional advantages of high availability, high performance, and easier use.

The functional differences of instances before and after the database agent function is enabled are as shown in the following table:


|Function |Turn on the database agent function |Turn off the database agent function |
|---|---|---|
|Connection pooling mode |You can choose transaction\-level connection pooling or direct connection mode connection pooling. |Only direct connection mode connection pool can be used. |
|Read and write separation function |Supported. |Not supported. |
|Adjust the nodes associated with the connection terminal |Supported. |Not supported. |
|Custom terminal's automatic addition of new nodes function |Supported. |Not supported. |
|Agent Monitoring |Supported. |Not supported. |


<span id="scenes-to-be-used"></span>
## Scenes to be used

When your business covers the following scenarios, it is recommended to use the database agent function:


* A large number of read requests within the transaction make the load on the master node too high.

* Too many connections cause the instance load to be too high.

* There are a large number of short connections in the business.

* Business needs to separate reading and writing.


<span id="fee-description"></span>
## Fee Description

The database proxy function has started to be billed at 00:00:00 (Beijing time) on December 30, 2024. For detailed billing information about the database proxy function, see [Billing items and prices](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If your instance has enabled the database proxy service before December 30, 2024, and has not changed the configuration of the database proxy service, the database proxy function of your instance will not be charged. However, your database proxy service only has basic functions. If you need to use the complete database proxy function and experience the new proxy\-related features that are continuously added, please enable the full version of the database proxy service. There are two ways to enable the full version of the database proxy service:</div>



* <div data-tips="true" data-tips-type="tip">Close and restart the database proxy service. For details on related operations, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/disable_database_agent">Disabling the database agent</a></div>


   <div data-tips="true" data-tips-type="tip">[Changing the agent configuration] and <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent">Enabling the database agent</a>.   </div>
   

* <div data-tips="true" data-tips-type="tip">Change the configuration of the database proxy service at that time. For details on related operations, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_agent_configurations">Changing the agent configuration</a>.</div>



<span id="instructions"></span>
## Instructions


* [Enable database agent](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent)

* [Turn off database agent](https://docs.byteplus.com/en/docs/RDS_for_MySQL/disable_database_agent)

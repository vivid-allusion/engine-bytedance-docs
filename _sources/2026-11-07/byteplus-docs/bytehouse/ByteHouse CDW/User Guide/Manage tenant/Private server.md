---
title: "Private server"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/private-server"
---

**Private server** is a **dedicated computing resource** solution provided by ByteHouse CDW, which allocates independent computing nodes (Server) to users, ensuring resource isolation, performance assurance, and higher flexibility.

<span id="3743ba9d"></span>
# Background information

<span id="5ad47062"></span>
## Function overview

**Private Server** is the core executive unit of ByteHouse CDW, responsible for receiving user query requests, conducting SQL analysis and optimization, and distributing query tasks to execution nodes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/509e9fa74c34486bbff2d359924fc71b~tplv-goo7wpa0wc-image.image) </span>


* SQL Analysis and Execution: Receives SQL query requests, completes syntax and semantic analysis, and generates an execution plan.

* Query Scheduling: Determines the optimal execution path by combining the query optimizer and execution engine to achieve efficient query performance.


<span id="44aac3b0"></span>
## Application scenarios

In a shared resource architecture, multiple users share the same Server computing resources. If a user's query task is too heavy, it may affect the query performance of other users. This  **"resource contention"**  issue is more pronounced in large\-scale concurrent queries and complex analysis tasks.


|Scenes |Shared Server Mode |Private Server Mode |
|---|---|---|
|High concurrent queries |Query Latency increases, and resource contention may occur |Each user has independent private server resources to avoid resource contention |
|Large\-scale data analysis |Complex query tasks may affect the query performance of other users |Private server nodes ensure complex query tasks do not affect other users |


Therefore, a private server is suitable for:


* **Scenes**: High\-concurrency point checks, high QPS, large\-scale data analysis, security compliance, etc.; current supported concurrency capability: 10,000 QPS.

* **Suggestion**: When your compute group specifications exceed the XL size (64 core 256 GB), we recommend that you activate a private server to obtain stable and reliable query performance.


Example Scenario:


* **Scenario 1, Real\-time analysis and high concurrency query**: Business scenarios such as Internet, gaming, e\-commerce, and advertising require handling high concurrency queries. An exclusive Server provides isolation and elastic scaling, delivering stable performance assurances for users.

* **Scenario 2, Sensitive data analysis in the finance industry**: Financial institutions have high security and isolation requirements for data. A private server can meet compliance requirements.

* **Scenario 3, Enterprise\-level big data analysis**: Enterprise users need to handle a large volume of query analysis tasks during peak business periods. A private server provides stable performance and elastic scaling capabilities.


<span id="5a2806cc"></span>
## Performance metric


|**Engine version** |**Private server specifications** |**Point\-click QPS capability (QPS/S)**  |
|---|---|---|
|2.2+ |32 cores 128GiB \* 2 nodes |8000 ～ 12000 |


<span id="4e62e17b"></span>
## Billing


* Pricing and Billing: The private server currently supports four specifications, meanwhile supporting **prepaid (recommended)**  and **postpaid** two billing modes. The specification & pricing and billing details for both modes can be found in the [Computational resources](https://docs.byteplus.com/docs/bytehouse/specifications-and-pricing#cadb49e9) section.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The private server is currently at the "tenant"\-"environment" level. A tenant in one region under a single environment needs only to activate one private server cluster; at present, a private server cluster supports the purchase of 2 nodes, and horizontal scaling capabilities are coming soon. Stay tuned...   </div>
   

* Settlement/Renewal, Arrears, Unsubscription: The settlement, renewal cycles for the private server are independent from public compute groups but are logically similar. For more details, please refer to the product billing document.


<span id="640a355c"></span>
# Prerequisite


* If you need to enable a private server simultaneously when initially enabling ByteHouse, you must have an AccountAdmin role to log in and enable the service.

* If you are enabling a private server separately via the ByteHouse Console, you must have either an AccountAdmin or SystemAdmin role to enable the service.

* For more details regarding roles and users, please see [Role management](https://docs.byteplus.com/docs/bytehouse/docs-access-control-administration).


<span id="e03f1580"></span>
# Activate private server

You can activate the private server when you first activate ByteHouse or support the subsequent independent activation of the private server for users who have activated ByteHouse.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After activating the private server, user queries will switch from the computing group (public Server) to the private server. The entire process takes about 5 minutes, please wait patiently.</div>


<span id="cc6eeb5c"></span>
## First\-time activation of ByteHouse

Activation path: Enter [ByteHouse Product Home Page](https://www.byteplus.com/en/product/bytehouse), when buying ByteHouse CDW for the first time, you can simultaneously activate a private server.


* At the initial activation, the system will by default use the created compute group as the default write compute group for the dedicated Server. If multiple compute groups are activated at the same time, the system will use the first compute group as the default write compute group.

* You can purchase the appropriate specifications according to business needs, currently supporting both pay\-as\-you\-go and monthly payment modes.

* When activating a private server later, you must simultaneously select the write compute group associated with the current private server.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The writing calculation group bound to the private server must turn off the automatic start and stop settings of the calculation group. You can edit the purchased computing group to modify the automatic start and stop settings of the computing group.</div>


<span id="6f0b09c9"></span>
## Activation through the console

**Prerequisites:** 

Before activating a dedicated Server separately through the console, you must confirm that you have set the default write compute group, as shown in the following figure.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/332cfe89ed314635abfa47faee4b972a~tplv-goo7wpa0wc-image.image) </span>

If not yet configured, you may follow the steps below.

Set the default write compute group via **Tenant management \> Parameter setting** path. Once set, the subsequent activation of a dedicated Server through the console will be bound to the default compute group set here.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3c60b3ee03f479f9fd22c5df3d128c8~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To set a compute group as the default writing group for a dedicated Server, disable its automatic start\-stop settings. You can refer to <a href="https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse#7190221b">Edit Virtual Warehouse Configuration</a> to change the automatic start and stop settings of the compute group.</div>


**Steps:** 


1. After logging into the ByteHouse console, click the **Tenant Management** tab, and at the **Basic Information** \> **Private Server** module, click **Create one now**.

2. In the pop\-up sidebar, configure the private server's payment type, specifications, and other parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a412a678cca4a109bc4fce4fb7c544b~tplv-goo7wpa0wc-image.image) </span>

   When purchasing, you can buy the appropriate specifications according to business needs. It currently supports both pre\-paid and post\-paid modes.

3. After completing the purchase according to the interface, the private server that has been opened starts Initialization, and the status of the private server becomes "Pending".

   The entire initialization process takes about 5 minutes, please wait patiently.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1384ae76f28e4b9a8c8285ba80ef15be~tplv-goo7wpa0wc-image.image) </span>

4. Once the private server initialization is complete, the status changes to "Running".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/563301c8e074490f92404be86a13d890~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After activating the private server, user queries will automatically switch from the computing group (public Server) to the private server.   </div>
   

<span id="45ff32e3"></span>
# Scale up the private server

If the specifications of the current private server do not meet your needs, you can click the **Edit** button in the row of the private server and configure the specifications of the private server in the pop\-up sidebar. Currently, only upward scaling is supported.

<span id="43a76e9e"></span>
# View private server monitoring

After creating a private server, you can view the monitoring metric data of the private server on **Tenant management** \> **Cloud monitor** page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/360454a66db64bd694ba42a0dac9bded~tplv-goo7wpa0wc-image.image) </span>

For details about the currently supported private server monitoring metrics and operation guidelines for creating monitoring and alarms via BytePlus Cloud Monitor, please refer to [Monitoring and alarm](https://docs.byteplus.com/docs/bytehouse/monitoring-and-alarm).

<span id="e33ebb5a"></span>
# Unsubscribe from private server

If you wish to unsubscribe from the private server later, you can click the **Delete** button after the private server in **Tenant Management\>Basic Information\>Private Server**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/909e3b1736224bed9d5013b3abe3d625~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After unsubscribing from the private server, user queries will switch from the private server to the public server; this process takes some time, currently around 5 minutes.</div>


* <div data-tips="true" data-tips-type="warning">The billing, renewal, and cancellation periods of the private server are independent from the public computing groups but are logically similar; more details can be seen in the <a href="https://docs.byteplus.com/docs/bytehouse/specifications-and-pricing#cadb49e9">Computational resources</a> document.</div>

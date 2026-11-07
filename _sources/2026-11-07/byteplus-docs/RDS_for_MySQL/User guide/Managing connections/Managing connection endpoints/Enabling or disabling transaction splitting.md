---
title: "Enabling or disabling transaction splitting"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Transaction_splitting"
---

By default, the database proxy sends all requests in a transaction to the primary node to ensure transaction correctness. However, some frameworks encapsulate all requests into non\-autocommit transactions (by disabling autocommit with `set autocommit=0;`), which overloads the primary node. To address this, RDS for MySQL provides a transaction splitting feature. This feature splits requests within a transaction by routing read requests that occur before the first write request to a read\-only or secondary node, reducing the load on the primary node.

<span id="注意事项"></span>
## Precautions


* Only proxy endpoints in Read/Write mode support transaction splitting.

* Only implicit transaction splitting is supported for transactions where `autocommit=0`.


<span id="前提条件"></span>
## Required


* An instance has been created and the instance state is **Running**. For more details, refer to [Create instance](https://www.volcengine.com/docs/6313/75366).

* The database proxy is enabled for the instance, and a connection endpoint in Read/Write mode has been created. For details about enabling the database proxy and creating a connection endpoint, refer to [Enable database proxy](https://www.volcengine.com/docs/6313/1215510) and [Create endpoint](https://www.volcengine.com/docs/6313/133043).


<span id="操作步骤"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. In the left navigation bar, choose MySQL \\> Instance list.

4. On the **Instances** page, click the target instance name.

5. At the top of the page, click the **Connectivity** tab.

6. On the **Connectivity** page, in the **Endpoints** list, click **Edit** in the **Actions** column for the target connection endpoint to open the **Modify endpoint** page.

7. On the **Modify endpoint** page, enable or disable transaction splitting, and then click **OK**.

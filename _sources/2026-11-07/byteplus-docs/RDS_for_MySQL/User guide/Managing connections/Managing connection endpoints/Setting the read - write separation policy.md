---
title: "Setting the read/write separation policy"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_read-write_splitting_policies"
---

This topic describes how to set the read/write separation policy for connection endpoints.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

The read/write separation strategy for a connection endpoint supports two methods: round robin scheduling and connection schedule. The default is round robin scheduling.


* **Connection schedule**

   When connection schedule is used, the system automatically distributes new connections to nodes with lighter loads based on the node's active request volume and response time.

* **Round robin scheduling**

   When round robin scheduling is used, the read load of each node in a connection endpoint depends on its custom read request weight. RDS for MySQL schedules new connections to the associated nodes in a round\-robin manner based on the weight configuration. For example, if an instance has three read\-only nodes with read weights of 100, 200, and 200, the read requests are processed by these nodes in a 1:2:2 ratio.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance has been created and the instance state is **Running**. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* Read/Write separation is enabled. For the procedure, refer to [Enabling or disabling read/write separation](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_read-write_splitting).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If your instance's read/write separation strategy does not include the Connection schedule option, you can [submit a ticket](https://console.byteplus.com/workorder/create) to technical support to request an instance version upgrade.

* When read/write separation is disabled, you can set the Read request scheduling policy, Weight allocation policy, and Read\-only latency threshold, but these settings only take effect when read/write separation is enabled.

* Multiple\-node instances only support round robin scheduling for the read request scheduling policy and automatic assignment for the Weight allocation policy.

* Single\-node instances do not support read/write separation.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.</div>



3. In the left navigation pane, click **Instances** to go to the **Instances** page.

4. On the **Instances** page, click the name of the target instance to enter the instance.

5. On the target instance page, click **Connectivity**.

6. In the **Endpoints** list on the **Connectivity** tab, click **Edit** in the **Actions** column for the target connection endpoint to open the **Modify endpoint** page.

7. On the **Modify endpoint** page, in the **Advanced configuration** section, set the **Read request scheduling policy**. It can be set to **Round robin scheduling** or **Connection schedule**.

   * Set it to Connection schedule. Click **Load scheduling**, and then click **OK**.

   * Set to Round robin scheduling.

      1. Click **Round robin scheduling**.

      2. In the **Weight allocation policy** area, set the weight allocation policy and click **OK**. Set to **Automatic assignment** or **Custom assignment**.

         * Automatic assignment

            The system automatically assigns weights to each node based on the specifications of the nodes associated with the connection endpoint.

         * Custom assignment

            When you select Custom assignment, the page displays all nodes associated with the connection endpoint, allowing you to set the Read request weight for each node in the list. The default weight is automatically calculated based on the node specification. Weight value ranges from 0 to 10000 and must be an integral multiple of 100.

            <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="4">tip            </div>
            

            <div data-tips="true" data-tips-type="tip" data-wrapper-indent="4">Set the weight according to the proportion of node specifications to prevent uneven node pressure from wasting resources.            </div>
            

<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[ModifyDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbendpoint) |Call the ModifyDBEndpoint API to modify an Endpoint. |

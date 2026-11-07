---
title: "Set consistency level"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Set_consistency_level"
---

This topic describes the three consistency levels supported by RDS for MySQL and their applicable scenarios. You can select an appropriate consistency level based on your business requirements.

## Introduction to consistency

RDS for MySQL supports distributing read requests to read\-only nodes through read/write separation to improve read performance. However, when primary\-replica replication has high latency, reading data from read\-only nodes may fail to meet the user's consistency requirement of "read\-after\-write". To address data consistency requirements, MySQL supports three consistency levels: **Global consistency**, **Session consistency**, and **Eventual consistency**. You can select an appropriate level based on your business requirements for data consistency and read performance.

### Eventual consistency

#### Function introduction

RDS for MySQL uses the eventual consistency level by default. At this level, read requests are sent directly to read\-only nodes to fully utilize the traffic distribution capability of read/write separation. If high primary\-replica replication latency exists, the latest data may not be available immediately after writes. However, consistent data can eventually be read once data synchronization completes.

#### Use cases

It applies to business scenarios that aim to reduce pressure on the primary node and do not impose strict requirements on real\-time data consistency.

### Session consistency

#### Function introduction

Session consistency ensures read\-after\-write within the same session. This mode routes based on session GTID positions. It prioritizes distributing read requests to read\-only nodes that have caught up to the corresponding positions. If read\-only nodes fail to catch up within the configured timeout period, read requests are forwarded to the primary node for reading or return an error message in accordance with the timeout policy. It meets the data consistency requirements within the same session while using read\-only nodes to share read pressure.

#### Use cases

It applies to business scenarios that require guaranteed read\-after\-write within the same session and want to offload read request pressure through read\-only nodes.

### Global consistency

#### Function introduction

Global consistency ensures that all read requests query the globally latest data. This mode routes based on the global GTID position and prioritizes distributing read requests to read\-only nodes that have caught up to the global position. This approach ensures that read requests can retrieve data updated by all sessions. It prevents differences in data visibility between different sessions caused by primary\-replica replication latency, thereby achieving global data consistency.

#### **Use cases**

It applies to business scenarios with logical dependencies between different sessions, where each session must read fully consistent data.

## Precautions

* When setting the consistency level, the instance must be in the running state.

* Only connection endpoints with an **Endpoint type** of **Proxy endpoint** and a **Read/Write mode** of **Read/Write** support setting the consistency level.

* After you modify the consistency level, the change takes effect only for newly arriving read requests. It does not affect established connections or requests that have already been issued.

* When you change the consistency level to session consistency or global consistency, the proxy waits for read\-only nodes to synchronize GTID positions (the maximum waiting time is the consistency read timeout period), which may increase read request latency.

* When read\-only nodes have replication latency, global consistency may route more read requests to the primary node, increasing primary node load and further raising business latency. It is recommended for read\-heavy and write\-light scenarios, and the switch is recommended during business off\-peak hours.

* When the timeout policy is set to **Return error**, an error message is returned to the application upon timeout, and the business must support retries. When **Switch to primary node** is selected, the load capacity of the primary database needs to be evaluated.

## Procedure

### Set When Creating an Endpoint

You can set the consistency level when creating an endpoint. For specific operations, see [Create an Endpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_connection_endpoints?lang=en).

### Set for an existing connection endpoint

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project to which the instance belongs is not set, this operation should select the project as **All resources**.

3. On the left navigation bar, click **Instances** to go to the **Instances** page.

4. Click the name of the target instance on the **Instance list** page to go to the **Instance information** page.

5. On the **Summary** page, click the **Connectivity** tab to enter the **Connectivity** page.

6. In the **Endpoints** list on the **Connectivity** tab, click **Edit** in the **Actions** column for the target connection endpoint to open the **Edit endpoint** page.

7. On the **Edit endpoint** page, in the **Read/Write separation configuration** section, enable the **Read/Write separation** switch, and set the **Consistency level, Consistent read timeout,**  and **Timeout policy** parameters **.**

|**Parameter** |**Description** |
|---|---|
|Consistency level<br><br> |Select one of the following levels based on your business scenario:<br><br><br>* Eventual consistency (Default value).<br><br>* Session consistency.<br><br>* Global consistency.<br><br><br>> **tip**<br><br><br>> For the application scenarios of Eventual consistency, Session consistency, and Global consistency, refer to [Consistency introduction](https://docs.byteplus.com/en/docs/RDS_for_MySQL/set-consistency-level?lang=en#9yKTOGwS).<br> |
|Consistent read timeout<br><br> |Sets the maximum time for the proxy to wait for read\-only nodes to catch up to the target data position. The default value is 10 ms. The value range is 0~60,000, and the unit is ms (milliseconds). When this parameter is set to 0, no waiting is required.<br><br>> **tip**<br><br><br>> This parameter can only be configured when the **consistency level** is set to **Session consistency** or **Global consistency**.<br> |
|Timeout policy |Set the method used by the proxy to handle read requests when the read\-only node fails to catch up with the target position within the timeout period. Values are as follows:<br><br><br>* **Switch to primary node** (Default value): Forwards read requests to the primary node. This approach may increase the load on the primary node.<br><br>* **Return error**: Returns an error message. It is recommended that your application has a retry mechanism.<br><br><br>> **tip**<br><br><br>> This parameter can only be configured when the **consistency level** is set to **Session consistency** or **Global consistency**.<br> |

8. Read and select **Important risk notice**, and click **OK**.

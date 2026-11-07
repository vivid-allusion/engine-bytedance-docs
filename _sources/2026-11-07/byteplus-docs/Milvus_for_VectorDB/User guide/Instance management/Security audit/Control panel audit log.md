---
title: "Control panel audit log"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Control_panel_audit"
---

Milvus for VectorDB now integrates with Volcengine Operation Audit Service. The operation audit service records operation events related to Milvus for VectorDB, facilitating subsequent queries, audits, and reviews. This topic describes how to view control panel audit events.

## Precautions

Currently, only Dedicated and Serverless instances support control panel audit logs.

## Procedure

Control panel audit is enabled by default. It records operation events such as instance changes and query instances to the operation audit service. You can view audit logs directly in the Milvus for VectorDB console.

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select the project and region of the instance in the top menu bar.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instance list** in the left navigation pane.

4. In **Instances**, select the **Dedicated** or **Serverless** tab, then click the instance name of the target instance.

5. Select the **Control plane audit** tab and filter audit events by time, user name, event name, and other criteria.

   > **tip**

   * > You can quickly filter logs from nearly 1 hour, nearly 1 day, and nearly 1 week.

   * > Action audit only provides events within 90 days.

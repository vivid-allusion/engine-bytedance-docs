---
title: "Node specification auto scaling management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Auto_scaling_management"
---

Database Workshop (DBW) provides the node specification auto scaling feature. When business load changes, this feature can quickly respond and perform scaling operations to ensure system stability and meet dynamic business needs. This topic describes how to enable, view, modify, and disable the node specification auto scaling feature.

## Prerequisite

* An NDB for MySQL instance has been created, and the instance state is Running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For details, refer to (veDB  [Enabling instance security control (NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control?lang=en) and  [](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket?lang=en)[](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket?lang=en)[](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket?lang=en).

## Precautions

* Currently, only instances with kernel versions 3.0.x.x and 2.0.x.x support node specification scaling.

* Scaling operations may interrupt OnlineDDL tasks in progress within the instance. Proceed with caution.

* During scaling, the database instance may experience brief connection interruptions.

* Automatic scaling\-up rules and automatic scaling\-down rules are independent of each other and can be configured separately without mutual interference.

* Before using the AutoOps function, make sure that there is sufficient balance in the account to support changing the instance configuration. For more billing information about the product, see [Billing overview](https://docs.byteplus.com/en/docs/DBW/billing-description?lang=en).

* Do not modify instance configurations while using the auto scaling function, as this may cause scaling operations to fail.

* Setting both CPU\-based auto scaling and scheduled scaling rules simultaneously is not supported. Only one of these rules can be selected. For details about scheduled scaling, refer to [Scheduled scaling management](https://docs.byteplus.com/en/docs/DBW/scheduled-scaling-management?lang=en).

## Advantages

* Ensures stable and sustainable business operations

   * Automatic scaling up: When business traffic surges (e.g., during large promotions, holidays, or unexpected events), this feature prevents performance bottlenecks, connection failures, or response delays due to insufficient resources.

   * Automatic scaling down: During low\-traffic periods, this feature prevents resource waste while ensuring stable service operation.

* Improve resource utilization efficiency and reduce costs

   * Traditional databases typically require resource provisioning based on peak demand, resulting in idle resources most of the time.

   * The auto scaling feature dynamically adjusts node specification resources based on actual workload, enabling a "pay\-as\-you\-go" model and significantly reducing operational costs.

* Simplify operation and maintenance management

   * Automatically adapt to workload fluctuations without manual intervention, reducing daily monitoring and manual parameter tuning for database administrators.

   * Avoid issues like delayed expansion or over\-provisioning caused by human judgment errors.

* Adapt to flexible business scenarios

For businesses with significant peak\-valley characteristics (e.g., live streaming, e\-commerce, online education), auto scaling quickly aligns with business rhythms.

## Enable auto scaling

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Configure AutoOps rules** \> **Node specification scaling**.

6. On the **Configure AutoOps rules** panel, configure the following parameters.

   |**Function** |**Parameter** |**Description** |
   |---|---|---|
   |**Automatic expansion** |**Automatic expansion** |Select **Enable auto scaling** to enable the automatic scaling up function. |
   ||**Scaling up type** |Currently, only **Node specification** can be selected and cannot be modified. |
   ||**Maximum CPU utilization** |* Maximum CPU utilization threshold: Set the CPU utilization threshold to trigger auto scaling as needed, in percentage (50%~90%).<br><br>* Instance specification threshold: Set the maximum scalable specification threshold for the instance. When the instance's maximum CPU utilization is greater than or equal to the set threshold, the instance will begin configuration changes. The instance specification threshold must be greater than the current instance specifications.<br><br><br>> **tip**<br><br><br>> For example, if you set the maximum CPU utilization threshold to **60%** and the instance specification threshold to **16 cores 128 GiB**, the instance will start scaling when the CPU utilization reaches or exceeds 60%, with a maximum upgrade to 16 cores 128 GiB.<br> |
   |**Automatic scaling down** |**Automatic scaling down** |Select **Enable automatic scaling** to enable the automatic scaling down function. |
   ||**Shrinking type** |Currently, only **Node specification** can be selected and cannot be modified. |
   ||**Maximum CPU utilization**<br><br> |* Maximum CPU utilization threshold: Set the CPU utilization threshold to trigger auto scaling as needed, in percentage (0%~30%).<br><br>* Instance specification threshold: Set the maximum specification threshold for automatic scaling down. The instance will start scaling when the maximum CPU utilization is less than or equal to the set threshold. The instance specification threshold must be less than the current instance specifications.<br><br><br>> **tip**<br><br><br>> For example, if you set the maximum CPU utilization threshold to **30%** and the instance specification threshold to **16 cores 128 GiB**, the instance will start scaling when the CPU utilization is less than or equal to 30%, with a minimum downgrade to 16 cores 128 GiB.<br> |

7. Set the **Duration**.

Select the duration from the drop\-down list, in minutes. Indicates that when the instance CPU utilization remains greater than or equal to/less than or equal to the set threshold for a period of time, instance scaling will be triggered.

8. Click **OK**.

   After enabling this feature, you cannot view the configuration content on the list page. You need to go to the configuration item to view details. The operation and maintenance event records will be displayed only after the trigger succeeds.

## View the triggered scaling up event

> **tip**

> You can view scaling up events within the last 30 days at most.

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, set the time range for the query events as needed. The target events to view include **Event ID**, **Event status**, **Trigger value**, **Trigger condition**, **Rule type**, **Before/After adjustment**, **Trigger time** and **Last update time**.

   > **tip**

   > Before/After triggering indicates the node specifications before and after automatic scaling up is triggered.

## Modify auto scaling rules

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Configure AutoOps rules** \> **Node specification scaling**.

6. On the **Configure AutoOps rules** panel, configure the following parameters.

   |**Function** |**Parameter** |**Description** |
   |---|---|---|
   |**Automatic expansion** |**Automatic expansion** |Select **Enable auto scaling** to enable the automatic scaling up function. |
   ||**Scaling up type** |Currently, only **Node specification** can be selected and cannot be modified. |
   ||**Maximum CPU utilization** |* Maximum CPU utilization threshold: Set the CPU utilization threshold to trigger auto scaling as needed, in percentage (50%~90%).<br><br>* Instance specification threshold: Set the maximum scalable specification threshold for the instance. When the instance's maximum CPU utilization is greater than or equal to the set threshold, the instance will begin configuration changes. The instance specification threshold must be greater than the current instance specifications.<br><br><br>> **tip**<br><br><br>> For example, if you set the maximum CPU utilization threshold to **60%** and the instance specification threshold to **16 cores 128 GiB**, the instance will start scaling when the CPU utilization reaches or exceeds 60%, with a maximum upgrade to 16 cores 128 GiB.<br> |
   |**Automatic scaling down** |**Automatic scaling down** |Select **Enable automatic scaling** to enable the automatic scaling down function. |
   ||**Shrinking type** |Currently, only **Node specification** can be selected and cannot be modified. |
   ||**Maximum CPU utilization**<br><br> |* Maximum CPU utilization threshold: Set the CPU utilization threshold to trigger auto scaling as needed, in percentage (0%~30%).<br><br>* Instance specification threshold: Set the maximum specification threshold for automatic scaling down. The instance will start scaling when the maximum CPU utilization is less than or equal to the set threshold. The instance specification threshold must be less than the current instance specifications.<br><br><br>> **tip**<br><br><br>> For example, if you set the maximum CPU utilization threshold to **30%** and the instance specification threshold to **16 cores 128 GiB**, the instance will start scaling when the CPU utilization is less than or equal to 30%, with a minimum downgrade to 16 cores 128 GiB.<br> |

7. Set the **Duration**.

Select the duration from the drop\-down list, in minutes. Indicates that when the instance CPU utilization remains greater than or equal to/less than or equal to the set threshold for a period of time, instance scaling will be triggered.

8. Click **OK**.

## Disable auto scaling rules

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Configure AutoOps rules** \> **Node specification scaling**.

6. On the **Configure AutoOps rules** panel, uncheck **Enable auto scaling** or **Enable automatic scaling**.

7. Click **OK**.

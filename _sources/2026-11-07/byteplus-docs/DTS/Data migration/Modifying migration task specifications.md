---
title: "Modifying migration task specifications"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/modifying_migration_task_specifications"
---

You can adjust the task link specification during the data migration process based on business data pressure. This topic explains how to change the link specifications of a migration task on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

A migration task has been created. For more information, refer to [Migration solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions).

<span id=".6LS555So6K-05piO"></span>
### Billing

After changing the link specifications of a migration task, BytePlus recalculates billing based on the new specifications. The current migration task supports only pay\-as\-you\-go billing. The new billing takes effect at the next full hour after modification. For more information, refer to [Configuration change and unsubscription](https://docs.byteplus.com/en/docs/DTS/modification_of_instance_specification_or_subscription_cancellation).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The link specification can only be changed when the migration progress enters the incremental migration phase. For methods of viewing migration progress, refer to [Viewing migration progress](https://docs.byteplus.com/en/docs/DTS/viewing_migration_progress).

* Before the specification change officially takes effect, the task can not be reconfigured again.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Data migration list** page, click **More operations** \> **Modify configuration** at the top right corner of the target task.

5. In the **Modify configuration** dialog box, set the **Link specifications**.

6. Click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details about each link specification, refer to <a href="https://docs.byteplus.com/en/docs/DTS/product_specifications">Product specifications</a>.   </div>

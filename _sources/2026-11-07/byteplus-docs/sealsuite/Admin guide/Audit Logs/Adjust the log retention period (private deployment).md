---
title: "Adjust the log retention period (private deployment)"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/privatized-version-log-audit-and-outgoing-configuration-guide"
---

For where to view each type of log, retention periods, and log forwarding support, see [View audit logs](https://docs.byteplus.com/en/docs/sealsuite/docs-zk9yxy9szc).

In private deployment scenarios, the Administrator can manually adjust log retention periods based on business requirements and the disk capacity of the underlying database.


1. Log in to the **O&M Platform**.

2. In the left navigation pane, choose **Business Configuration** \> **Data Storage and Concurrency**.

3. On the **Data Storage and Traffic Control Management** page, switch to the **Data Storage** tab.

4. Find the log name to adjust, and click **Modify Storage Duration** in the Actions column.

5. Adjust the storage duration of the target log based on the adjustable range for each log storage duration. After the storage duration expires, the system automatically clears the logs. They can no longer be searched or downloaded from the Admin Console. If you reduce the retention days and save the change, expired historical logs are physically deleted and cannot be restored. Confirm that you no longer need to retain them or that backups are complete.

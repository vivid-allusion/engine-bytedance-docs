---
title: "Manage write processors"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Manage_data_processors"
---

This document describes how to view write processor information, as well as how to enable, pause, edit, and delete write processors.

## Prerequisites

Write processors have been created. For details, see [Create a write processor](https://docs.byteplus.com/docs/tls/Create_a_data_processor).

## View data processor information

1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region where TLS is deployed.

3. In the left navigation bar, select **Data processing** \> **Data processors**.

4. In the write processor list, click the project name to expand the list of write processors in that project.

5. Click the write processor name to access the write processor configuration information.

   * View the enabled status of the write processor.

      You can view the enabled status of the write processor next to its name.

   * View write processor configuration information.

      In the write processor configuration information, you can view detailed configuration information for the write processor, as follows:

      |Parameters |Description |
      |---|---|
      |Name |The name of the write processor. |
      |ID |The ID of the write processor, which is automatically created by the system and cannot be modified. |
      |Description |Description of the write processor. |
      |Failure handling policy |The failure handling policy of the write processor. |
      |Update time |The update time of the write processor. |
      |Associated topic |The log topic associated with the write processor. |
      |Processing rules |The data processing rules of the write processor. |

## Manage write processor

1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region where TLS is deployed.

3. In the left navigation bar, select **Data processing** \> **Data processors**.

4. In the write processor list, click the project name to expand the list of write processors in that project.

5. Click the write processor name to access the write processor configuration information.

   |Actions |Description |
   |---|---|
   |Enable |Click **Start** in the upper right corner of the interface to start the write processor. |
   |Pause |Click **Pause** in the upper right corner of the interface to pause the write processor. |
   |Edit |Click **Edit** in the upper right corner of the interface to open the edit write processor page.<br><br><br>* You can modify parameters except for the **project**. For details, refer to [Create a write processor](https://docs.byteplus.com/docs/tls/Create_a_data_processor).<br><br>* Write processor names cannot be duplicated. |
   |Delete |Click **Delete** in the upper right corner of the interface to open the delete popup. After confirming the information of the resource to be deleted and its associated resources, check the acknowledgment statement and click **Delete write processor**.<br><br>> **Note**<br><br><br>> Deleting a write processor does not delete the corresponding log topic, but it will stop data processing. Proceed with caution.<br> |

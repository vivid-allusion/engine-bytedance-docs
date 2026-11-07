---
title: "Manage consumer processor"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Manage_consumer_processor"
---

This topic describes how to view consumer processor information, as well as how to enable, pause, edit, and delete consumer processors.

## Prerequisites

Consumer processors have been created. For details, see [Create consumer processor](https://docs.byteplus.com/docs/tls/Create_consumer_processor).

## View consumer processor information

1. Log in to [TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. In the left navigation bar, choose **Data processing** \> **Data processor**.

4. On the **Consumer processors** tab, click the project name to expand the list of consumer processors in that project.

5. Click the consumer processor name to access its configuration page.

   * View the enabled status of the consumer processor.

      You can view the running status of the data processor next to its name.

   * View consumer processor configuration information.

      On the consumer processor configuration information page, you can review detailed settings for that processor as follows:

      |Parameters |Description |
      |---|---|
      |Name |Name of the data processor. |
      |ID |ID of the data processor. Created automatically by the system and can not be modified. |
      |Description |Description of the data processor. |
      |Failure handling policy |Failure handling policy for the data processor. |
      |Update time |Data processor update time. |
      |Processing rules |Data processing rules of the data processor. |

## Manage consumer processors

1. Log in to [TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. In the left navigation bar, choose **Data processing** \> **Data processor**.

4. On the **Consumer processors** tab, click the project name to expand the list of consumer processors in that project.

5. Click the consumer processor name to access its configuration page.

   |Actions |Notice |
   |---|---|
   |Start |Click **Start** in the upper right corner of the interface to launch the consumer processor. |
   |Pause |Click **Pause** in the upper right corner of the interface to pause the consumer processor. |
   |Edit |Click **Edit** in the upper right corner of the interface to access the **Edit consumer processor** page.<br><br><br>* You can modify all parameters except for the associated **project**. For details, see [Create consumer processor](https://docs.byteplus.com/docs/tls/Create_consumer_processor).<br><br>* Consumer processor names must be unique. |
   |Delete |Click **Delete** in the upper right corner of the interface to open the deletion dialog. Confirm the information of the resource to be deleted and the associated resources, check the acknowledgment message, and then click **Delete consumer processor**.<br><br>> **Notice**<br><br><br>> Deleting a consumer processor does not delete the corresponding log topic, but it will stop data processing. Proceed with caution.<br> |

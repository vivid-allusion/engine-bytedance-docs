---
title: "Delete instance"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Delete_instance"
---

For business needs, if certain instances are no longer required, you can delete them promptly to save resources and costs. This section explains the steps to delete an instance in the Message Queue for RabbitMQ console.

<span id="前提条件"></span>
## Prerequisites


* The billing method of the RabbitMQ instance is **Pay\-as\-you\-go**. 

* The RabbitMQ instance is in **Running** or **Fault** status.

* The related Queue, Exchange, and Vhost of the RabbitMQ instance have been deleted.


<span id="注意事项"></span>
## Notes


* After deleting an instance, all original data in the instance will be erased and cannot be recovered. Proceed with caution.

* Deleting the instance will also automatically unbind its elastic public network EIP. The EIP will remain reserved and incur charges. Please release the related resources if no longer needed.


<span id="操作步骤"></span>
## Operation Steps


1. Log in to [Message Queue RabbitMQ Console](https://console.byteplus.com/rabbitmq/).

2. Delete the instance.

   Message Queue for RabbitMQ supports both standard and forced deletion. When your instance fails to meet the deletion criteria but still requires deletion, you can opt for forced deletion, ensuring a more effective process.

   * Standard deletion (instance has no resources)

      1. On the **Instances** page, first select the target instance. Then click **Actions** column and select ··· \> **Delete**.

      2. In the dialog, check the instance information to be deleted and click **Delete**.

   * Force delete (instance with no queue, has other resources)

      1. On the **Instances** page, first select the target instance. Then click **Actions** column and select ··· \> **Delete**.

      2. In the confirmation dialog, check the instance information to be deleted and click **Delete**.

   * Force delete (instance with queue)

      1. On the **Instances** page, first select the target instance. Then click **Actions** column and select ··· \> **Delete**.

      2. In the **Cannot delete instance now** dialog, click **Force Release**.

      3. In the confirmation dialog, check the instance information to be deleted and click **Force Delete**.

---
title: "Resetting a SASL user password"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/resetting-SASLuser-password"
---

After creating a Simple Authentication and Security Layer (SASL) user, ensure to securely store the username and password. If you forget the password, set a new SASL username and password by resetting the password.

<span id="注意事项"></span>
## Precautions

After resetting the password, producer and consumer instances using this SASL user for authentication must update the username and password details in their respective codes to prevent connection issues due to authentication failures.

<span id="操作步骤"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. On the **Instances** page, click the name of the instance.

4. On the **User Management** tab, locate the SASL user you want to delete and click **Reset password** in the **Actions** column.

5. On the **Reset password** page, enter a new password and click **OK**.

   Make sure to securely store the new username and password after resetting the password.

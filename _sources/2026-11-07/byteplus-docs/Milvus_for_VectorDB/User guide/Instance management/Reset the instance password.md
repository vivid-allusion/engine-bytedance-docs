---
title: "Reset the instance password"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Reset_the_instance_password"
---

After creating a Milvus for VectorDB instance, you can reset the instance password as needed. This topic describes how to reset the instance password.

## Prerequisites

An instance is created. For more information about how to create an instance, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

## Precautions

Resetting the instance password will cause existing service connections to fail; proceed with caution.

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. in the top menu bar, select the project and region for the instance.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instance list** in the left navigation pane.

4. In the **Instances** tab, select the **Dedicated**, **Serverless**, or **On\-Demand** tab as needed, then click the target instance's instance name.

5. On the **Instance details** page, click **Reset** to the right of **Password**.

6. In the pop\-up dialog, set and confirm the new password, then click **OK**. The password rules are as follows:

   * Contain only uppercase letters, lowercase letters, digits, and the following special characters `_#!@$%^&*()+=-`.

   * Must include at least three types from uppercase letters, lowercase letters, digits, and special characters.

   * Length must be between 8 and 32 characters.

   * Weak passwords are not allowed. For details, see the [Weak password dictionary](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Weak_password_dictionary).

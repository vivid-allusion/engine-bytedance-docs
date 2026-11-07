---
title: "Configure instance public network access"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Configure_instance_public_network_access"
---

Milvus for VectorDB instances support enabling public network access to allow devices outside the VPC to access the instance When devices outside the VPC no longer need to access the Milvus for VectorDB instance, disable public network access promptly This topic describes how to configure instance public network access.

## Precautions

* To enable public network access for the instance, you need to associate an existing Elastic IP (EIP). Charges are billed by EIP. For more information, see [Billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview).

* Monitor the expiration time of the EIP. If it expires without renewal, the public domain name will become unavailable.

## Enable public network access

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. in the top menu bar, select the project and region for the instance.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. In the **Instances** list, select the **Dedicated**, **Serverless**, or **On\-Demand** tab as needed, then click the instance name of the target instance.

4. On the **Instance details** tab, turn on the **Public network access** switch in the **Instance Access Information** section.

5. In the **Reminder** panel, configure the following parameters, then click **OK**.

   |Parameter |Description |
   |---|---|
   |EIP |Click the dropdown list, select the EIP to use on the **Enable public network access** panel, then click **OK**. If no EIP is available, click **Apply for EIP**. |
   |IP allowlist |To ensure your access security, when enabling public network access, the IP allowlist automatically adds `127.0.0.1`, blocking all public IP addresses from access. If you need normal use, modify the IP allowlist by entering the allowlist group name and adding IP addresses. You can also click **Add IP allowlist group** to add multiple groups.<br><br><br>* All groups can upload up to 300 IP addresses or IP subnets in total.<br><br>* `0.0.0.0/0` means allowing access from all IPv4 addresses, which is not recommended for security reasons. |

6. Check the progress of enabling public network access for the instance.

   Return to the Instances page, where the instance status shows as **Updating**. When the status shows **Running**, it indicates that the association and public network access activation succeeded.

## Disable public network access

After disabling public network access for the instance, the client cannot access the Milvus for VectorDB instance through the original public access address. Confirm your services are not using the public address to avoid unnecessary losses.

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. in the top menu bar, select the project and region for the instance.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. In the **Instances** list, choose the **Dedicated**, **Serverless**, or **On\-Demand edition** tab as needed, then click the instance name of the target instance.

4. In the **Instance details** tab, under **Instance Access Information**, turn off the **Public network access** switch.

5. In the pop\-up dialog box, review the precautions for disabling public network access, then click **OK**.

   > **warning**

   > After disabling public network access, the disassociated EIP will remain and incur charges. Release the EIP resource on your own.

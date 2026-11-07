---
title: "Create integration"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_integration"
---

The integration center manages external storage connection configurations used by On\-Demand instance External Collections in a unified way. By creating integrations, you can save the connection information of external storage. When creating an External Collection, you can directly reference the configured integration, simplifying the external storage setup process. This topic describes how to create an integration.

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the region where you want to create the integration.

3. In the left navigation bar, select **Integration center**, then click **Create integration**.

4. In the Create Integration dialog box, configure the following parameters, then click **OK**.

   |**Parameter** |**Description** |
   |---|---|
   |Configuration name |Enter the name of the integration. Naming rules are as follows:<br><br><br>* Only uppercase and lowercase letters, numbers, and separators (\-) are allowed.<br><br>* Must start with a letter.<br><br>* Length must be between 2 and 64 characters. |
   |Integration type |Select the data source used for integration. Currently only **TOS** is supported. |
   |Region |Defaults to the region of the current instance and cannot be changed. |
   |Bucket |Select the TOS Bucket used for integration. |
   |Authorize to use an instance |Authorize the selected Bucket.<br><br><br>* Authentication method: select an authentication method from the drop\-down list. Currently, only **Bucket Policy** is supported.<br><br>* Bucket permissions: select Bucket permissions from the dropdown list.<br><br>   * Read\-only: allows only reading Bucket data (data import).<br><br>   * Read and write: allows reading and writing Bucket data (Backup/Data export).<br><br><br>Click **Verify integration**. |

## Subsequent operations

### Delete integration

You can delete a Query cluster when it is no longer needed.

> **warning**

> This model cannot be recovered after deletion. Please proceed with caution.

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select the region where you want to create the integration from the top navigation bar.

3. In the left navigation bar, select **Integration center**. Click **delete** to the right of the target integration, then click **delete** in the pop\-up dialog.

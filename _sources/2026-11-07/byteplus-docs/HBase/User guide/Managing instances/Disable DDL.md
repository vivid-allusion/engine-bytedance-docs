---
title: "Disable DDL"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Disable_DDL"
---

HBase provides the Disable DDL feature to ensure the stability of an instance's table structure and prevent accidental or unauthorized DDL operations on tables. When this feature is enabled, you cannot perform DDL operations on the instance's tables. This prevents unintended modifications and reduces the risk of structural changes from incorrect operations.

<span id="R54gbr0f"></span>
## Precautions

After you enable the Disable DDL feature, you cannot perform DDL operations on the instance's tables. The following APIs will be disabled:


|**Type** |**API** |
|---|---|
|Table DDL<br><br> |* CreateTable<br><br>* DeleteTable<br><br>* TruncateTable<br><br>* EnableTable<br><br>* DisableTable<br><br>* ModifyTable |
|ColumnFamily DDL |* AddColumn<br><br>* DeleteColumn<br><br>* ModifyColumn |
|Namespace DDL |* CreateNamespace<br><br>* DeleteNamespace<br><br>* ModifyNamespace |


<span id="AoWXWAnE"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the instance name of the target instance to enter the **Summary** page.

4. Enable or disable the Disable DDL feature in the **Disable DDL** setting under the **Configuration** section.

   * **Enable Disable DDL**: Click **Enable Disable DDL**. In the pop\-up dialog, confirm the operational impact and click **OK**.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">After the Disable DDL feature is enabled, you cannot perform DDL operations on the tables of this instance. Attempting a DDL operation will trigger an error with the message: <code>DDL operations have been disabled.</code>      </div>
      

   * **Disable Disable DDL:**  Click **Disable Disable DDL**. In the pop\-up dialog, confirm the operational impact and click **OK**.

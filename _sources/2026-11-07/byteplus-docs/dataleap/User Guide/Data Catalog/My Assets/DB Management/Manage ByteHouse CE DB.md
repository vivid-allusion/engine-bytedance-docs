---
title: "Manage ByteHouse CE DB"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Manage_ByteHouse_CE_Database"
---

Database management provides unified creation, editing, and authorized ownership of metadata. This article introduces how to manage ByteHouse CE databases.

<span id="_1-约束限制"></span>
## Constraints


* Only the main account or sub\-accounts with **ByteHouseCEStandardAccess** permission can create and edit databases correctly. To activate sub\-account authorization, carry out the following steps. See [Bytehouse Enterprise Documentation](https://docs.byteplus.com/en/docs/bytehouse/getting-started#_3-import-users) for details.

   1. The main account grants the **ByteHouseCEStandardAccess** permission to the sub\-account in the console.

   2. The sub\-account logs in once to the [ByteHouse CE Console](https://console.byteplus.com/bytehouse-ce/region:bytehouse-ce+ap-southeast-1/home/overview).

* Users can only manage databases they are responsible for.


<span id="_2-前提条件"></span>
## Prerequisites

Collector created, and ByteHouse CE metadata ingested into Data Catalog. Related operating instructions can be found in [Metadata Ingestion](https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion).

<span id="_3-操作步骤"></span>
## Operation Steps


1. Log in to DataLeap console.

2. Select **Overview \> Catalog \> My Assets \> DB Management** to enter the DB Management page.

3. Click the **ByteHouse CE** tab to enter the ByteHouse CE page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67e2f8e5b1234041a199a8d149708322~tplv-goo7wpa0wc-image.image) </span>

4. The following actions can be executed:

   * Click the **Create ByteHouse CE DB** button. In the popup database creation window, fill in the information and click the **OK** button to create a new ByteHouse CE DB.

      The related parameters for creating a ByteHouse CE DB are described in the following table.

      
      |Parameter |Description |
      |---|---|
      |\*Cluster |ByteHouse CE cluster name. Select from the dropdown of created clusters. |
      |\*Database name |The name of the created database, which cannot be changed once set.<br><br>Supports only lowercase English letters, numbers, and underscores, starting with a lowercase letter, up to 50 characters. |
      |\*Database owner |The database administrator, typically a developer role responsible for daily operation.<br><br><br>* Automatically filled with the current user when creating a database; supports setting multiple owners and selecting from created tenant accounts via dropdown. The owner can be changed, but you cannot remove yourself.<br><br>* Optionally synchronize to the database authority owner. |
      |\*Database authority owner |A security management role that manages all resources under the database (authorization revoke, classification settings, approval flow configuration, etc.), decides whether data can be publicly used, and directly participates in the approval of the entire database’s permissions.<br><br>When the **DB owners** uncheck **synchronization to the database authority owner**, this option becomes editable and supports selecting multiple choices. |
      |Description |Information explaining the database's range, usage, etc., to facilitate future management. |
      |\*DB usage |There are two options: production environment and test environment. |
      |\*Confidentiality Level |The database security level ranges from low to high as L1, L2, L3, and L4, selectable from a dropdown. |
      

   * Enter a name or description keyword to search the list of databases that match the criteria.

   * Click the **Edit** button in the **Action** column of a database entry in the list. In the pop\-up edit window, you can modify the database's basic info and click the **go to settings** button on the row of the parameter **permission settings** to access the permission management module to set database permissions and approval processes.

      Please refer to [Set Application Permissions](https://docs.byteplus.com/docs/dataleap/Set_Application_Permissions) for related instructions on permission management operations.

   * Click the **Delete** button in the **Action** column of a database entry. In the pop\-up confirmation dialog, click **Confirm** to delete the database.


<span id="f1053979"></span>
## Subsequent Operations

After creating the database, go to the **Table management** page to create the required tables under the database. See [Manage ByteHouse CE Tables](https://docs.byteplus.com/docs/dataleap/Manage_ByteHouse_CE_Tables) for related operation instructions of table management.

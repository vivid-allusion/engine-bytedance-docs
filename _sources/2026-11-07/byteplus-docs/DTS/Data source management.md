---
title: "Data source management"
product: "Database Transmission Service"
product_code: "DTS"
section: "Document"
source: "https://docs.byteplus.com/en/docs/DTS/Data_source"
---

Database Transmission Service (DTS) supports pre\-entry of database instance information. When creating a data transmission task, you can directly select a pre\-registered database instance, avoiding the repetitive steps of re\-entering database information and saving time. This topic describes how to enter, edit, and delete data source instances in the DTS console, using MySQL as an example.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* If you need to register a database of public and express networks, you must first add the CIDR block of the DTS server to the allowlist or security group. For more information, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* If you need to implement cross\-account data transmission, you need to grant cross\-account permissions to the relevant accounts. For detailed steps, refer to [How to authorize users for cross-account data transmission](https://docs.byteplus.com/en/docs/DTS/How_to_authorize_users_for_cross-account_data_transmission).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The database instances registered in your data sources are only available for use when creating data transmission tasks.

* The instance region can not be modified when you edit a data source.

* When creating a data source, you can choose to either validate the correctness of the database account and password or skip this verification.

* The data source does not support the sub\-account project permission management. To use it, you need to grant the global permissions of DTS. For details, refer to [IAM user permission management](https://docs.byteplus.com/en/docs/DTS/iam_user_permission_management).

* When you select a data source with the access method set to Redis connected over express network and the architecture type as cluster edition, this data source can only be used as the destination for migration tasks. To use it as the source end of a migration task, you need to select the standalone edition for the architecture type.


<span id=".5Yib5bu65pWw5o2u5rqQ"></span>
## Create data source


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data source**.

4. On the **List of data sources** page, click **Create data source**.

5. On the **Create data source** panel, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Data source name** |Custom data source name. Naming rules are as follows: <br><br><br>* Must start with a Chinese character or letter.<br><br>* Must be 64 characters or less.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is recommended to set a data source name related to the business to improve operational efficiency.</div><br> |
   |**Database type** |Select database type as needed. This topic uses **MySQL** as an example. |
   |**Access method** |Select an access method for the database instance as needed. This topic uses **Volcegine MySQL** as an example. |
   |**Region** |Select the region to which the instance belongs. |
   |**Cross\-BytePlus account?**  |Select whether to transmit data cross\-account as needed, with the following options:<br><br><br>* **This account**: Selecting this means data transmission occurs only within this account.<br><br>* **Cross\-account**: Selecting this means data transmission occurs between two accounts.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When transmitting data across accounts, log on to the Database Transmission Service (DTS) console through the account of the destination.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Before cross\-account data transmission, create and authorize an IAM role in the source root user. For detailed steps, refer to <a href="https://docs.byteplus.com/en/docs/DTS/How_to_authorize_users_for_cross-account_data_transmission">How to authorize users for cross\-account data transmission</a>.</div><br> |
   |**Cross\-accountID** |Enter the BytePlus account ID to which the source database belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Configure this parameter when selecting cross\-volcan engine accounts for data transmission.</div><br> |
   |**Cross\-account roles** |Enter the IAM role authorized for DTS to access cross\-account resources.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Configure this parameter when selecting cross\-BytePlus accounts for data transmission.</div><br> |
   |**MySQL instance** |Select the target instance of RDS for MySQL from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can also search for the target instance by instance ID or name.</div><br> |
   |**Node type** |Select node types as needed, currently supporting **Primary node** and **Read\-only node**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Select read\-only nodes when read\-only nodes are created within the instance. For specific steps on creating a read\-only node, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/overview_of_read-only_nodes">Read\-only node overview</a>.</div><br> |
   |**MySQL read\-only node** |Select the target read\-only node from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When a read\-only node is created in the instance and <strong>Node type</strong> selects <strong>Read\-only node</strong>, this parameter can be configured.</div><br> |
   |**Database account** |Enter the database account of the source instance. |
   |**Database password** |Enter the password corresponding to the database account of the source instance. |
   |**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can choose to either validate the correctness of the database account and password or skip this verification.</div><br> |
   

6. Click **OK**.


<span id=".57yW6L6R5pWw5o2u5rqQ"></span>
## Edit data source


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data source**.

4. On the **List of data sources** page, click **Edit** in the **Actions** column of the target data source.

5. On the **Edit data source** panel, configure the relevant parameters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The modification of the region is not supported when editing a data source.   </div>
   

6. Click **OK**.


<span id=".5p-l55yL5pWw5o2u5rqQ"></span>
## View data source


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data source**.

4. On the **List of data sources** page, you can view the following data source information:

   * Basic information about the data source includes ** Data source name/ID**, **Access method**, **Database type**, **Instance ID/link address**, **Creation time**, and **Update time**.

   * Data source details: Click the name of the target data source. In the **Data source details** dialog box, view the **Data source name**, **Database type**, **Access method**, **Region**, **Architecture**, **Incremental data acquisition method**, **Whether to cross Volcegine accounts**, **Instance**, **Node type**, **Database account**, and other information (refer to the DTS console).


<span id=".5Yig6Zmk5pWw5o2u5rqQ"></span>
## Delete data source


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data source**.

4. On the **List of data sources** page, click **Delete** in the **Actions** column of the target data source.

5. In the **Confirm** dialog box, click **OK**.

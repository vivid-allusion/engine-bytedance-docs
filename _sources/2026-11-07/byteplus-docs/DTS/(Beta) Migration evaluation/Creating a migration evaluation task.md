---
title: "Creating a migration evaluation task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Creating_a_migration_evaluation_task"
---

This topic describes how to create a data migration evaluation task on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* When the access method of the database instance is self\-managed over the Internet and access restrictions are enabled, add the DTS server IP addresses to the allowlist or security group of the database instance before creating the database transmission task. DTS server IP addresses vary by region, as detailed below:

   * DTS server IP addresses in China (Guangzhou), China (Shanghai), and China (Beijing) are `221.194.189.0/27,157.148.90.32/27,180.184.132.64/27,61.129.54.64/27,220.196.172.32/27,117.135.143.32/27,220.196.168.32/27,116.132.250.32/27,111.45.13.32/27,125.88.248.32/27,180.153.35.32/27,220.181.65.32/27,220.181.65.64/27`.

   * DTS server IP addresses in Asia Pacific (Johor) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.

   * DTS server IP addresses in Asia Pacific (Jakarta) are `221.194.189.0/27,157.148.90.32/27`.

   * DTS server IP addresses in China (Hong Kong) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.

      For more information on the CIDR block of DTS servers, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* When your instance connects via the VPC, the subnet of the VPC must communicate with the source or target database. To allow DTS to access instances in the VPC normally, add the subnet CIDR block to the source or target database allowlist or security group rules. For more information, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* When the source database instance is MySQL connected over express network:

   * When using VPN to perform data migration, the local network where the self\-managed database is located has been connected to BytePlus via VPN gateway. For detailed steps, refer to [Building a cloud VPC and on-premises multi-data-center network interconnection](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-multiple-data-centers).

   * If data migration requires a dedicated line connection, you need to establish a dedicated line connection between a single cloud VPC and a single on\-premises data center network. For more information, refer to [Configuring direct connections](https://docs.byteplus.com/en/docs/directconnect/Quick-start#.6YWN572u5LiT57q_6L-e5o6l).

   * When the database instance’s access method is VPC and access restrictions are enabled, add the subnet segment of the VPC connected by the dedicated line to the database instance’s allowlist or security group before creating the database transmission task. For more information, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* An instance and database for RDS for MySQL have been created. For details, refer to [Creating an instance (RDS for MySQL)](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating a database](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_database).

* An instance and database for NDB for MySQL have been created. For more information, refer to [creating an NDB for MySQL instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance?lang=zh), and [creating a database](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_database_and_account?lang=zh).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. Select a method to enter migration evaluation:

   * Method 1: In the left navigation bar, click **Migration evaluation**.

   * Method 2:

      1. In the left navigation bar, click **Data migration**.

      2. On the **Data migration list** page, click **Migration evaluation**.

4. On the **Create migration evaluation task** page, locate the **Configure source and target database** wizard, and configure the following parameters.

   * Create a data migration evaluation task with the source as MySQL connected over public network

      
      <Tabs>
      <Tab zoneid="Fdgp61jTtm" title="To RDS for MySQL">
      <TabTitle>To RDS for MySQL</TabTitle>
      
      
      |**Type** |**Parameter** |**Description** |
      |---|---|---|
      |**Basic information** |**Task name** |(Optional) Customize the migration evaluation task name. The naming rules are as follows:<br><br><br>* Must start with a Chinese character or letter.<br><br>* Must be 64 characters or less.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not customize the task name, the system will automatically generate a task name starting with <code>dts-</code>.</div><br> |
      |**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
      ||**Instance type** |Only **MySQL ** can be selected. |
      ||**Access method** |Select **MySQL connected over public network**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When migrating a MySQL connected over public network instance, you need to add DTS IP segment access permissions in the allowlist or security group policies of the source end in advance. Click <strong>View DTS CIDR blocks</strong> to view and copy the CIDR block.</div><br> |
      ||**Region** |Select the region where the target instance is located. |
      ||**Host address** |Enter the host address of the target database's self\-managed instance. |
      ||**Port** |Enter the port number of the target self\-managed instance. |
      ||**Database account** |Enter the database account of the target instance. |
      ||**Database password** |Enter the password corresponding to the database account of the target instance. |
      ||**Connection method** |Select an **Unencrypted** or **SSL\-secured connection** as needed to establish a more secure and reliable migration link.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When you select an <strong>SSL\-secured connection</strong>, you must first enable the SSL encryption feature for <strong>MySQL connected over public network</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When a migration task selects an <strong>Unencrypted connection</strong> and runs normally, enabling the SSL encryption feature for <strong>MySQL connected over public network</strong> may cause the unencrypted task to fail.</div><br> |
      ||**SSL encryption certificate** |Click **Upload SSL encryption certificate** to upload the CA certificate. When the **Connection method** is set to **SSL\-secured connection**, this configuration is supported. |
      ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address. |
      |**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
      ||**Instance type** |Only **MySQL ** can be selected. |
      ||**Access method** |Only **BytePlus MySQL** can be selected. |
      ||**Region** |Select the region where the target instance is located. |
      ||**MySQL instance source** |Supports the following methods: **Select an existing instance** and **Select instance configuration**. |
      ||When **MySQL instance source** selects **Select an existing instance**, you need to configure information such as **MySQL instance**, **Database account**, and **Database password**. ||
      ||**MySQL instance** |Select the target instance of RDS for MySQL from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The drop\-down list only shows the first 10 instances. You can also search for the target instance by instance ID or name.</div><br> |
      ||**Database account** |Enter the database account of the target instance. |
      ||**Database password** |Enter the password corresponding to the database account of the target instance. |
      ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
      ||When **Select instance configuration ** is selected for **MySQL instance** type, you need to configure **Compatible version**, **Specification type**, **Instance specification** and other information. ||
      ||**Compatible version** |Select the compatible version of the instance as needed. **MySQL 5.7** and **MySQL 8.0** are supported. |
      ||**Specification type** |Support two specification types: **General type** (formerly "shared type") and **Dedicated type** (formerly "general type").<br><br><br>* **General type**: Exclusive use of allocated memory and storage resources, shares CPU resources with other shared instances in the same physical machine.CPU utilization is maximized through resource reuse, with high cost performance. CPU utilization is maximized through resource reuse, with high cost performance.<br><br>* **Dedicated type**: Fully exclusive use of allocated CPU, memory, and storage resources, with stable performance, not affected by other instances in the physical machine. |
      ||**Instance specification** |Select the instance specification configuration from the drop\-down list. |
      
      
      
      
      
      </Tab>
      <Tab zoneid="cJZvi0XRCP" title="To veDB for MySQL">
      <TabTitle>To veDB for MySQL</TabTitle>
      
      
      |**Type** |**Parameter** |**Description** |
      |---|---|---|
      |**Basic information** |**Task name** |(Optional) Customize the migration evaluation task name. The naming rules are as follows:<br><br><br>* Must start with a Chinese character or letter.<br><br>* Must be 64 characters or less.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you do not customize the task name, the system will automatically generate a task name starting with <code>dts-</code>.</div><br> |
      |**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to Data source management.<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
      ||**Instance type** |Only **MySQL ** can be selected. |
      ||**Access method** |Select **MySQL connected over public network**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When migrating a MySQL connected over public network instance, you need to add DTS IP segment access permissions in the allowlist or security group policies of the source end in advance. Click <strong>View DTS CIDR blocks</strong> to view and copy the CIDR block.</div><br> |
      ||**Region** |Select the region where the target instance is located. |
      ||**Host address** |Enter the host address of the target database's self\-managed instance. |
      ||**Port** |Enter the port number of the target self\-managed instance. |
      ||**Database account** |Enter the database account of the target instance. |
      ||**Database password** |Enter the password corresponding to the database account of the target instance. |
      ||**Connection method** |Select an **Unencrypted** or **SSL\-secured connection** as needed to establish a more secure and reliable migration link.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When you select an <strong>SSL\-secured connection</strong>, you must first enable the SSL encryption feature for <strong>MySQL connected over public network</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When a migration task selects an <strong>Unencrypted connection</strong> and runs normally, enabling the SSL encryption feature for <strong>MySQL connected over public network</strong> may cause the unencrypted task to fail.</div><br> |
      ||**SSL encryption certificate** |Click **Upload SSL encryption certificate** to upload the CA certificate. When the **Connection method** is set to **SSL\-secured connection**, this configuration is supported. |
      ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address. |
      |**Target database configuration**<br><br> |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to Data source management.<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
      ||**Instance type** |Only **MySQL ** can be selected. |
      ||**Access method** |Select  or **MySQL connected over express network** as needed. |
      ||**Region** |Select the region where the target instance is located. |
      ||**MySQL instance source** |Supports the following methods: **Select an existing instance** and **Select instance configuration**. |
      ||Configure parameters such as MySQL instance, Database account, and Database password when selecting Select an existing instance under MySQL instance sourceSelect an existing instance**MySQL instance**, **Database account**, and **Database password** when selecting Select an existing instance under MySQL instance source. ||
      ||**MySQL instance** |Select the target instance of NDB for MySQL from the drop\-down list.<br><br>The drop\-down list only shows the first 10 instances. You can also search for the target instance by instance ID or name. |
      ||**Database account** |Enter the database account of the target instance. |
      ||**Database password** |Enter the password corresponding to the database account of the target instance. |
      ||**Test connection**<br><br> |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
      ||When **Select instance configuration ** is selected for **MySQL instance** type, you need to configure **Compatible version**, **Specification type**, **Instance specification** and other information. ||
      ||**Compatible version** |Select the compatible version of the instance as needed. **MySQL 5.7** and **MySQL 8.0** are supported. |
      ||**Specification type** |Supports two specification types: **General type** and **Dedicated type**.<br><br><br>* **General type**: Exclusive use of allocated memory and storage resources, shares CPU resources with other shared instances in the same physical machine.CPU utilization is maximized through resource reuse, with high cost performance. CPU utilization is maximized through resource reuse, with high cost performance.<br><br>* **Dedicated type**: Fully exclusive use of allocated CPU, memory, and storage resources, with stable performance, not affected by other instances in the physical machine. |
      ||**Instance specification** |Select the instance specification configuration from the drop\-down list. |
      
      
      
      
      
      </Tab>
      </Tabs>
      

   * Create a data migration from MySQL connected over express network to BytePlus edition MySQL

      
      <Tabs>
      <Tab zoneid="ctaCZDsfG6" title="To RDS for MySQL">
      <TabTitle>To RDS for MySQL</TabTitle>
      
      
      |**Type** |**Parameter** |**Description** |
      |---|---|---|
      |**Basic information** |**Task name** |(Optional) Customize the migration evaluation task name. The naming rules are as follows:<br><br><br>* Must start with a Chinese character or letter.<br><br>* Must be 64 characters or less.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not customize the task name, the system will automatically generate a task name starting with <code>dts-</code>.</div><br> |
      |**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
      ||**Instance type** |Select **MySQL**. |
      ||**Access method** |Select **MySQL connected over express network**. |
      ||**Region** |Select the region of the virtual private cloud. |
      ||**Host address** |Enter the host address of the MySQL instance connected over express network.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, only IPv4 addresses are supported for access. IPv6 addresses are not yet supported.</div><br> |
      ||**Port** |Enter the port of the MySQL instance connected over express network. |
      ||**Virtual private cloud** |Select the target VPC from the drop\-down list as follows:<br><br><br>* Direct connect: Select any VPC under the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Select the VPC bound to the VPN gateway when achieving data connectivity through VPN. |
      ||**Subnet** |Select a subnet within the VPC from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When migrating a MySQL instance connected over express network, you need to add subnet CIDR block access permissions to the allowlist or security group policy on the source end in advance. Click <strong>View subnet CIDR blocks</strong> to view and copy CIDR blocks.</div><br> |
      ||**Database account** |Enter the database account of the target instance. |
      ||**Database password** |Enter the password corresponding to the database account of the target instance. |
      ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address.<br><br>* **The Express network requires the subnet to have \* available IPs. The current number of available IPs in the subnet is insufficient, and the task can not be created. Check the subnet resources in the VPC**: When this error prompt appears, adjust the number of available IPs in the VPC subnet to ensure enough IPs in the target VPC subnet. |
      |**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
      ||**Instance type** |Only **MySQL ** can be selected. |
      ||**Access method** |Only **BytePlus MySQL** can be selected. |
      ||**Region** |Select the region where the target instance is located. |
      ||**MySQL instance source** |Supports the following methods: **Select an existing instance** and **Select instance configuration**. |
      ||When **MySQL instance source** selects **Select an existing instance**, you need to configure information such as **MySQL instance**, **Database account**, and **Database password**. ||
      ||**MySQL instance** |Select the target instance of RDS for MySQL from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The drop\-down list only shows the first 10 instances. You can also search for the target instance by instance ID or name.</div><br> |
      ||**Database account** |Enter the database account of the target instance. |
      ||**Database password** |Enter the password corresponding to the database account of the target instance. |
      ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
      ||When **Select instance configuration ** is selected for **MySQL instance** type, you need to configure **Compatible version**, **Specification type**, **Instance specification** and other information. ||
      ||**Compatible version** |Select the compatible version of the instance as needed. **MySQL 5.7** and **MySQL 8.0** are supported. |
      ||**Specification type** |Support two specification types: **General type** (formerly "shared type") and **Dedicated type** (formerly "general type").<br><br><br>* **General type**: Exclusive use of allocated memory and storage resources, shares CPU resources with other shared instances in the same physical machine.CPU utilization is maximized through resource reuse, with high cost performance. CPU utilization is maximized through resource reuse, with high cost performance.<br><br>* **Dedicated type**: Fully exclusive use of allocated CPU, memory, and storage resources, with stable performance, not affected by other instances in the physical machine. |
      ||**Instance specification** |Select the instance specification configuration from the drop\-down list. |
      
      
      
      
      
      </Tab>
      <Tab zoneid="TnNF73y4Zs" title="To veDB for MySQL">
      <TabTitle>To veDB for MySQL</TabTitle>
      
      
      |**Type** |**Parameter** |**Description** |
      |---|---|---|
      |**Basic information** |**Task name** |(Optional) Customize the migration evaluation task name. The naming rules are as follows:<br><br><br>* Must start with a Chinese character or letter.<br><br>* Must be 64 characters or less.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you do not customize the task name, the system will automatically generate a task name starting with <code>dts-</code>.</div><br> |
      |**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to Data source management.<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
      ||**Instance type** |Select **MySQL**. |
      ||**Access method** |Select **MySQL connected over express network**. |
      ||**Region** |Select the region of the virtual private cloud. |
      ||**Host address** |Enter the host address of the MySQL instance connected over express network.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Currently, only IPv4 addresses are supported for access. IPv6 addresses are not yet supported.</div><br> |
      ||**Port** |Enter the port of the MySQL instance connected over express network. |
      ||**Virtual private cloud** |Select the target VPC from the drop\-down list as follows:<br><br><br>* Direct connect: Select any VPC under the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Select the VPC bound to the VPN gateway when achieving data connectivity through VPN. |
      ||**Subnet** |Select a subnet within the VPC from the drop\-down list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When migrating a MySQL instance connected over express network, you need to add subnet CIDR block access permissions to the allowlist or security group policy on the source end in advance. Click <strong>View subnet CIDR blocks</strong> to view and copy CIDR blocks.</div><br> |
      ||**Database account** |Enter the database account of the target instance. |
      ||**Database password** |Enter the password corresponding to the database account of the target instance. |
      ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address.<br><br>* **The Express network requires the subnet to have \* available IPs. The current number of available IPs in the subnet is insufficient, and the task can not be created. Check the subnet resources in the VPC**: When this error prompt appears, adjust the number of available IPs in the VPC subnet to ensure enough IPs in the target VPC subnet. |
      |**Target database configuration**<br><br> |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to Data source management.<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
      ||**Instance type** |Only **MySQL ** can be selected. |
      ||**Access method** |Select **NDB for MySQL** as needed. |
      ||**Region** |Select the region where the target instance is located. |
      ||**MySQL instance source** |Supports the following methods: **Select an existing instance** and **Select instance configuration**. |
      ||Configure parameters such as **MySQL instance**, **Database account**, and **Database password** when selecting **Select an existing instance** under **MySQL instance source**. ||
      ||**MySQL instance** |Select the target instance of NDB for MySQL from the drop\-down list.<br><br>The drop\-down list only shows the first 10 instances. You can also search for the target instance by instance ID or name. |
      ||**Database account** |Enter the database account of the target instance. |
      ||**Database password** |Enter the password corresponding to the database account of the target instance. |
      ||**Test connection**<br><br> |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
      ||When **Select instance configuration ** is selected for **MySQL instance** type, you need to configure **Compatible version**, **Specification type**, **Instance specification** and other information. ||
      ||**Compatible version** |Select the compatible version of the instance as needed. **MySQL 5.7** and **MySQL 8.0** are supported. |
      ||**Specification type** |Supports two specification types: **General type** and **Dedicated type**.<br><br><br>* **General type**: Exclusive use of allocated memory and storage resources, shares CPU resources with other shared instances in the same physical machine.CPU utilization is maximized through resource reuse, with high cost performance. CPU utilization is maximized through resource reuse, with high cost performance.<br><br>* **Dedicated type**: Fully exclusive use of allocated CPU, memory, and storage resources, with stable performance, not affected by other instances in the physical machine. |
      ||**Instance specification** |Select the instance specification configuration from the drop\-down list. |
      
      
      
      
      
      </Tab>
      </Tabs>
      

5. Click **Next step: configure migration evaluation object**.

6. On the **Configure migration evaluation object** wizard page, configure the following parameters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you do not need to start the migration task immediately, click save after configuring the migration evaluation objects, and then start it when you need to evaluate it. For details, refer to Starting a migration evaluation.   </div>
   

   
   |**Parameter** |**Description** |
   |---|---|
   |**Migration evaluation object** |In the **Migration evaluation object** area, select the databases to be evaluated for migration. Target objects can be queried by **Normal search** and **Global search**. |
   

7. Click **Next: view evaluation results**.

8. On the **View evaluation results** configuration wizard page, view the evaluation results of the migration task.

   You can modify the evaluation item that failed or has risk, and then click **Reevaluate** to evaluate again.

9. After completing the evaluation or confirming that the evaluation result is correct, you can click **Close**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

[Managing migration evaluation tasks](https://docs.byteplus.com/en/docs/DTS/Managing_migration_evaluation_tasks)

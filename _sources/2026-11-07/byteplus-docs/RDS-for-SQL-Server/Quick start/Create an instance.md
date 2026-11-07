---
title: "Create an instance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance"
---

Creating an instance is the first step to using RDS for SQL Server. This topic describes how to create an SQL Server instance.

<span id="Sfg2Au2A"></span>
## Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services on nodes in the Chinese mainland through BytePlus. For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).


<span id="FkH3BnDw"></span>
## Procedure


1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the project and region of the instance.

3. On the **Instances** page, click **Create an instance**.

4. On the **Create an instance** page, configure the following instance parameters.

   
   |**Category** |**Parameter** |**Description** |
   |---|---|---|
   |\- |**Database type** |Select **Microsoft SQL Server**. |
   |**Basic information** |**Instance name** |(Optional) Set an instance name. The naming rules are as follows:<br><br><br>* Can not start with digits or hyphen (\-).<br><br>* Must be 1 to 128 characters in length.<br><br>* Can only contain Chinese characters, letters, digits, underscores (_) and hyphens(\-).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not enter an instance name, it will be the same as the instance ID.</div><br> |
   ||**Compatible versions** |You can select **SQL Server 2019 Standard Edition**, **SQL Server 2019 Enterprise Edition**, **SQL Server 2019 Web Edition**, **SQL Server 2022 Standard Edition**, **SQL Server 2022 Enterprise Edition**, **SQL Server 2022 Web Edition**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">To create instances of SQL Server 2025 Standard Edition and SQL Server 2025 Enterprise Edition, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to the SQL Server technical team to be added to the allowlist. This feature is currently available on an allowlist.</div><br> |
   |**Specification configuration** |**Instance type** |Select an instance type as needed. The supported types are as follows: **High availability**, **Single node edition**, and **Cluster edition**.<br><br><br>* **High Availability**: A classic high\-availability architecture with one primary and one secondary node, suitable for production databases in large and medium\-sized enterprises for scenarios like the internet, IoT, retail e\-commerce, logistics, and gaming. You can select **High availability** as the **Instance type** when the **Compatible version** is **SQL Server 2019 Standard Edition**, **SQL Server 2022 Standard Edition** .<br><br>* **Single node edition**: It adopts a single node deployment architecture. Compared to typical primary and secondary instances, it comprises only one node while offering high cost\-performance ratio. It is suitable for personal learning, micro\-websites, and development and testing environments for small and medium\-sized enterprises. You can select **Single node edition** as the **Instance type** when the **Compatible version** is **SQL Server 2019 Standard Edition**, **SQL Server 2019 Enterprise Edition**, **SQL Server 2019 Web Edition**, **SQL Server 2022 Standard Edition**, **SQL Server 2022 Enterprise Edition**, **SQL Server 2022 Web Edition**  .<br><br>* **Cluster**: Features a high\-availability architecture with one primary, one standby, and multiple read\-only nodes. This edition is suitable for production databases in large and medium\-sized enterprises, such as those in the internet, hospitality, and online education industries. When the **Compatible version** is **SQL Server 2019 Enterprise Edition**, **SQL Server 2022 Enterprise Edition** or , you can select **High availability** as the **Instance type**. |
   ||**Specification family** |Optional: Select the **Include previous generations** radio button to choose a specification type that includes previous generations in the **Specification type** section.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When the selected <strong>Compatible version</strong> is later than SQL Server 2022 , the 1ie specification family of <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/master-instance-specification?lang=zh#Jwh2eKoh">historical generation specifications</a> is not supported.</div><br> |
   ||**Specification type** |The specification type is **Exclusive Type** by default. If you click the **Include previous generation specifications** radio button above:<br><br><br>* When the **Compatible version** is later than SQL Server 2022, the **Specification type** only supports **Exclusive Type.** <br><br>* When the **Compatible version** is SQL Server 2022 or earlier, the **Specification type** supports    . **Exclusive Type II**, **General Type II.**  The details are as follows:<br><br>   * **Exclusive Type II**: Exclusive type instance performance is better and more stable, suitable for business scenarios with database as the core system, such as finance, e\-commerce, government affairs, large and medium\-sized Internet business.<br><br>   * **General Type II**: General type instance is suitable for scenarios with high requirements for cost efficiency and budget optimization.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about each specification type, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/product-specification-family">Product specification family</a>.</div><br> |
   ||**Node specification** |Configure the node specifications and availability zones for the instance's primary and secondary nodes as needed. The details are as follows:<br><br><br>* **Node specification**: Click the dropdown list to set the node specifications for the primary and secondary nodes. The secondary node's specification is the same as the primary node's by default.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more details about node specifications, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/master-instance-specification?lang=en">Primary instance specifications</a>.   </div><br>   <br><br>* **Availability zones**: Select the availability zone for the node from the drop\-down list. The availability zone is the geographic location of the node. If an instance has primary and secondary nodes, you can deploy them across different availability zones.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Select an availability zone close to your target users to improve access speed.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The availability zone can not be modified after the instance is created successfully.   </div><br>    |
   ||**Storage Type** |Only **Extremely\-Fast SSD PL1 Cloud Disk** is currently supported. |
   ||**Storage space** |Storage space includes data file space and temporary file space. Enter a storage space between 20 GiB and 4000 GiB in 10 GiB increments. Select a value based on your business needs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For the storage space range of each specification, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/master-instance-specification">Primary instance specifications</a>.</div><br> |
   |**Network configuration** |**VPC** |Select the VPC for the instance from the dropdown list. You can also click **Create VPC** on the right to create a VPC. For more information, see [Create a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">VPC stands for Virtual Private Cloud. A VPC is an isolated network environment that offers higher security and better performance than a traditional classic network.</div><br> |
   ||**Subnet** |The subnets vary depending on the availability zones selected for the primary and secondary nodes, as follows:<br><br><br>* If the primary and secondary nodes are in the same availability zone, the field is displayed as **Subnet**. Select an available subnet in the VPC from the drop\-down list.<br><br>* If the primary and secondary nodes are in different availability zones, the fields are displayed as **Primary node subnet** and **Secondary node subnet**. From their respective drop\-down lists, select an available subnet in the VPC for the primary and secondary nodes.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A subnet is a block of IP addresses within a VPC. All cloud resources in the VPC must be deployed in a subnet. The subnet assigns private IP addresses to cloud resources. For more information, see <a href="https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet">Create a subnet</a>.</div><br> |
   ||**Allowlist** |Associate an allowlist with the instance. Click the allowlist text box to go to the Associate allowlist page. On this page, select an allowlist and click Confirm. You will return to the Create instance page, and the selected allowlist will appear in the allowlist text box.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can also create a new allowlist on the Associate allowlist page. For more information about creating an allowlist, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-allowlist">Create an allowlist</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">An instance can bind a maximum of 100 allowlists.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>×</strong> next to the allowlist to remove it.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If a default allowlist is set for the current account, it will appear in the allowlist box.</div><br> |
   |**Account configuration** |**Super account** |The system selects **veyun_user** by default and this cannot be modified. |
   ||**Super account password** |Set the password for the super account. The requirements are as follows:<br><br><br>* It must contain at least three of the following character types: uppercase letters, lowercase letters, numbers, and special characters.<br><br>* Special characters include `~!@#$%^*-_+?`.<br><br>* It must be 8 to 32 characters long.<br><br>* It cannot contain the string `veyun_user` (case\-insensitive). |
   ||**Confirm password** |Enter the password again. |
   |**Advanced configuration** |**Time zone** |The only supported time zone is  **(UTC+08:00) Beijing**, **Chongqing**, **Hong Kong**, **Urumqi**. |
   ||**Instance character set** |Select the character set for the instance database. Supported options include **Chinese_PRC_90_CI_AI**, **Chinese_PRC_BIN**, **Chinese_PRC_BIN2**, **Chinese_PRC_CI_AI**, **Chinese_PRC_CI_AS**, **Chinese_PRC_CS_AS**, **Chinese_Taiwan_Stroke_CI_AS**, **Chinese_Taiwan_Stroke_CS_AS**, **Cyrillic_General_CI_AS**, **Japanese_CI_AS**, **Japanese_CS_AS**, **Latin1_General_100_CI_AS_SC_UTF8, Latin1_General_CI_AS**, **Latin1_General_CS_AS**, **SQL_Latin1_General_CP1_CI_AS**, **SQL_Latin1_General_CP1_CS_AS**, and **Thai_CI_AS**. The default is **Chinese_PRC_CI_AS**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The instance character set can not be modified after the instance is successfully created.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Even if you select a case\-sensitive instance character set, creating case\-sensitive databases is not supported. For example, databases named <code>A</code> and <code>a</code> will be treated as the same database.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For more information about the instance character set, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide?lang=en#PkNxJyXS">References</a>.</div><br> |
   ||**Maintenance window** |Confirm the maintenance window for the instance. To modify, click **Modify**. In the **Modify maintenance period** dialog box, set the **Maintenance window** and click **OK**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The system performs periodic maintenance on instances to ensure the stability of cloud databases. Set the maintenance window during off\-peak hours to avoid affecting your business.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">During the maintenance window, your instance may experience 1 to 2 transient disconnections. Ensure your application has an automatic reconnection mechanism.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The maintenance window duration ranges from 1 to 24 hours. The selected time range can not span across two days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can modify the maintenance window of an instance after it has been created. For more information, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/configuring-maintenance-window">Set maintenance window</a>.</div><br> |
   ||**Project** |Select a project for this instance from the dropdown list. The default project is **default**. You can also click **Create new project** to create a new project. For detailed instructions, see [Creating project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management#creating-project).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A project is a virtual concept that includes a set of resources, users, and roles. Projects allow you to centrally view and manage a group of resources and control the permissions of users and roles on these resources within the project. For more information, see <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management">Project resource management</a>.</div><br> |
   ||**Tag** |(Optional) Add tags to the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Tags help identify and categorize cloud resources. RDS for SQL Server lets you add tags to instances for classification, simplifying instance searches and resource aggregation. For more information, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/tag-overview">Tag overview</a>.</div><br> |
   |**Billing information** |**Billing methods** |You can select either **pay\-as\-you\-go** or **subscription**. If you select **subscription**, you need to set the **subscription duration**. You can also select **auto\-renewal**, and the system will automatically renew the instance before it expires.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can also create a pay\-as\-you\-go instance and switch to a subscription after confirming it meets your requirements. For more billing information, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/price-overview">Billing overview</a>.</div><br> |
   | **\-**  |**Quantity** |Select the number of instances to create in the lower\-left corner of the page. You can create up to 10 instances in a batch.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">By default, each BytePlus primary account can purchase up to 30 instances in each region. If you need to increase your quota to purchase more instances, go to the Quota Center to submit a <a href="https://console.byteplus.com/quota/productList/coParameterList?ServiceCode=redis">Quota application</a>.</div><br> |
   

5. Click **Confirm order**.

6. Complete the following steps based on the selected billing method.

   * If the instance's billing method is **Pay\-as\-you\-go**: On the **Confirm Order** page, confirm the order details, select the checkbox to agree to  , [BytePlus Customer Agreement](https://docs.byteplus.com/en/docs/legal/docs-customer-agreement), [Service Specific Terms](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/specific-terms-for-bytePlus-database-products-and-services), and [SLA for RDS for SQL Server](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/service-level-agreement-for-RDS-for-SQL-Server), then click **Buy Now**.

   * If the instance's billing method is **Subscription**:

      1. On the **Confirm Order** page, confirm the order details, read and select [BytePlus Customer Agreement](https://docs.byteplus.com/en/docs/legal/docs-customer-agreement),[ Service Specific Terms](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/specific-terms-for-bytePlus-database-products-and-services), [SLA for RDS for SQL Server](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/service-level-agreement-for-RDS-for-SQL-Server), and click **Submit Order**.

      2. On the **Confirm order Information** page, confirm the order information again, and click **Next**.

      3. On the **Submit payment information** page, confirm the payment details, select a payment method, click **Go to Pay**, and follow the prompts to complete the payment and create the instance.


<span id="3yBoXehK"></span>
## Next steps

<span id="hRRDDfJ7"></span>
### View instance information


1. On the **Instances** page, click the target instance name to go to the **Summary** page.

2. On the **Summary** page, you can view the **Summary**, **Configuration information**, and **Usage statistics**. For more information, see [View instances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-instance-details).


<span id="f6zdVeqx"></span>
## Reference content

<span id="BY9Usxnz"></span>
### Instance character set

The following table shows the instance character sets that RDS for SQL Server currently supports.


|**Instance character set** |**Description** |
|---|---|
|Chinese_PRC_90_CI_AI |Chinese\-PRC (Simplified Chinese), case\-insensitive, accent\-insensitive (compatible with SQL Server 2005). |
|Chinese_PRC_CI_AI |Chinese\-PRC (Simplified Chinese), case\-insensitive, accent\-insensitive. |
|Chinese_PRC_CI_AS |Chinese\-PRC (Simplified Chinese), case\-insensitive, accent\-sensitive. |
|Chinese_PRC_CS_AS |Chinese\-PRC (Simplified Chinese), case\-sensitive, accent\-sensitive. |
|Chinese_PRC_BIN |Chinese\-PRC (Simplified Chinese), binary comparison, case\-sensitive, and accent\-sensitive. |
|Chinese_PRC_BIN2 |Chinese\-PRC (Simplified Chinese), binary comparison, case\-sensitive, and accent\-sensitive. BIN2 provides more accurate sorting for Unicode characters. |
|Cyrillic_General_CI_AS |Cyrillic_General (Cyrillic character set), case\-insensitive, accent\-sensitive. |
|Latin1_General_100_CI_AS_SC_UTF8 |Latin1_General (Latin character set), case\-insensitive, accent\-sensitive, with support for supplementary Unicode characters and UTF\-8 encoding. |
|Latin1_General_CI_AS |Latin1_General (Latin character set), case\-insensitive and accent\-sensitive. |
|Latin1_General_CS_AS |Latin1_General (Latin character set), case\-sensitive and accent\-sensitive. |
|SQL_Latin1_General_CP1_CI_AS |For Unicode data, the character set is Latin1_General (Latin character set), which is case\-insensitive and accent\-sensitive. |
|SQL_Latin1_General_CP1_CS_AS |Latin1_General (Latin character set) for Unicode data, case\-sensitive, and accent\-sensitive. |
|Japanese_CI_AS |Japanese, case\-insensitive, accent\-sensitive. |
|Japanese_CS_AS |Japanese, case\-sensitive, accent\-sensitive. |
|Chinese_Taiwan_Stroke_CI_AS |Chinese_Taiwan (Traditional Chinese), case\-insensitive, accent\-sensitive. |
|Chinese_Taiwan_Stroke_CS_AS |Chinese_Taiwan (Traditional Chinese), case\-sensitive and accent\-sensitive. |
|Thai_CI_AS |Thai (Thai), case\-insensitive, accent\-sensitive. |


The collation and suffix of the instance character set, and the server\-level collation are as follows:


* Character set collation

   
   |Collation options |Description |
   |---|---|
   |Case\-sensitive (_CS) |Distinguishes between uppercase and lowercase letters.<br><br><br>* If specified, lowercase letters are sorted before their corresponding uppercase letters.<br><br>* If this option is not specified, sorting will be case\-insensitive. That is, RDS for SQL Server treats uppercase and lowercase letters as the same during sorting.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can select case\-insensitivity by specifying _CI.</div><br> |
   |Accent\-sensitive (_AS) |Distinguishes between accented and non\-accented characters. For example, `a` and `á` are different characters. If this option is not specified, the collation is accent\-insensitive. RDS for SQL Server treats accented and unaccented forms of letters as identical during sorting.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can select accent\-insensitivity by specifying _AI.</div><br> |
   |Strictly case\-sensitive (_BIN) |Binary collation is strictly case\-sensitive and accent\-sensitive. It treats uppercase and lowercase letters, as well as accented and unaccented characters, as different characters. For example, A and a are treated as different characters, and `a` and `á` are also treated as different characters. |
   

* Instance character set suffix

   
   |**Instance character set suffix** |**Description** |
   |---|---|
   |_CI_AS |Case\-insensitive and accent\-sensitive. |
   |_CS_AS |Case\-sensitive and accent\-sensitive. |
   |_CI_AI |Case\-insensitive, accent\-insensitive. |
   |_SC_UTF8 |Supports Unicode supplementary characters and UTF\-8 encoding. |
   

* Server\-level collation

   The table below lists the default collations for some operating systems.

   
   |**Windows regional settings** |**Default collation** |
   |---|---|
   |Afrikaans (South Africa) |Latin1_General_CI_AS |
   |Alsatian (France) |Latin1_General_CI_AS |
   |Basque (Basque) |Latin1_General_CI_AS |
   |Bosnian (Bosnia and Herzegovina, Latin) |Latin1_General_CI_AS |
   |Bulgarian (Bulgaria) |Cyrillic_General_CI_AS |
   |Chinese (Macao SAR) |Latin1_General_CI_AI |
   |Chinese (People's Republic of China) |Chinese_PRC_CI_AS |
   |Dutch (Netherlands) |Latin1_General_CI_AS |
   |English (Australia) |Latin1_General_CI_AS |
   |English (India) |Latin1_General_CI_AS |
   |English (Canada) |Latin1_General_CI_AS |
   |English (New Zealand) |Latin1_General_CI_AS |
   |English (UK) |Latin1_General_CI_AS |
   |English (United States) |Latin1_General_CI_AS |
   |Filipino (Philippines) |Latin1_General_CI_AS |
   |Italian |Latin1_General_CI_AS |
   |Thai (Thailand) |Thai_CI_AS |

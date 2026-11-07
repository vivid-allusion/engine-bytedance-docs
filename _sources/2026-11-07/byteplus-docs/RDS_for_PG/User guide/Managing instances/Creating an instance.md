---
title: "Creating an instance"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance"
---

Creating an instance is the first step when using RDS for PostgreSQL. This topic describes how to create a database for PostgreSQL instance.

## Prerequisites

* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services on regions in the Chinese mainland through BytePlus. For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* VPC service access authorization has been completed. For the authorization method, refer to [Cross-service access authorization](https://docs.byteplus.com/en/docs/RDS_for_MySQL/cross-service_access_authorization).

## Procedure

1. Login to the [RDS for PostgreSQL](https://console.byteplus.com/db/rds-pg) console.

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   * > In subsequent steps, only the VPCs and subnets under the selected project can be selected.

   * > In subsequent steps, the project to which the instance belongs can be reselected.

4. On the **Instances** page, click **Create instance**.

5. On the **Create instance** page, set the following instance parameters.

   |Parameter |Is it required? |Note |
   |---|---|---|
   |Instance name |No |Set the instance name. When empty, the instance ID is named. Naming rules are as follows:<br><br><br>* Cannot start with a digit or a hyphen (\-).<br><br>* Can only contain Chinese characters, English letters, digits, underscores (_) and hyphens(\-).<br><br>* Must be 1 to 128 characters in length. |
   |Compatible version |Yes |Select the compatible version for the instance. You can choose **PostgreSQL 11**, **PostgreSQL 12**, **PostgreSQL 13**, **PostgreSQL 14**, **PostgreSQL 15**, **PostgreSQL 16, PostgreSQL 17**, or **PostgreSQL 18**.<br><br>> **warning**<br><br><br>> If you need to enable TDE encryption, only **PostgreSQL 17** is supported.<br> |
   |Instance types |Yes |High\-availability version: the classic high\-availability architecture that contains one primary node and one secondary node. |
   |Availability zone |Yes |The region and AZ of the instance, that is, the geographical location of the instance.Availability zone<br><br>> **tip**<br><br><br><br>* > The instance region and AZ cannot be changed after the instance purchase.<br><br><br>* > Select a nearby region based on the geographical location of your target users to speed up users' access.<br><br><br>* > Make sure that the PostgreSQL instance is in the same region as the ECS instance to connect to. Otherwise, they cannot be connected through the private network, and can only be connected via Internet, which undermines their performance.<br> |
   |Node specification |Yes |Select the specification and AZ of the primary node, and select the specification of the read\-only node. You can click "+" at the bottom left to add a read\-only node. Parameter configuration rules:<br><br><br>* The specifications of the secondary and primary nodes must be consistent.<br><br>* The specification of a read\-only node must be greater than or equal to that of the primary node.<br><br>* You can add up to 10 read\-only nodes.<br><br>* Primary, secondary, and read\-only nodes can be deployed in different availability zones within the same region. |
   |Storage type |Yes |**Local SSD disk** is supported, and the SSD must be in the same node as the database engine. Storing data in the local SSD disk can reduce I/O delay. |
   |Storage space |Yes |Select the storage space for the instance. Storage space includes data space, log space, WAL log space, and transaction file space. The storage space ranges from 20 to 12,000 GB. Select reasonably based on business needs.<br><br>> **tip**<br><br><br><br>* > Different specifications have different storage space value ranges. For detailed information on storage space value ranges, refer to [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications).<br><br><br>* > Storage space above 3000 GB is currently an allowlisted feature, available only in the China (Beijing), China (Shanghai), and China (Guangzhou) regions. If you need to use this feature, [submit a ticket](https://console.byteplus.com/workorder/create) to contact us.<br><br><br>* > Supports automatic expansion of storage space. For specific operations, refer to [storage space expansion management](https://docs.byteplus.com/en/docs/DBW/Storage_expansion_management_pg). If you enabled automatic storage expansion rules for your instance and later obtained authorization for a larger storage capacity, manually adjust the expansion limit. Otherwise, the rule will cap capacity at 3000 GB and fail to expand to your authorized storage size.<br> |
   |Virtual private cloud |Yes |Select the VPC used by the instance.<br><br>> **tip**<br><br><br><br>* > **Virtual Private Cloud (VPC)**, is an isolated network environment with higher security and performance than traditional classical networks. You can create a new private network by clicking **Create VPC** on the right. For more details, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).<br><br><br>* > Only the virtual private cloud under the project specified in the navigation bar is supported for selection.<br> |
   |Subnet |Yes |Select the subnets available to the instance in the VPC.<br><br>> **tip**<br><br><br><br>* > A subnet is a CIDR block in the VPC. All cloud resources in the VPC must be deployed in subnets, which assign VPC IP addresses to the cloud resources. You can create a new subnet by clicking**Create subnet** on the right. For more details, see [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).<br><br><br>* > Only subnets in the availability zone where the instance is located can be selected.<br><br><br>* > Subnets and virtual private clouds can belong to different projects, but RDS for PostgreSQL instances can only use subnets and virtual private clouds under the same project. Notice that the target subnet and the selected virtual private cloud belong to the same project. You can verify this in the [Project console](https://console.byteplus.com/iam/resourcemanage/project).<br> |
   |Allowlists |No |Click the allowlist text box to go to the **Associate allowlist** page. Under this page, after checking the allowlist, click **OK** and go back to **Create instance** page. The selected allowlist will be displayed in the allowlist text box.<br><br>> **tip**<br><br><br><br>* > On the **Associate allowlist** page, you can also create a new allowlist. For more information about creating an allowlist, see [Creating an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/adding_an_ip_address_allowlist).<br><br><br>* > An instance can associate up to 100 allowlists.<br><br><br>* > Click the × after the allowlist to remove the allowlist.<br><br><br>* > If there is a default allowlist set under the current account, the allowlist will appear in the allowlist text box.<br> |
   |Maintenance window |No |Confirm the maintenance window for the instance. To modify, click the edit button to enter the maintenance window, set **Maintainable day** and **Maintenance window**, then click **OK**.<br><br>> **tip**<br><br><br><br>* > At least one day and up to seven days per week can be set as maintainable days.<br><br><br>* > The maintenance window can only be set from 00:00 to 05:59 (UTC+08:00).<br><br><br>* > The minimum duration of the maintenance window is 2 hours and the maximum duration is 6 hours. Cross\-day settings are not allowed.<br><br><br>* > After an instance is created, you can modify the maintenance window of the instance again. For details, refer to [Configuring maintenance window.](https://docs.byteplus.com/en/docs/RDS_for_PG/Configuring_maintenance_window)<br> |
   |Data encryption |No |Whether to enable the TDE encryption feature. It is disabled by default. After enabling, select the keyring and key in the pop\-up **Enable transparent data encryption (TDE) function** dialog box.<br><br>> **warning**<br><br><br><br>* > TDE encryption is currently in invitation\-only testing. To use it, [submit a ticket](https://console.byteplus.com/workorder/create).<br><br><br>* > TDE encryption cannot be disabled once enabled.<br> |
   |Affiliated project |Yes |Select the project to which the instance belongs.<br><br>> **tip**<br><br><br><br>* > A project is a virtual concept that includes a set of resources, users, and roles. A project allows you to view and manage a group of resources in a unified manner and control the permissions of users and roles to these resources. For more details, refer to [Resource management](https://docs.byteplus.com/en/docs/6649/94333).<br><br><br>* > RDS for PostgreSQL will assign the newly created instance to the "default" project by default. You can adjust the instance's project during or after the creation process.<br> |
   |Tag |No |Add tag(s) to the instance. Tags are used for the identification and classification of cloud resources. RDS for PostgreSQL supports adding tags to instances. You can classify PostgreSQL instances by tags to facilitate instance search and resource aggregation. For more information, see [Tag overview](https://docs.byteplus.com/en/docs/RDS_for_PG/overview).<br><br>> **tip**<br><br><br>> If you need to separate accounts by tags, you need to enable tags in [Bill management \> Bill tags](https://console.byteplus.com/finance/bill/tag/) to apply corresponding tags to bill details. For more details, see [Tag\-based bill splitting for instances](https://docs.byteplus.com/en/docs/RDS_for_PG/tag-based_bill_splitting_for_instances).<br> |
   |Billing method |Yes |RDS for PostgreSQL supports two billing methods: pay\-as\-you\-go and subscription.<br><br><br>* Pay\-as\-you\-go: If you plan to use your PostgreSQL instance for a short period of time, choose pay\-as\-you\-go (hourly rate). You can save money by releasing the instance when you no longer need it.<br><br>* Subscription: If you plan to use your PostgreSQL instance for a long period of time, select Subscription (one\-time payment) and choose the duration of the purchase in the lower left corner of the page. Subscription is more affordable than pay\-as\-you\-go, and the longer you buy, the more discounts you get.<br><br><br>> **tip**<br><br><br>> You can also create a pay\-as\-you\-go instance first and confirm that the instance meets the requirements before switching to a yearly/monthly subscription. If you choose pay\-as\-you\-go billing, make sure your BytePlus account balance is at least 100 USD. For more information on billing, see[Billing overview](https://docs.byteplus.com/en/docs/RDS_for_PG/price_overview).<br> |
   |Subscription duration |No |If the billing method is **Subscription**, select the subscription duration. Support monthly purchase (can purchase 1~9 months) and yearly purchase (can purchase 1~3 years). |
   |Automatic renewal |No |If you select the billing method as **Subscription**, you can check the option for **Automatic renewal**. After checking, the platform will automatically renew the instance monthly before expiration without manual renewal. You can also modify the renewal configuration. For more information, refer to [Renewal management](https://docs.byteplus.com/en/docs/RDS_for_PG/renewal_management). |
   |Quantity |No |Choose the number of instances. Up to 20 instances can be created at once.<br><br>> **tip**<br><br><br>> Each BytePlus account can purchase up to 50 instances in each region by default. To increase the quota, apply in [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=rds_pg).<br> |

6. Click **Confirm order**.

7. Complete the next steps based on the selected billing method.

   * If you select **Pay\-as\-you\-go**: On the **Confirm order** page, confirm the order details. Read and check the **Database Product and Services Terms**, and click **Buy now** to create a new instance.

   * If you select **Subscription**:

      * On the **Confirm order** page, confirm the order details. Read and check the **Database Product and Services Terms**, and click **Submit the order**.

      * On the **Confirm order information** page, confirm the order information again and click **Next step**.

      * On the **Submit payment information** page, confirm the payment details and select the payment method. Click **Go to pay**, and create a new instance after completing the payment according to the prompts.

##

## Procedure

1. Login to the [RDS for PostgreSQL](https://console.byteplus.com/db/rds-pg) console.

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   * > In subsequent steps, only the VPCs and subnets under the selected project can be selected.

   * > In subsequent steps, the project to which the instance belongs can be reselected.

4. On the **Instances** page, click **Create instance**.

5. On the **Create instance** page, set the following instance parameters.

   |Parameter |Is it required? |Note |
   |---|---|---|
   |Instance name |No |Set the instance name. When empty, the instance ID is named. Naming rules are as follows:<br><br><br>* Cannot start with a digit or a hyphen (\-).<br><br>* Can only contain Chinese characters, English letters, digits, underscores (_) and hyphens(\-).<br><br>* Must be 1 to 128 characters in length. |
   |Compatible version |Yes |Select the compatible version for the instance. You can choose **PostgreSQL 11**, **PostgreSQL 12**, **PostgreSQL 13**, **PostgreSQL 14**, **PostgreSQL 15**, **PostgreSQL 16, PostgreSQL 17**, or **PostgreSQL 18**.<br><br>> **warning**<br><br><br>> If you need to enable TDE encryption, only **PostgreSQL 17** is supported.<br> |
   |Instance types |Yes |High\-availability version: the classic high\-availability architecture that contains one primary node and one secondary node. |
   |Availability zone |Yes |The region and AZ of the instance, that is, the geographical location of the instance.Availability zone<br><br>> **tip**<br><br><br><br>* > The instance region and AZ cannot be changed after the instance purchase.<br><br><br>* > Select a nearby region based on the geographical location of your target users to speed up users' access.<br><br><br>* > Make sure that the PostgreSQL instance is in the same region as the ECS instance to connect to. Otherwise, they cannot be connected through the private network, and can only be connected via Internet, which undermines their performance.<br> |
   |Node specification |Yes |Select the specification and AZ of the primary node, and select the specification of the read\-only node. You can click "+" at the bottom left to add a read\-only node. Parameter configuration rules:<br><br><br>* The specifications of the secondary and primary nodes must be consistent.<br><br>* The specification of a read\-only node must be greater than or equal to that of the primary node.<br><br>* You can add up to 10 read\-only nodes.<br><br>* Primary, secondary, and read\-only nodes can be deployed in different availability zones within the same region. |
   |Storage type |Yes |**Local SSD disk** is supported, and the SSD must be in the same node as the database engine. Storing data in the local SSD disk can reduce I/O delay. |
   |Storage space |Yes |Select the storage space for the instance. Storage space includes data space, log space, WAL log space, and transaction file space. The storage space ranges from 20 to 12,000 GB. Select reasonably based on business needs.<br><br>> **tip**<br><br><br><br>* > Different specifications have different storage space value ranges. For detailed information on storage space value ranges, refer to [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications).<br><br><br>* > Storage space above 3000 GB is currently an allowlisted feature, available only in the China (Beijing), China (Shanghai), and China (Guangzhou) regions. If you need to use this feature, [submit a ticket](https://console.byteplus.com/workorder/create) to contact us.<br><br><br>* > Supports automatic expansion of storage space. For specific operations, refer to [storage space expansion management](https://docs.byteplus.com/en/docs/DBW/Storage_expansion_management_pg). If you enabled automatic storage expansion rules for your instance and later obtained authorization for a larger storage capacity, manually adjust the expansion limit. Otherwise, the rule will cap capacity at 3000 GB and fail to expand to your authorized storage size.<br> |
   |Virtual private cloud |Yes |Select the VPC used by the instance.<br><br>> **tip**<br><br><br><br>* > **Virtual Private Cloud (VPC)**, is an isolated network environment with higher security and performance than traditional classical networks. You can create a new private network by clicking **Create VPC** on the right. For more details, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).<br><br><br>* > Only the virtual private cloud under the project specified in the navigation bar is supported for selection.<br> |
   |Subnet |Yes |Select the subnets available to the instance in the VPC.<br><br>> **tip**<br><br><br><br>* > A subnet is a CIDR block in the VPC. All cloud resources in the VPC must be deployed in subnets, which assign VPC IP addresses to the cloud resources. You can create a new subnet by clicking**Create subnet** on the right. For more details, see [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).<br><br><br>* > Only subnets in the availability zone where the instance is located can be selected.<br><br><br>* > Subnets and virtual private clouds can belong to different projects, but RDS for PostgreSQL instances can only use subnets and virtual private clouds under the same project. Notice that the target subnet and the selected virtual private cloud belong to the same project. You can verify this in the [Project console](https://console.byteplus.com/iam/resourcemanage/project).<br> |
   |Allowlists |No |Click the allowlist text box to go to the **Associate allowlist** page. Under this page, after checking the allowlist, click **OK** and go back to **Create instance** page. The selected allowlist will be displayed in the allowlist text box.<br><br>> **tip**<br><br><br><br>* > On the **Associate allowlist** page, you can also create a new allowlist. For more information about creating an allowlist, see [Creating an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/adding_an_ip_address_allowlist).<br><br><br>* > An instance can associate up to 100 allowlists.<br><br><br>* > Click the × after the allowlist to remove the allowlist.<br><br><br>* > If there is a default allowlist set under the current account, the allowlist will appear in the allowlist text box.<br> |
   |Maintenance window |No |Confirm the maintenance window for the instance. To modify, click the edit button to enter the maintenance window, set **Maintainable day** and **Maintenance window**, then click **OK**.<br><br>> **tip**<br><br><br><br>* > At least one day and up to seven days per week can be set as maintainable days.<br><br><br>* > The maintenance window can only be set from 00:00 to 05:59 (UTC+08:00).<br><br><br>* > The minimum duration of the maintenance window is 2 hours and the maximum duration is 6 hours. Cross\-day settings are not allowed.<br><br><br>* > After an instance is created, you can modify the maintenance window of the instance again. For details, refer to [Configuring maintenance window.](https://docs.byteplus.com/en/docs/RDS_for_PG/Configuring_maintenance_window)<br> |
   |Data encryption |No |Whether to enable the TDE encryption feature. It is disabled by default. After enabling, select the keyring and key in the pop\-up **Enable transparent data encryption (TDE) function** dialog box.<br><br>> **warning**<br><br><br><br>* > TDE encryption is currently in invitation\-only testing. To use it, [submit a ticket](https://console.byteplus.com/workorder/create).<br><br><br>* > TDE encryption cannot be disabled once enabled.<br> |
   |Affiliated project |Yes |Select the project to which the instance belongs.<br><br>> **tip**<br><br><br><br>* > A project is a virtual concept that includes a set of resources, users, and roles. A project allows you to view and manage a group of resources in a unified manner and control the permissions of users and roles to these resources. For more details, refer to [Resource management](https://docs.byteplus.com/en/docs/6649/94333).<br><br><br>* > RDS for PostgreSQL will assign the newly created instance to the "default" project by default. You can adjust the instance's project during or after the creation process.<br> |
   |Tag |No |Add tag(s) to the instance. Tags are used for the identification and classification of cloud resources. RDS for PostgreSQL supports adding tags to instances. You can classify PostgreSQL instances by tags to facilitate instance search and resource aggregation. For more information, see [Tag overview](https://docs.byteplus.com/en/docs/RDS_for_PG/overview).<br><br>> **tip**<br><br><br>> If you need to separate accounts by tags, you need to enable tags in [Bill management \> Bill tags](https://console.byteplus.com/finance/bill/tag/) to apply corresponding tags to bill details. For more details, see [Tag\-based bill splitting for instances](https://docs.byteplus.com/en/docs/RDS_for_PG/tag-based_bill_splitting_for_instances).<br> |
   |Billing method |Yes |RDS for PostgreSQL supports two billing methods: pay\-as\-you\-go and subscription.<br><br><br>* Pay\-as\-you\-go: If you plan to use your PostgreSQL instance for a short period of time, choose pay\-as\-you\-go (hourly rate). You can save money by releasing the instance when you no longer need it.<br><br>* Subscription: If you plan to use your PostgreSQL instance for a long period of time, select Subscription (one\-time payment) and choose the duration of the purchase in the lower left corner of the page. Subscription is more affordable than pay\-as\-you\-go, and the longer you buy, the more discounts you get.<br><br><br>> **tip**<br><br><br>> You can also create a pay\-as\-you\-go instance first and confirm that the instance meets the requirements before switching to a yearly/monthly subscription. If you choose pay\-as\-you\-go billing, make sure your BytePlus account balance is at least 100 USD. For more information on billing, see[Billing overview](https://docs.byteplus.com/en/docs/RDS_for_PG/price_overview).<br> |
   |Subscription duration |No |If the billing method is **Subscription**, select the subscription duration. Support monthly purchase (can purchase 1~9 months) and yearly purchase (can purchase 1~3 years). |
   |Automatic renewal |No |If you select the billing method as **Subscription**, you can check the option for **Automatic renewal**. After checking, the platform will automatically renew the instance monthly before expiration without manual renewal. You can also modify the renewal configuration. For more information, refer to [Renewal management](https://docs.byteplus.com/en/docs/RDS_for_PG/renewal_management). |
   |Quantity |No |Choose the number of instances. Up to 20 instances can be created at once.<br><br>> **tip**<br><br><br>> Each BytePlus account can purchase up to 50 instances in each region by default. To increase the quota, apply in [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=rds_pg).<br> |

6. Click **Confirm order**.

7. Complete the next steps based on the selected billing method.

   * If you select **Pay\-as\-you\-go**: On the **Confirm order** page, confirm the order details. Read and check the **Database Product and Services Terms**, and click **Buy now** to create a new instance.

   * If you select **Subscription**:

      * On the **Confirm order** page, confirm the order details. Read and check the **Database Product and Services Terms**, and click **Submit the order**.

      * On the **Confirm order information** page, confirm the order information again and click **Next step**.

      * On the **Submit payment information** page, confirm the payment details and select the payment method. Click **Go to pay**, and create a new instance after completing the payment according to the prompts.

## Next steps

* [Viewing instance list](https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_instance_list)

* [View instance details](https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_the_details_of_an_instance)

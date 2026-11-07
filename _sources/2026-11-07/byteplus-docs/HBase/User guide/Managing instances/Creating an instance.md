---
title: "Creating an instance"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Creating_an_instance_1"
---


Creating an instance is the first step for using Table Storage for HBase. This topic describes how to create an HBase instance.

<span id="1OU9U2QD"></span>
## Prerequisites


* A BytePlus account has been registered. For account registration, refer to [How to Register an Account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account#create-byteplus-account).

* VPC and subnet have been created. See [Creating VPC](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC).

* If you use sub\-user to manage HBase instances, you need to grant sub\-user relevant permissions, see [Using HBase with sub-accounts](https://docs.byteplus.com/en/docs/HBase/Using_HBase_with_sub-accounts).


<span id="1SIyTLRQ"></span>
## Precautions

Currently, the Table Storage for HBase is in gray\-scale release. If you need to use it, [submit a ticket](https://console.byteplus.com/workorder/create/) and contact technical support to apply for usage.

<span id="w5yn4fNb"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click **Create instance**.

4. On the **Create instanc**e page, set the following parameters.

   
   |Classification |Parameter |Description |
   |---|---|---|
   |**Basic information** |Instance name |Enter an instance name. Optional. If the instance name is not set, the instance is named with the instance ID. The naming convention is as follows:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* It must be 1 to 128 characters in length. |
   ||Instance type |Currently only the **Standard** is supported, no selection is required. |
   ||Database version |Only **HBase 2.0** is supported, no selection is required. |
   ||Instance specification |For the **Master** node, you need to select the following configuration:<br><br><br>* **Node specifications**: Select the resource specifications for the Master node. For more information about Master node specifications, see [Product specifications](https://docs.byteplus.com/en/docs/HBase/Product_specifications).<br><br>* **Number of nodes**: The number of Master nodes is fixed and does not need to be selected. High availability is supported by default. |
   |||For **Region Server** nodes, you need to select the following configuration:<br><br><br>* **Node specifications**: Select the resource specifications for the Region Server node. For more information about Region Server node specifications, see [Product specifications](https://docs.byteplus.com/en/docs/HBase/Product_specifications).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In a production environment, it is recommended that Region Server nodes use 16 cores or above.   </div><br>   <br><br>* **Number of nodes**: Select the number of Region Server nodes. The default number of Region Server nodes is 2, and the value range is 2 to 100. |
   ||Storage type |Select the storage type, value:<br><br><br>* **HDD disk**: HDD disk has large storage capacity and is cheaper than SSD disk. It is suitable for scenarios that require long\-term storage of large amounts of data and have high cost\-effectiveness requirements.<br><br>* **SSD disk**: SSD disk has fast read and write speed, low latency, and high stability. It is suitable for scenarios that require frequent read and write and have high stability requirements. |
   ||Storage space |Select the storage space for the instance in increments of 10 GiB, and the value range is 100 GiB to 20,000 GiB.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The default storage limit for HDD and SSD file storage for all instance types is 20,000 GiB. You can <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support to increase the limit.</div><br> |
   ||Enable Capacity storage |For a detailed introduction to Capacity storage, see [About hot and cold data separation](https://docs.byteplus.com/en/docs/HBase/About_hot_and_cold_data_separation).<br><br><br>* Select **Yes** to enable Capacity storage (enable hot and cold storage separation) and set the Capacity storage space size. The value range is: 800 GiB to 1,000,000 GiB, in steps of 10 GiB.<br><br>* Select **No** (default) to not enable Capacity storage. You can also enable Capacity storage for an instance at any time after creating it. For more information, see [Enabling Capacity storage](https://docs.byteplus.com/en/docs/HBase/Enabling_Capacity_storage).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The hot and cold data separation function is supported only when the deployment plan is single availability zone deployment.</div><br> |
   |**Network configuration** |Virtual private cloud |Select the target VPC from the drop\-down list, and depending on the item you selected in the upper left corner of the console, the following will happen:<br><br><br>* If you select **All resources**, you can select the VPC of all accessible items under the current account.<br><br>* If you select any specific project, you can only select the VPC under that project.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you select any specific project, you can only select the VPC under that project.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Please ensure that the instance is created in the same region as the ECS instance that needs to be connected, otherwise they cannot be connected through the private network, and will not perform at their best. For detailed steps, refer to <a href="https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC">Creating VPC</a>.</div><br> |
   ||Primary availability zone subnet |In the primary availability zone, select a subnet that can be used by the private network.<br><br>A subnet is an IP address block within a VPC. The subnet allocates private IP addresses to cloud resources. For detailed steps, refer to [Creating subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |**Advanced configuration** |Affiliated project |Select the item to which the instance belongs, and depending on the item you selected in the upper left corner of the console, the following defaults will apply:<br><br><br>* If you select **All resources**, the newly created instance will be added to the **default** project by default, and other projects can also be selected according to business needs.<br><br>* If you select any specific project, the newly created instance will be added to that project by default. You can also select other projects based on business needs.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">After the instance is successfully created, the project to which the instance belongs cannot be changed. Please make a reasonable choice based on your business situation.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a virtual concept that includes a set of resources, users, and roles. A project allows you to view and manage a group of resources in a unified manner and control the permissions of users and roles to these resources. For more details, see <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-projects">Resource management</a>.</div><br> |
   ||Managing tags |Click **Add tag** and select an existing tag key and tag value from the drop\-down list or enter a new tag key and tag value based on your business needs. For tag key setting rules, see [Tag setting rules](https://docs.byteplus.com/en/docs/HBase/Tag_overview#.5qCH562-6K6-572u6KeE5YiZ).<br><br>A tag consists of a key\-value object that identifies cloud resources. It can help you classify cloud resources with the same characteristics (such as use, owner, or environment) for easy filtering and aggregation, so that you can easily manage the cloud resources. For more information, refer to [Tag management](https://docs.byteplus.com/en/docs/HBase/Tag_overview).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you use sub\-account management instances, you need to add a globally <code>TagFullAccess</code> permission policy for sub\-account, so that all existing tags under the main account can be viewed in the drop\-down list, otherwise the drop\-down list is empty. Whether a sub\-account has <code>TagFullAccess</code> does not affect adding new tags to the instance. Add permissions for sub\-accounts see <a href="https://docs.byteplus.com/en/docs/HBase/Using_HBase_with_sub-accounts">Using HBase with sub\-accounts</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can also bind tags to an instance after it is successfully created. See <a href="https://docs.byteplus.com/en/docs/HBase/Associating_or_adding_tag">Associating a tag</a>.</div><br> |
   ||Deletion protection |Select whether to enable instance **Deletion protection**. After instance deletion protection is enabled, the instance cannot be deleted, preventing instance deletion due to misoperation.<br><br>You can also enable instance deletion protection after the instance is successfully created. For more information about removal protection, see [Instance deletion protection](https://docs.byteplus.com/en/docs/HBase/Instance_deletion_protection#.5byA5ZCv5a6e5L6L5Yig6Zmk5L-d5oqk). |
   |**Billing information** |Billing method |HBase supports Pay\-as\-you\-go billing.<br><br>Pay\-as\-you\-go: If you plan to use instance for a short period of time, choose pay\-as\-you\-go (hourly rate). You can save money by releasing the instance when you no longer need it. |
   ||Purchase duration |When the billing type selects the subscription, you need to select the purchase duration. Support monthly purchase (can purchase 1~9 months) and yearly purchase (can purchase 1~3 years). |
   ||Automatic renewal |If the billing type is selected as subscription, you can check the box of **Auto\-renewal on expiration**, and the platform will automatically renew the subscription on a monthly basis before the expiration of the instance, so there is no need to renew the subscription manually. You can also modify the renewal configuration after successful creation. For details, see [Renewal management](https://docs.byteplus.com/en/docs/HBase/Renewal_management). |
   

6. Click **Confirm order**.

7. Complete the subsequent steps based on the billing type selected.

   * If Pay\-as\-you\-go is selected:

      On the **Confirm order** page, confirm the order details, read and check the terms, and click **Buy now**.

   * If Subscription is selected:

      1. on the **Confirm order** page, confirm the order details, read and check the terms, and click **Submit the order**.

      2. On the **Confirm order information** page, reconfirm the order information, and click **Next step**.

      3. On the **Submit payment information** page, confirm the payment details and select the payment method, click **Go to payment**.


<span id="dfmACbE9"></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeRegions](https://docs.byteplus.com/en/docs/HBase/DescribeRegions) |Call the DescribeRegions API to query the regional resource information available in HBase. |
|[DescribeZones](https://docs.byteplus.com/en/docs/HBase/DescribeZones) |Call the DescribeZones API to query HBase's available zone resource information in a specified region. |
|[CreateDBInstance](https://docs.byteplus.com/en/docs/HBase/CreateDBInstance) |Call the CreateDBInstance API to create an HBase instance. |
|[DescribeDBInstances](https://docs.byteplus.com/en/docs/HBase/DescribeDBInstances) |Call the DescribeDBInstances interface to query the HBase instance list. |
|[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/HBase/DescribeDBInstanceDetail) |Call the DescribeDBInstanceDetail interface to query detailed information about a specified instance. |

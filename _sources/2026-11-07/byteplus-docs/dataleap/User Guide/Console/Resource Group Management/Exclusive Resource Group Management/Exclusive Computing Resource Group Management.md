---
title: "Exclusive Computing Resource Group Management"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/exclusive_computing_resource_group"
---

DataLeap supports two types of resource groups: public resource groups and dedicated resource groups. Dedicated resource groups include dedicated data integration resource groups, dedicated computing resource groups, dedicated scheduling resource groups, and dedicated data service resource groups, which require purchase. Dedicated resource groups have the following features:


* Support flexible configuration such as scaling up, scaling down, and specification changes.

* After purchase, you will have exclusive usage rights for the resource group.

* Supports self\-allocation of project binding and task usage for each resource group.


Since DataLeap users share public resource groups, task execution cannot be guaranteed during peak times. For multiple tasks or high\-priority tasks, purchasing an **exclusive resource group** is recommended. This article explains how to select and use exclusive compute resource groups.

<span id="_1-费用说明"></span>
## Cost Explanation

Exclusive computing resource groups support annual and monthly subscription modes. For detailed cost information, please see [Billing information for exclusive resource groups](https://docs.byteplus.com/docs/dataleap/Billing_Instructions_for_Exclusive_Resource_Groups).

<span id="_2-适用场景"></span>
## Applicable Scenarios


* Suitable for tasks with strict requirements on execution and completion times, requiring strong guarantees and high time sensitivity.

* For stable online services with many daily scheduled tasks, annual or monthly subscriptions offer better cost\-effectiveness and savings.


<span id="_3-使用限制"></span>
## Usage Restrictions

Only the tenant primary account or a sub\-account with DataLeapFullAccess permission can purchase dedicated resource groups.

<span id="_4-购买独享资源组"></span>
## Purchase Dedicated Computing Resource Groups


1. Log in to the DataLeap console.

2. Select **Resource Groups \> Exclusive resource group \> Exclusive computing** to enter the exclusive computing resource groups page.

3. Click the **Create Resource Group** button to enter the create resource group page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9612bb7f77c42ba875d55f1a53782e0~tplv-goo7wpa0wc-image.image) </span>

4. Set resource group information, click the **Create now** button, then follow the page prompts to pay the fee and complete the purchase of the dedicated resource group.

   The related parameters for creating a dedicated computing resource group are explained in the following table. Parameters marked with \* before the name are required, while those without \* are optional.

   
   |Parameter |Description |
   |---|---|
   |**Basic information** ||
   |\*Resource group type |Type of resource group purchased. Select **Exclusive task computing** for Notebook, Python, Shell, and other task types. |
   |\*Region |Current DataLeap service region information, defaulting to the region selected when activating DataLeap service; this field is not editable.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you have enabled multiple regions, you can select the region closest to your business through the region dropdown in the top navigation bar of the page.</div><br> |
   |\*Availability zone |Refers to physically isolated regions within the same area with separate power and network, as follows:<br><br><br>* Asia Pacific (Johor) Region: Supports Asia Pacific (Johor) A, Asia Pacific (Johor) B<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Within the same private network, internal communication is available between availability zones.</div><br> |
   |\*Name |The name of the resource group. Set it yourself; once set, it cannot be changed.<br><br>The name must start and end with a letter or number, can include numbers, underscores (_), and lowercase letters a\-z, and be 3 to 50 characters long. |
   |Resource group remarks |Enter a description of the resource group to facilitate future management. |
   |**Payment information** ||
   |\*Billing type |year and month subscription. |
   |\*Billing cycle |You can choose a one\-time purchase cycle or select the **automatic renewal** option. The system renews monthly after the cycle expires. |
   |**Resource configuration** ||
   |\*Resource specification |exclusive task computing supports **4 vCPU 16 GiB, 8 vCPU 32 GiB**, **16 vCPU 64 GiB**, and **32 vCPU 128 GiB** with a total of 4 specifications.<br><br>For detailed billing of specifications, see [Billing information for exclusive resource groups](https://docs.byteplus.com/docs/dataleap/Billing_Instructions_for_Exclusive_Resource_Groups). |
   |\*Number of resources |Set the number of resource groups to purchase based on demand.<br><br>Different resource specifications have different purchase quantity limits, as follows:<br><br><br>* 4 vCPU 16 GiB specification: quantity limit is 1 to 250 units.<br><br>* 8 vCPU 32 GiB specification: quantity limit is 1 to 125 units.<br><br>* 16 vCPU 64 GiB specification: quantity limit is 1 to 62 units.<br><br>* 32 vCPU 128 GiB specification: quantity limit is 1 to 31 units.<br><br><br>For detailed billing of specifications, please refer to [Billing information for exclusive resource groups](https://docs.byteplus.com/docs/dataleap/Billing_Instructions_for_Exclusive_Resource_Groups). |
   |**Configuration information** ||
   |\*Private network |Select a data source or task that requires access to the private network where the resources are located. If the existing private network does not meet your requirements, go to the Console [Create a private network](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/vpc/create?). |
   |\*Subnet |Choose the corresponding optional subnet information under the VPC. If the existing subnets do not meet your requirements, go to the subnet Console to [Create a subnet](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/subnet/create). |
   |\*Security team |Select the security group information attached to the VPC. If the existing security groups do not meet your requirements, go to the security group Console to [Create security group](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/securitygroup/create?). |
   |**Advanced Configuration** ||
   |BytePlus project |BytePlus offers a resource management method allowing you to group cloud resources by different businesses or projects through BytePlus projects for management.<br><br>To modify the resource's project, go to [Project Management](https://console.byteplus.com/iam/resourcemanage/project).<br><br>By default, **default (default project)**  is selected; use the dropdown to choose other created BytePlus projects.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When creating project binding with resource groups, only resource groups within the same BytePlus engine project can be selected; resource groups from different BytePlus engine projects cannot communicate with each other.</div><br> |
   |BytePlus tags |It is a resource management method provided by BytePlus that lets you tag and classify cloud resource instances with labels for quick retrieval of instances with specific features.<br><br>Tags can be added via the **Add tag** button, up to 20 tags in total. Each BytePlus label consists of a tag key and tag value. Use the dropdown to select created tag keys and automatically fill in the corresponding tag values.<br><br>To create new BytePlus labels, please [go to Resource Management > Tag List](https://console.byteplus.com/resourcemanager/tag/list). |
   


<span id="_5-管理独享资源组"></span>
## Manage Dedicated Computing Resource Groups


1. Log in to the DataLeap Console.

2. Select **Resource Groups \> Exclusive resource group \> Exclusive computing** to enter the dedicated computing resource group page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47dede9ab57b4aa692cdb092899c3d9b~tplv-goo7wpa0wc-image.image) </span>

3. You can perform the following operations:

   * Search resource groups

      Set search criteria to view a list of resource groups that meet the conditions.

   * View resource group details

      1. Click the **Name** or the **Detail** button to enter the resource group details page.

      2. You can view the purchased resource group configuration, payment information, network configuration, etc., and perform the following actions:

         * Click the **order number** to view the order details for the purchased resource group.

         * Click the **Manual Renewal** button to enter the renewal page for the resource group. In the **Renewal Period** dropdown menu, select the desired duration. The page will display the total cost and expiration date. Click the **Renew Now** button to go to the payment page, then follow the instructions to complete the payment.

         * Click the **auto\-renewal** **toggle** button. After a second confirmation, you can enable the automatic renewal service.

            After auto\-renewal is enabled, the system will automatically charge the fee for the next cycle based on the current billing cycle (monthly) after the expiration date.

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21f0ea5671dc410a9f38dae3402a1ce0~tplv-goo7wpa0wc-image.image) </span>

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Only resource groups that are running or have failed to run support renewal.         </div>
         

   * View BytePlus project details

      Click the **BytePlus project** name to which a resource group belongs in the list to go to the project details page and view detailed information.

   * View running instances

      Click the **Running Instance** button in the **Actions** column for a resource group entry. In the pop\-up side window, you can view the list of task run instances bound to this resource group. You can also click an instance's **Instance ID**, **Task ID**, **Task Name**, or **Project** to navigate to the corresponding page and view detailed information.

      * Instance ID: Go to the **Instance Operations** page to view details of the instance.

      * Task ID: To view all instances of this task, go to the **Instance O&M** page.

      * Task name: Go to the **Task Development** page and view this task's configuration.

      * Project: View details of the project associated with the task.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The list of running instances only displays instances whose task <strong>running status</strong> is <strong>in progress</strong>.      </div>
      

   * Edit image configuration

      Click the  **... \> Modify image** button in the **Action** column of a resource group. After modifying the configuration in the pop\-up window, click the **Modify** button to save.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">One image repository can bind multiple resource groups.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Changing the network configuration or image settings may cause tasks using the computing resource group to fail; modify with caution.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If modified, create a Python/Shell test task to verify connectivity before use. For detailed instructions, see <a href="https://docs.byteplus.com/docs/dataleap/python">Python</a>.      </div>
      

      The table below describes the related parameters for editing image configuration.

      
      |Parameters |Description |
      |---|---|
      |Mirror address |The access address of the image repository in this resource group. You can use third\-party mirror addresses or the BytePlus mirror repository address.<br><br>If no suitable image repository address is available, click **Create** to jump to the image repository platform and create and manage repository instances. For related instructions, see [Create a standard edition instance](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance) and [push and pull images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images) |
      |User name |The username for creating an image repository instance.<br><br>You can view the username (**username**) on the respective repository instance page. |
      |Password |Login password for the image repository instance.<br><br>You can modify this password on the corresponding repository instance page.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Ensure the password is entered correctly to avoid task binding failures.</div><br> |
      

   * Change resource configuration

      1. Click the  **... \> Modify resource allocation** button in the **Action** column for a running resource group to open the change resource configuration side panel.

      2. After modifying resource specifications and quantity, click the **Modify** button.

      3. Complete the payment according to the page prompts.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The resizing operation theoretically combines <strong>unsubscribing from the old configuration</strong> and <strong>purchasing the new configuration</strong>, so one resizing operation corresponds to multiple resizing orders. The payable amount for a single resizing order is the theoretical amount calculated based on the upgrade or downgrade formula. It is only used for calculating the total payable amount and is not the actual payment. Your actual payment is based on the total payable amount. For specific billing methods for resizing, please refer to <a href="https://docs.byteplus.com/docs/dataleap/exclusive_computing_resource_group#_6-%E5%90%8E%E7%BB%AD%E6%93%8D%E4%BD%9C">Billing Examples</a>.      </div>
      

   * Delete resource group

      Click the **Delete** button in the **Actions** column for resource groups in the creation failed or released status. After secondary confirmation, the resource group can be deleted.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only the main account can manage created exclusive computing resource groups.</div>


<span id="_6-后续操作"></span>
## Billing Examples

The **Change Resource Configuration** operation theoretically combines **cancelling the old configuration** and **purchasing the new configuration**. Therefore, one change operation corresponds to multiple change orders. The payable amount of a single change order is a theoretical amount calculated based on the scale\-up or scale\-down formula. It is only used for payable summary calculations and does not represent the actual payment. Your actual payment is based on the total payable amount. The following gives examples of change billing.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The following examples are for reference only. The actual change is based on the total payable amount calculated by the platform.</div>


If the original dedicated computing resource group was purchased on May 22, 2024, with specifications of **4 vCPU 16 GiB** and a quantity of **1** resource group, the corresponding change billing is as follows:


* Scaling operation

   The scaling operation took place later on May 28, upgrading to **8 vCPU 32 GiB** with a quantity of **2** resource groups. Assuming the old configuration resource group has a remaining duration of 2,160,000 seconds (platform calculates remaining duration accurately to the second), the scaling\-up billing example is as follows:

   **Total amount payable for the upgrade order**

   = Cost of purchasing new configuration \- Cost of unsubscribing from old configuration

   = [Remaining purchase duration of new configuration resource group (2,160,000) / 3600 \* (2 new specification resource group monthly package price 1920 / 30 / 24)] \- [Remaining duration of old configuration resource group (2,160,000) / 3600 \* (resource group monthly package price 480 / 30 / 24)]

   = [2160000 / 3600 \* (1920 / 30 / 24)] \- [2160000 / 3600 \* (480 / 30 /24)]

   = 1,200 yuan

* Scaling down operation

   Two days later, on May 30, perform scaling down operation. After scaling down, the specification is **4 vCPU 16 GiB**, with **1** resource group instance. Assuming when submitting the scaling down order, the resource group has a remaining duration of 1,987,200 seconds (platform calculates remaining duration accurately to the second), the scaling down billing example is as follows:

   **Amount to be refunded for the scaling down order**

   =Old configuration remaining refundable value \- cost of purchasing new configuration

   =[Actual payment value of expansion order / remaining purchase duration \* remaining usable duration] \- [Current resource group remaining duration (1987200) / 3600 \* (new specification resource group monthly list price 480 / 30 / 24)]

   =[1600 / 2160000 \* 1987200] \- [1987200 /3600 \* (480 / 30 / 24)]

   =1472 \- 368

   =1104 RMB


<span id="c0af0f03"></span>
## Subsequent Operations

Dedicated computing resource groups in **running** status can be bound to corresponding projects for exclusive computing resources used in Notebook, Python, Shell, and other tasks.

For detailed instructions on binding resource groups to projects, see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project) and [Modify Project Configuration Information](https://docs.byteplus.com/docs/dataleap/modify_project).

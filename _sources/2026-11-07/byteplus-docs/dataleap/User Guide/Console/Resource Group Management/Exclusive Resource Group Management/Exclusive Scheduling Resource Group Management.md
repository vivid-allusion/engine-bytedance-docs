---
title: "Exclusive Scheduling Resource Group Management"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/exclusive_scheduling_resource_group"
---

DataLeap supports two types of resource groups: public resource groups and exclusive resource groups. Exclusive resource groups include exclusive data integration resource groups, exclusive computing resource groups, exclusive scheduling resource groups, and exclusive data service resource groups, which require purchase. Exclusive resource groups have the following features:


* Support flexible configurations such as expansion, scaling, and specification changes.

* After purchase, you will have exclusive use rights to the resource group.

* Support self\-assigning project binding and task usage for each resource group.


Since DataLeap users share public resource groups, tasks cannot guarantee timely completion during peak periods. Therefore, for a high number of tasks or tasks requiring high priority guarantees, purchasing an **exclusive resource group** is recommended. This article explains how to choose and use exclusive scheduling resource groups.

<span id="_1-费用说明"></span>
## Cost Explanation

Exclusive scheduling resource groups support yearly and monthly subscription modes. For detailed cost explanations, please refer to [Billing information for exclusive resource groups](https://docs.byteplus.com/docs/dataleap/Billing_Instructions_for_Exclusive_Resource_Groups).

<span id="_2-适用场景"></span>
## Applicable Scenarios


* Suitable for business scenarios sensitive to task execution and completion time, requiring strong guarantees and high timeliness.

* For stable online business with frequent daily scheduled tasks, yearly or monthly subscriptions offer better cost performance and savings.


<span id="_3-使用限制"></span>
## Usage Restrictions

Only tenant main accounts or sub\-accounts with the DataLeapFullAccess permission can purchase exclusive resource groups.

<span id="_4-购买独享资源组"></span>
## Purchase an Exclusive Scheduling Resource Group


1. Log in to the DataLeap console.

2. Select **Resource Groups \> Exclusive Resource Group \> Exclusive Scheduling** to enter the exclusive scheduling resource group page.

3. Click the **Create resource group** button to go to the create resource group page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77b9c0a87e524bb38f0a9bf012f60c0b~tplv-goo7wpa0wc-image.image) </span>

4. Set the resource group information, click the **Create now** button, and pay the fee as prompted to complete the purchase of the exclusive resource group.

   The table below describes the parameters related to creating an exclusive scheduling resource group. Parameters marked with \* before the name are required; those without \* are optional.

   
   |Parameters |Description |
   |---|---|
   |**Basic information** ||
   |\*Resource group type |The purchased resource group type. Select **exclusive task scheduling** to generate scheduling instances. |
   |\*Region |The current DataLeap service region is based on the region selected when activating the DataLeap service and is not editable.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If multiple regions are activated, you can choose the region closest to your business via the region dropdown menu in the top navigation bar.</div><br> |
   |\*Name |The name of the resource group, set by the user and cannot be changed once set.<br><br>The name must start and end with a number or letter, support numbers, underscore (_), lowercase letters a\-z, and be 3 to 50 characters long. |
   |Resource Group Remarks |Enter a description for the resource group to facilitate future management. |
   |**payment information** ||
   |\*Billing Type |Year and month subscription. |
   |\*billing cycle |You can choose a one\-time purchase period or select the **automatic renewal** option. The system will renew automatically on a monthly basis after each billing cycle expires. |
   |**Resource allocation** ||
   |\*Resource specification |Exclusive task scheduling supports 4 specifications: **4CU: 16 concurrency**, **8CU: 32 concurrency**, **16CU: 64 concurrency**, and **32CU: 128 concurrency**.<br><br>For detailed specification billing, please refer to [Billing information for exclusive resource groups](https://docs.byteplus.com/docs/dataleap/Billing_Instructions_for_Exclusive_Resource_Groups). |
   |\*Number of resources |Set the quantity of purchased resource groups as needed.<br><br>The purchase limits vary by resource specification, as follows:<br><br><br>* 4CU: 16 concurrency specification: quantity limit is 1~250 units.<br><br>* 8CU: 32 concurrency specification: quantity limit is 1~125 units.<br><br>* 16CU: 64 concurrency specification: quantity limit is 1~62 units.<br><br>* 32CU: 128 concurrent specification: quantity limit is 1~31 units.<br><br><br>For detailed billing of specifications, please refer to [Billing information for exclusive resource groups](https://docs.byteplus.com/docs/dataleap/Billing_Instructions_for_Exclusive_Resource_Groups). |
   |**Advanced Configuration** ||
   |BytePlus project |It is a resource management method provided by BytePlus. You can group and manage cloud resources used by different businesses or projects through BytePlus projects.<br><br>If you need to modify the project a resource belongs to, please go to [Project Management](https://console.byteplus.com/iam/resourcemanage/project).<br><br>By default, **default (default project)**  is selected. You can select other created BytePlus projects from the dropdown.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When creating project binding for a resource group, you can only select resource groups within the same BytePlus project; resource groups under different BytePlus projects are not interoperable.</div><br> |
   |BytePlus tags |It is a resource management method provided by BytePlus that lets you tag and classify cloud resource instances with labels for quick retrieval of instances with specific features.<br><br>Tags can be added via the **Add tag** button, up to 20 tags in total. Each BytePlus label consists of a tag key and tag value. Use the dropdown to select created tag keys and automatically fill in the corresponding tag values.<br><br>To create new BytePlus labels, please [go to Resource Management > Tag List](https://console.byteplus.com/resourcemanager/tag/list). |
   


<span id="_5-管理独享资源组"></span>
## Manage Exclusive Scheduling Resource Groups


1. Log in to the DataLeap console.

2. Select **Resource Groups \> Exclusive Resource Group \> Exclusive Scheduling** to enter the exclusive scheduling resource group page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/773c940704d641d0a98b1724df1fc80e~tplv-goo7wpa0wc-image.image) </span>

3. The following operations can be performed:

   * Search resource groups

      Set search criteria to view the list of resource groups that meet the conditions.

   * View resource group details

      1. Click the **Name** to enter the resource group details page.

      2. You can view purchased resource group configurations, payment information, network configuration information, and perform the following operations:

         * Click the **order number** to view the order information for the purchased resource group.

         * Click the **manual renewal** button to go to the renewal page for this resource group. In the **renewal cycle** dropdown list, select the desired purchase duration. The page will display the total billing price, expiration date, and other information. Click the **renew now** button to go to the payment page and complete the payment according to the instructions on the page.

         * Click the **automatic renewal** **on/off** button. After the secondary confirmation, you can enable the automatic renewal service for this resource group.

            After automatic renewal is enabled, the system automatically deducts the fee for the next cycle according to the current billing cycle (1 month/time) after the expiration date.

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21f0ea5671dc410a9f38dae3402a1ce0~tplv-goo7wpa0wc-image.image) </span>

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Only resource groups that are running or have failed to run support renewal operations.         </div>
         

   * View BytePlus project details

      Click the **BytePlus project** name corresponding to a resource group in the list to open that project's detail page and view its information.

   * View running instances

      Click the **Running Instance** button in the **Actions** column for a resource group entry. In the pop\-up side window, you can view the list of task run instances bound to this resource group. You can also click an instance's **Instance ID**, **Task ID**, **Task Name**, or **Project** to navigate to the corresponding page and view detailed information.

      * Instance ID: Go to the **Instance Operations** page to view details of the instance.

      * Task ID: To view all instances of this task, go to the **Instance O&M** page.

      * Task name: Go to the **Task Development** page and view this task's configuration.

      * Project: View details of the project associated with the task.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The list of running instances only displays instances whose task <strong>running status</strong> is <strong>in progress</strong>.      </div>
      

   * Change resource allocation

      1. Click the  **... \> Modify resource allocation** button in the **Action** column of a running resource group to open the change resource allocation side panel.

      2. Modify resource specifications, quantity, and other details as needed, then click the **Modify** button.

      3. Complete the payment process as prompted on the page.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The upgrade operation theoretically combines <strong>unsubscribing old configuration</strong> and <strong>purchasing new configuration</strong>, so one upgrade operation corresponds to multiple upgrade orders. The payable amount for a single upgrade order is a theoretical amount calculated based on the upgrade or downgrade formula. It is used only for payable summary calculation and does not represent the actual payment. Your actual payment is based on the payable summary amount. For detailed explanation of the upgrade billing method, please see <a href="https://docs.byteplus.com/docs/dataleap/exclusive_scheduling_resource_group#b6345c33">Billing Example</a>.      </div>
      

   * Delete resource group

      Click the  **... \> Delete** button in the **Action** column of a resource group with a failed or released status. After confirming again, you can delete the resource group.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only the main account can manage created exclusive scheduling resource groups.</div>


<span id="b6345c33"></span>
## Billing Example

The **change resource allocation** operation theoretically combines **unsubscribing from old configurations** and **purchasing new configurations**, so one change operation corresponds to multiple change orders. The payable amount for a single upgrade or downgrade order is the theoretical amount calculated by the upgrade or downgrade formula. It is only used for calculating the payable summary and does not represent the actual payment amount. Your actual payment amount is based on the payable summary amount. The following provides examples to illustrate upgrade billing.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The following examples are for reference only. The actual payable amount calculated by the platform shall prevail for any changes.</div>


If the original exclusive scheduling resource group purchase date is May 22, 2024, with a specification of **4CU: 16 concurrency** and **1** resource group, the corresponding upgrade billing cases are as follows:


* expansion operation

   On May 28, an expansion operation was performed, upgrading the specification to **8CU: 32 concurrency** with **2** resource groups. Assuming the old configuration resource group has a remaining duration of 2,160,000 seconds (remaining duration is calculated precisely to the second by the platform), the expansion billing example is as follows:

   **upgrade order total payable amount**

   = cost of purchasing new configuration \- cost of unsubscribing old configuration

   = [remaining purchase duration of new configuration resource group (2,160,000) / 3600 × (monthly package price for 2 new specification resource groups 1920 / 30 / 24)] \- [remaining duration of old configuration resource group (2,160,000) / 3600 × (monthly package price for resource group 480 / 30 / 24)]

   = [2160000 / 3600 \* (1920 / 30 / 24)] \- [2160000 / 3600 \* (480 / 30 /24)]

   = 1200 yuan

* scaling operation

   two days later, on May 30, perform the scaling operation; after scaling, the specification is **4CU: 16 concurrency**, with **1** resource group unit. assuming that at the time of submitting the scaling order, the resource group has 1,987,200 seconds of remaining duration (the platform calculates remaining duration accurate to the second), the scaling billing example is as follows:

   **amount to be refunded for the scaling order**

   = remaining refundable value of the old configuration \- cost of purchasing the new configuration

   = [actual payment value of the expansion order / remaining purchase duration \* remaining usable duration] \- [current resource group's remaining duration (1,987,200) / 3600 \* (monthly price of the new specification resource group 480 / 30 / 24)]

   =[1600 / 2160000 \* 1987200] \- [1987200 /3600 \* (480 / 30 / 24)]

   =1472 \- 368

   = 1104 yuan


<span id="_6-后续操作"></span>
## Subsequent Operations

Exclusive scheduling resource groups in **running** status can be bound to the corresponding project to generate scheduling instances.

For detailed instructions on binding resource groups to projects, see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project) and [Modify Project Configuration Information](https://docs.byteplus.com/docs/dataleap/modify_project).

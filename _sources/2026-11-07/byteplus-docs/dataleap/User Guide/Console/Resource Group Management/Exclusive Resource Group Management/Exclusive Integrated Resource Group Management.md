---
title: "Exclusive Integrated Resource Group Management"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/exclusive_integrated_resource_group"
---

DataLeap supports two main types of resource groups: public resource groups and exclusive resource groups. The exclusive resource groups include exclusive data integration resource groups, exclusive computing resource groups, exclusive scheduling resource groups, and exclusive data service resource groups, which require purchase for use. The exclusive resource group has the following features:


* Supports flexible configurations such as expansion, scaling down, and specification changes.

* Purchasing grants independent usage rights for the resource group.

* Supports self\-allocation of project bindings and task usage for each resource group.


Since DataLeap users share public resource groups, task execution during peak periods cannot be guaranteed timely. Therefore, for heavy or high\-priority assured tasks, purchasing an **exclusive resource group** is recommended. This article introduces how to select and use an exclusive integrated resource group.

<span id="_1-费用说明"></span>
## Cost Explanation

The exclusive integrated resource group supports annual and monthly subscription plans. For detailed cost information, refer to [Billing information for exclusive resource groups](https://docs.byteplus.com/docs/dataleap/Billing_Instructions_for_Exclusive_Resource_Groups).

<span id="_2-适用场景"></span>
## Applicable Scenarios


* Suitable for tasks with strict requirements on execution and completion times, requiring strong assurance and high timeliness.

* Online business is relatively stable. When daily scheduling tasks are numerous, annual or monthly subscriptions offer better cost\-effectiveness and value.


<span id="_3-使用限制"></span>
## Usage Restrictions

Only tenant main accounts or sub\-accounts with DataLeapFullAccess permission can purchase exclusive integrated resource groups.

<span id="_4-购买独享资源组"></span>
## Purchase Exclusive Integrated Resource Groups


1. Log in to the DataLeap console.

2. Select **Resource Groups \> Exclusive Resource Group \> Exclusive Integrated** to enter the exclusive integrated resource group page.

3. Click the **Create Resource Group** button to open the resource group creation page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb07d76a6bb340c3a1953fb0fe7b1ec5~tplv-goo7wpa0wc-image.image) </span>

4. Set the resource group information, then click the **Create now** button and follow the prompts to complete the payment for purchasing the exclusive integrated resource group.

   The table below explains the parameters related to creating an exclusive integrated resource group. Parameters marked with \* are required; those without \* are optional.

   
   |Parameters |Description |
   |---|---|
   |**Basic Information** ||
   |\*Resource group type |Type of purchased resource group. Select **exclusive data transmission service** for data synchronization tasks. |
   |\*Resource group subtype |Only the **Exclusive integration resource group** option is supported. This resource group is used for stream and batch job processing. |
   |\*Region |The region information of the current DataLeap service, defaulted to the region selected when activating the DataLeap service. This field is not editable.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you have activated multiple regions, select the region closest to your business via the region dropdown in the top navigation bar.</div><br> |
   |\*Availability zone |Refers to a physical area isolated in power and network within the same region.<br><br><br>* Asia Pacific (Johor) Region: Supports Asia Pacific (Johor) A, Asia Pacific (Johor) B<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Internal network communication is available between availability zones within the same private network.</div><br> |
   |\*Name |The name of the resource group is customizable and cannot be changed once set.<br><br>The name must start and end with a number or letter, may include numbers, underscore _, lowercase letters a\-z, and must be 3 to 50 characters in length. |
   |Resource Group Remarks |Enter resource group description to facilitate subsequent use and management. |
   |**Payment information** ||
   |\*Billing type |Billing type used for this resource group, supporting year and month subscription. |
   |\*Billing cycle |You can choose a one\-time purchase cycle or enable the **automatic renewal** button. The system automatically renews monthly after one billing cycle expires. |
   |**Resource configuration** ||
   |\*Resource specification |Resource specification supports only **1 vCPU 4 GiB**.<br><br>For detailed billing of specifications, please refer to [Billing information for exclusive resource groups](https://docs.byteplus.com/docs/dataleap/Billing_Instructions_for_Exclusive_Resource_Groups). |
   |\*Number of resources |Set the number of purchased resource groups as needed.<br><br>Exclusive Data Integration quantity limits are 4 to 1500 units; input value must be a multiple of 4.<br><br>For detailed billing of specifications, please refer to [Billing information for exclusive resource groups](https://docs.byteplus.com/docs/dataleap/Billing_Instructions_for_Exclusive_Resource_Groups). |
   |**Configuration information** ||
   |TOS bucket |Stores the runtime status of data integration jobs. There are two settings:<br><br><br>* First registration: The tenant has no TOS bucket yet; you can select an existing TOS bucket from the dropdown.<br><br>* Non\-first registration: The TOS bucket selected during the first registration is the default and cannot be edited.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">All Data Integration Resource Groups must use the same TOS bucket. Newly created resource groups can only select the TOS bucket bound to the first resource group, ensuring jobs can recover from state after switching resource groups.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you have not activated Object Storage TOS or created a TOS bucket, please go to <strong>TOS</strong> to create one.</div><br> |
   |\*Private network |Select the private network that the data source or task needs to access resources. If the existing private network does not meet your requirements, go to the console [create a private network](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/vpc/create?). |
   |\*Subnet |Select the available subnet information under the VPC; up to 3 subnets can be selected. If existing subnets do not meet your requirements, go to the subnet console to [create a subnet](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/subnet/create). |
   |\*Security group |Select the security group information mounted under the VPC. If existing security groups do not meet your requirements, go to the security group console to [create security group](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/securitygroup/create?). |
   |**Advanced Configuration** ||
   |BytePlus Project |BytePlus provides a resource management method allowing you to group cloud resources used by different businesses or projects under BytePlus projects.<br><br>To change the resource’s project, go to [project management](https://console.byteplus.com/iam/resourcemanage/project).<br><br>The **default (default project)**  is selected by default; use the dropdown to choose other created BytePlus projects.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When creating a project binding for a resource group, you can only select resource groups within the same BytePlus project. Resource groups under different BytePlus projects are not interoperable.</div><br> |
   |BytePlus tags |It is a resource management method provided by BytePlus that lets you tag and classify cloud resource instances with labels for quick retrieval of instances with specific features.<br><br>Tags can be added via the **Add tag** button, up to 20 tags in total. Each BytePlus label consists of a tag key and tag value. Use the dropdown to select created tag keys and automatically fill in the corresponding tag values.<br><br>To create new BytePlus labels, please [go to Resource Management > Tag List](https://console.byteplus.com/resourcemanager/tag/list). |
   


<span id="_5-管理独享资源组"></span>
## Manage Exclusive Integrated Resource Groups


1. Log in to the DataLeap console.

2. Select **Resource Groups \> Exclusive Resource Group \> Exclusive Integrated** to access the exclusive integrated resource group page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d59606592e174dcfbba2054bfe12dafc~tplv-goo7wpa0wc-image.image) </span>

3. You can perform the following management actions:

   * Search resource groups

      Set search criteria to view the list of matching resource groups.

   * View resource group details

      1. Click the resource group **Name** or the **Detail** button in the **Action** column to enter the resource group details page.

      2. You can view purchased resource group configurations, payment information, network configuration, and perform the following actions:

         * Click the **Order number** in the **Payment information** section to view the order number details for the purchased resource group.

         * Click the **Config** tab's **TOS bucket, Private network, Subnet, Security team** info button to view detailed information.

         * Click the **Manual renewal** button to enter the renewal page for the resource group. Select the desired duration from the **Renewal cycle** dropdown; the page will show the total cost and expiration date. Then click the **Renew now** button to proceed to payment and follow the instructions to complete payment.

         * Click the **Automatic renewal** **on/off** button and confirm to enable automatic renewal for this service.

            After enabling automatic renewal, the system will automatically deduct the fee for the next cycle based on the current billing cycle (1 month/time) after the expiration date.

            <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="4">tip            </div>
            

            <div data-tips="true" data-tips-type="tip" data-wrapper-indent="4">Only resource groups in the <strong>running</strong> state support renewal actions.            </div>
            

   * View BytePlus project details

      Click the **BytePlus project** name associated with a resource group in the list to jump to the project's detail page and view its information.

   * Run instance

      Click the **Running instance** button in the **Action** column of a resource group entry to open a side panel where you can filter and view the list of task run instances bound to this resource group and dynamically view the total resources of the selected tasks on the current page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b0b764e255f47a0a4bbd745d884805d~tplv-goo7wpa0wc-image.image) </span>

   * Edit

      Click the  **... \> Edit** button in the **Action** column of a resource group entry, to open a side panel where you can manage **resource group name**, **remarks**, **automatic renewal**, and **add or remove subnets**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Permissions at the DataLeapSailReadOnlyAccess level or higher can modify resource group names and remarks; modifying subnets requires DataLeapSailFullAccess permission.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Previously created and saved subnet information cannot be deleted.      </div>
      

   * project binding

      Click the  **...**   **\> Project binding** button in the **Action** column of a resource group entry, to open a side panel to view the tenant’s existing project list and bind or unbind projects as needed.

   * resource utilization rate

      Click the  **...**   **\> Resource utilization rate** button in the **Action** column of a resource group entry, to open a side panel to view the CPU and Memory utilization rates of the resource group over different time periods.

   * expansion

      Click the  **...**   **\> Expansion** button in the **Action** column of a resource group entry, to open a side panel; after increasing the resource quantity, click the **Expand now** button to pay and perform expansion.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When paying for expansion, the difference will be calculated based on the original expiration date.      </div>
      

   * scaling

      Click the  **...**   **\> Scaling** button in the **Action** column of a resource group entry, to reduce the number of resources in the side panel, then click **immediate scaling** to perform the refund scaling operation.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The scaling operation will reduce the resource capacity. If you have a task that uses more resources than the scaled resource capacity, the scaling will cause the task to fail to be submitted. Please operate with caution.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The refund for scaling down is calculated based on the original expiration date.      </div>
      

   * unsubscribe

      1. Click the  **...**   **\> Unsubscribe** button in the **Action** column for a running resource group. The system checks the resource group's dependencies. If no task is running, a confirmation dialog for unsubscribing appears.

      2. Click the **Confirm** button to enter the unsubscribe page. After verification, submit the application to complete the process.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After unsubscribing, the resource will be released and cannot be restored.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the resource group is linked to active tasks, you must stop the tasks as prompted by the system before unsubscribing.      </div>
      

   * renewal fee

      Click the  **...**   **\> Renewal** button in the **Action** column for a resource group to manually renew the resource group as needed.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only <strong>running</strong> resource groups support renewal.      </div>
      

   * Delete Resource Group

      Click the  **...**   **\> Delete** button in the **Action** column for resource groups in failed creation, released, or unsubscribed status. After confirmation, you can delete the resource group.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The main account can manage exclusive integrated resource groups created by everyone, while sub\-accounts can only manage the resource groups they created.</div>


<span id="_6-后续操作"></span>
## Subsequent Operations

Resource groups in **Running** status can bind to corresponding projects. These groups provide resources needed for synchronize task runs and enable data transfer between data sources.

For detailed instructions on project binding resource groups, see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project) and [Modify Project Configuration Information](https://docs.byteplus.com/docs/dataleap/modify_project).

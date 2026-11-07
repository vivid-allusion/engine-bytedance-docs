---
title: "Manage cost allocation"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/manage-cost-allocation"
---

ByteHouse CDW (Cloud Data Warehouse) supports binding a project or tag to a virtual warehouse, a private server, or storage resources. After configuration, you can use the cost analysis feature in the BytePlus Cost Center to view detailed costs for different projects or tags, enabling accurate management of cloud resource costs.

The configuration steps for project and tag are consistent across the three types of resources: virtual warehouse, private server, and storage resources. This tutorial uses "adding project and tag to a virtual warehouse" as an example to illustrate the process. The configuration for private servers and storage resources can follow the same procedure.

<span id="aa70df3d"></span>
# Function overview

Cost allocation refers to the process by which an enterprise divides the costs of cloud computing resources or storage resources among various business departments or project groups based on projuects or tags, quickly organizes the cloud cost structure, establishes cost relationships within complex organizational structures, and facilitates cloud cost management. BytePlus provides a tag\-based cost allocation feature that enables enterprises to manage cloud cost sharing. You can view the cost details for specified tag values at the end of consumption.

The concepts explained in this document are as follows:


* **Project**: Project management is a resource management method provided by BytePlus, which allows you to group and manage cloud resources used by different businesses or projects. To modify the project to which a resource belongs, please go to [Project Management](https://console.volcengine.com/iam/resourcemanage/project).

* **Tag**: A resource tag consists of a set of key\-value pairs. You can use resource tags to classify and aggregate cloud resources based on different dimensions, and they are also used in scenarios including tag\-based authorization and tag\-based billing. For more information, see the [help document](https://docs.byteplus.com/en/docs/resourcemanagement/Tag_Overview).


<span id="dbc52431"></span>
# Limitations


* **Annual/monthly subscription** (**pre\-paid**): Both existing resources and new resources now support split billing by project or tag.

* **Pay\-as\-you\-go** (**post\-paid**):

   * The cost allocation feature for newly added resources is a Beta feature. To use it, submit a ticket or contact the ByteHouse team to obtain allowlist permission.

   * Existing resources do not support this feature yet. To use, you can choose from the following two methods:

      * You can switch the payment mode to an annual or monthly prepaid plan. For instructions, see [Billing mode switch](https://docs.byteplus.com/docs/bytehouse/virtual-warehouse-specification-change#b2bde1ae).

      * You may also delete existing resources and recreate them after obtaining allowlist permission.


<span id="3d5d3dca"></span>
# Bind projects and tags

<span id="14553b94"></span>
## Bind projects


1. (Optional) If you have not yet created a project, please create a new project first.

   1. Log in to the [BytePlus Access Control Platform](https://console.byteplus.com/iam/resourcemanage/project), go to the **Project Management** page, and click **New project**.

   2. Fill in the project name and description, then click **Apply**.

2. Log in to the ByteHouse CDW Console. Click **Tenant management** at the top, and click **Basic information**. In the virtual warehouse module, click the **project edit** button in the row of the target virtual warehouse to enter the edit page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9cf6288d26d41c287de94af258364e4~tplv-goo7wpa0wc-image.image) </span>

3. In the project dropdown list, select the target project. ByteHouse CDW supports automatically reading projects in the BytePlus Console, allowing users to select and bind the required projects.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae11fcad1e634c4dafc4b2d92145ffe6~tplv-goo7wpa0wc-image.image) </span>

4. Click **Apply**.


<span id="c1de9b5b"></span>
## Bind tags

<span id="fd6e6d23"></span>
### Step 1: Create a tag


1. Log in to the ByteHouse CDW Console, click **Tenant management** at the top, click **Basic information**, in the virtual warehouse module, click the **edit tag** button in the row of the target virtual warehouse to enter the editing page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e126150ff63a43eab677185f29b305c3~tplv-goo7wpa0wc-image.image) </span>

2. Click **Add Tags**. You can configure the tag keys and values according to the actual business revenue sharing plan. Click **Confirm**. The tag key\-value pair will be automatically synchronized to the BytePlus Resource Management Console.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e36072f08b464ca480a81f7c090835c6~tplv-goo7wpa0wc-image.image) </span>


<span id="321fc6b0"></span>
### Step 2: Enable the cost tag

Log in to the [BytePlus Cost Center](https://console.volcengine.com/finance/bill/tag), click **Cost Tag** under **Bill Management**, click the **Enable** button in the Actions column, and after confirming, the cost tag will be enabled. After enabling the tag, the Platform will add the tag within 4 hours after the bill is generated. Therefore, please wait 4 hours after adding before using the tag to view bill details.

<span id="92b6a310"></span>
# View bill details

After binding resources to a project or tag in ByteHouse CDW, during the **post\-billing period following the end of the billing cycle**, you can use the BytePlus Cost Center to access functions such as split billing, cost billing, billing analysis, and more. By filtering by project or tag, you can accurately view detailed billing information for the corresponding dimension. This section uses the cost billing feature as an example to demonstrate how to view allocation information by project or flight tag.

**How to use**:


1. Log in to the [BytePlus Cost Center](https://console.volcengine.com/finance/bill/cost-analyse), and click **Cost Bill** under **Bill Management** to enter the bill details page.

2. Select project or tag as a filter to view the corresponding revenue sharing information.

3. (Optional) Download fee breakdown.

   1. Click the **Download** button, set the export content, allocation month, accounting period, and other information, then click **Apply**. The system will automatically jump to the export record page and export the expense list according to the filter criteria you set. Due to the large file size, the download is expected to take about 3 minutes. Please wait patiently.

   2. On the **Export Record** page, click the **Refresh** button to view the export status of the expense details in the file list. When the status is **Downloadable**, click **Click here** to download the current expense list.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Because exported files may be too large, and to ensure an efficient and secure experience for you, exported files will be automatically deleted after 3 days.   </div>
   

<span id="b45ca067"></span>
# Unbind projects and tags

To stop using the revenue sharing feature, you may unbind projects and flight tags as needed.

<span id="7e8486f8"></span>
## Unbind projects


1. To unbind a project that is bound to a virtual warehouse, you need to use the virtual warehouse ID. Please record it in advance.

   Log in to the ByteHouse CDW Console, click **Virtual warehouse** at the top, and in the virtual warehouse list, view and record the virtual warehouse ID.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbfc9f19cc1d4fed9cbb18f5291db0b8~tplv-goo7wpa0wc-image.image) </span>

2. In the ByteHouse CDW Console, click the top **Tenant management**, click **Basic information**, in the virtual warehouse module, click the **project name** in the row of the target virtual warehouse, and navigate to the **Project management** page of the **BytePlus** **Access Console**.

3. Search for and click the target project name in the project list.

4. In the resource name column, locate the virtual warehouse ID that needs to be unbound, select the resource, and click **Resource Transfer Out**.

5. Click **Apply** to unbind projects bound to the virtual warehouse.


<span id="d9e0a665"></span>
## Unbind tags


1. Log in to the ByteHouse CDW Console, click the top **Tenant management**, click **Basic information**, in the virtual warehouse module, click the **Edit tag** button in the row of the target virtual warehouse to enter the edit page.

2. Click the **Delete** button to the right of the target tag to delete the tag bound to the virtual warehouse.

3. Click **Apply**.

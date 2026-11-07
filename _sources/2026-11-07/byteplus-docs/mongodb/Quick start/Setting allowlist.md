---
title: "Setting allowlist"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/set-allowlist"
---

After the Document Database for MongoDB instance is created successfully, you can set allowlist for the instance to allow devices to access the instance. This topic describes how to set allowlist via the console.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

To ensure the security and stability of the MongoDB database, accessing MongoDB instances from any IP address is not allowed by default in the system. Before using MongoDB instances, you need to create an allowlist and add the client's IP address or CIDR block to the allowlist of the MongoDB instance to allow the client to access the MongoDB instance. We recommend that you regularly maintain and manage the allowlist to ensure the security of accessing MongoDB instances.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Each BytePlus account can create up to 500 allowlists per region.

* Each BytePlus account can allow up to one default allowlist per region. A newly created default allowlist will automatically override the existing default allowlist, i.e. the existing default allowlist will automatically become a non\-default allowlist.

* Each allowlist can be associated with up to 1,000 IP addresses or IP address segments in CIDR format.

* Each allowlist can be associated with up to 500 instances.

* Each allowlist can be associated with a maximum of 200 instances in batches each time.

* Each instance can be associated with a maximum of 100 allowlists, but the total number of IP addresses or IP address segments in CIDR format across all allowlists associated with each instance must not exceed 1000.

* Each allowlist can be associated with a maximum of 100 allowlists in batches each time.

* If an instance is not associated with any allowlist, it means all addresses are forbidden from accessing it.


<span id=".5a6e5L6L5Yib5bu65pe257uR5a6a55m95ZCN5Y2V"></span>
## Associate allowlist during instance creation

You can associate MongoDB instances with allowlists during instance creation, so that clients in the allowlist can access the instance. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance).

<span id=".5a6e5L6L5Yib5bu65ZCO57uR5a6a55m95ZCN5Y2V"></span>
## Associate allowlist to existing instance


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Security** tab.

6. Under the **Allowlist** sub\-tab, click **Associate allowlist**.

7. In the pop\-up control panel, first confirm the **Instance name** and **Project** information, then complete the subsequent operations based on the selected association mode.

   * If you select **Existing allowlist**, that is, associate an existing allowlist to the current instance, you need to:

      1. In the **Existing allowlist** list, select the allowlists to be associated.

      2. click **OK**.

   * If you select **New allowlist**, that is, create a new allowlist and automatically associate it to the current instance, you need to:

      1. Select the project to be added to the allowlist from the **Affiliated project** drop\-down list. By default, the **default** project will be added.

      2. Enter a new allowlist name, description (optional), and IP address.

      3. click **OK**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For more information on configuring the name, description, and IP address when creating an allowlist, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/create-allowlist">Creating allowlist</a>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you use the MongoDB cloud service through IAM user, you can only see the allowlist information under the projects that have been authorized for the current IAM user. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/using_mongodb_services_with_subusers">Using MongoDB with IAM users</a>.      </div>
      


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[CreateAllowList](https://docs.byteplus.com/en/docs/mongodb/createallowlist) |Call the CreateAllowList API to create a new IP allowlist. |
|[ModifyAllowList](https://docs.byteplus.com/en/docs/mongodb/modifyallowlist) |Call the ModifyAllowList API to modify the target allowlist settings (such as the name of the allowlist, IP address in the allow list, whether to set it as the default allowlist, etc.). |
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) |Call the DescribeAllowLists API to query all IP allowlists for the account in the specified region. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/mongodb/describeallowlistdetail) |Call the DescribeAllowListDetail API to query the details of the target allowlist group, including the IP addresses and the details of associated instances. |
|[AssociateAllowList](https://docs.byteplus.com/en/docs/mongodb/associateallowlist) |Call AssociateAllowList API to associate the target instance to the specified IP allowlist. |

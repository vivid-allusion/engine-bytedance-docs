---
title: "Configuring an allowlist"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Configuring_an_Allowlist"
---

After creating a Table Storage for HBase instance, you can set an allowlist for the instance to allow devices to access it. This article describes how to associate instances to allowlists using the console.

<span id="jz6KRZVR"></span>
## Limitation


* Each BytePlus account can create a maximum of 100 allowlists in each region. To create an allowlist, see [Creating an allowlist](https://docs.byteplus.com/en/docs/HBase/Creating_an_allowlist).

* Each allowlist can contain a maximum of 300 IP addresses or IP address segments.

* Each allowlist can be associated with up to 200 instances. You can associate up to 50 instances in a single batch.

* Each instance can be associated with up to 100 allowlists. You can associate up to 100 allowlists in a single batch.

* If an instance is not associated with any allowlist, access from all addresses is denied.


<span id="9TVsxTtZ"></span>
## Procedure

You can choose any of the following methods to associate an instance with an allowlist:

<span id="O1WldJ7Q"></span>
### Method 1: Associate the instance to the allowlist


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. Click **Allowlists** in the left\-side navigation bar.

4. On the **Allowlists** page, click **Associate instance** in the allowlist **Actions** column.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click on the target allowlist name, and in the pop\-up control panel, in the <strong>List of associated instances</strong> area, click <strong>Associate instance</strong>.   </div>
   

5. In the pop\-up control panel, select the target instance to be associated.

6. Click **OK**.


<span id="7RKHkswr"></span>
### Method 2: Associate the allowlist to the instance


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click the **Security** tab.

5. On the **Security** tab, click **Associate instance**.

6. In the pop\-up control panel, complete the subsequent operations based on the selected binding mode.

   * If you select an **Existing allowlist** (associate an existing allowlist with the current instance), you need to:

      1. In the **Existing allowlist** list, select the allowlist you want to associate with.

      2. Click **OK**.

   * If you select **New allowlist** (create a new allowlist and associate it with the current instance), you need to:

      1. Enter a new allowlist name, description (optional), and IP addresses.

      2. Click **OK**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For more information about configuring the name, description, and IP address when creating an allowlist, see <a href="https://docs.byteplus.com/en/docs/HBase/Creating_an_allowlist">Creating an allowlist</a>.      </div>
      

<span id="oHXCDtDB"></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/HBase/DescribeAllowLists) |Call the DescribeAllowLists API to query all IP allowlists in a specified region for the current account. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/HBase/DescribeAllowListDetail) |Call the DescribeAllowListDetail API to view the details of a specified allowlist, including its IP addresses and associate instances. |
|[AssociateAllowList](https://docs.byteplus.com/en/docs/HBase/AssociateAllowList) |Call the AssociateAllowList interface to associate the target instance with the specified allowlist. |

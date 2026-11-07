---
title: "Editing allowlist"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/edit-allowlist"
---

After creating a MongoDB instance, you need to set allowlists for the instance to allow access to the instance from external devices. This topic describes how to edit the allowlist, including modifying the allowlist name, IP address, and whether or not to set it as the default allowlist.

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


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/region:db+cn-beijing/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. In the left navigation bar, choose **NoSQL Database \> MongoDB \> Allowlists**.

4. On the **Allowlist** page, locate the target allowlist and perform the corresponding actions as needed.

   
   |Operation type |Procedure |
   |---|---|
   |Modify allowlist name |1. Hover over the target allowlist name and click <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_d9dfb828e5bfd2e2f537fff88cdd83c6.jpg) </span> icon next to the name.<br><br>2. Enter a new name in the pop\-up dialog box.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The name must meet the following requirements:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It cannot start with a number or hyphen (\-).   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The length should be 1 to 128 characters.   </div><br>   <br><br>3. click **OK**. |
   |Modify allowlist IP address |1. Click the name of the target allowlist.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also find the target allowlist on the <strong>Security</strong> tab of the MongoDB instance. The specific method is as follows:   </div><br>   <br><br>   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Log in to the <a href="https://console.byteplus.com/db/mongodb">MongoDB console</a>.   </div><br>   <br><br>   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the upper\-left corner of the top menu bar, select the project and region for instance.   </div><br>   <br><br>   3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Select either <strong>Replica set instances</strong> or <strong>Sharding instances</strong> in the left navigation bar depending on the instance type.   </div><br>   <br><br>   4. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">On the target instance type list page, click the target instance name.   </div><br>   <br><br>   5. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">On the instance details page, click the <strong>Security</strong> tab.   </div><br>   <br><br>   6. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the allowlist under the <strong>Allowlist</strong> sub\-tab, find and click the name of the target allowlist.   </div><br>   <br><br>2. In the pop\-up panel, click **Edit** next to **Allowlist information**.<br><br>3. In the **IP address** dialog box of **Modify allowlist information** panel, enter an IP address or an address segment in CIDR format.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Duplicate addresses are not allowed. Separate multiple addresses with commas (,).   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Setting <code>0.0.0.0/0</code> allows access from all addresses.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Setting <code>127.0.0.1</code> blocks access from all addresses.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Setting both <code>0.0.0.0/0</code> and <code>127.0.0.1</code> allows access from all addresses.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Setting CIDR <code>192.168.1.0/24</code> allows access from IP addresses within that network segment.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Setting <code>192.168.1.1</code> allows access from this IP address only.   </div><br>   <br><br>4. click **OK**.<br><br>5. In the pop\-up dialog box, click **OK**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This modification will be applied to all instances associated with this allowlist.   </div><br>    |
   |Set default aAllowlist |1. Click the name of the target allowlist.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also find the target allowlist on the <strong>Security</strong> tab of the MongoDB instance. The specific method is as follows:   </div><br>   <br><br>   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Log in to the <a href="https://console.byteplus.com/db/mongodb">MongoDB console</a>.   </div><br>   <br><br>   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the upper\-left corner of the top menu bar, select the project and region for instance.   </div><br>   <br><br>   3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Select either <strong>Replica set instances</strong> or <strong>Sharding instances</strong> in the left navigation bar depending on the instance type.   </div><br>   <br><br>   4. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">On the target instance type list page, click the target instance name.   </div><br>   <br><br>   5. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">On the instance details page, click the <strong>Security</strong> tab.   </div><br>   <br><br>   6. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the allowlist under the <strong>Allowlist</strong> sub\-tab, find and click the name of the target allowlist.   </div><br>   <br><br>2. In the pop\-up panel, click **Edit** next to **Allowlist information**.<br><br>3. In the **Default allowlist** area of the **Modify allowlist information** panel, select whether to set the current allowlist as the default allowlist according to business needs.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If set as the default allowlist, it is automatically selected when creating new instances.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Each BytePlus account can allow up to one default allowlist per region. A newly created default allowlist will automatically override the existing default allowlist. That is, the existing default allowlist will automatically become a non\-default allowlist. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/product-limit">Constraints and limits</a>.   </div><br>   <br><br>4. click **OK**. |
   |Associating instances and allowlists |For spcific procedure, refer to [Associating instances to allowlists](https://docs.byteplus.com/en/docs/mongodb/associate-allowlist). |
   |Disassociating instances from allowlists |For spcific procedure, refer to [Disassociating instances from allowlists](https://docs.byteplus.com/en/docs/mongodb/disassociate-allowlist). |
   |Deleting allowlist |For spcific procedure, refer to [Deleting allowlist](https://docs.byteplus.com/en/docs/mongodb/delete-allowlist). |
   


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) |Call the DescribeAllowLists API to query all IP allowlists for the account in the specified region. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/mongodb/describeallowlistdetail) |Call the DescribeAllowListDetail API to query the details of a target allowlist, including IP addresses and details of associated instance. |
|[ModifyAllowList](https://docs.byteplus.com/en/docs/mongodb/modifyallowlist) |Call the ModifyAllowList API to modify the target allowlist settings (such as the name of the allowlist, IP address in the allow list, whether to set it as the default allowlist, etc.). |
|[AssociateAllowList](https://docs.byteplus.com/en/docs/mongodb/associateallowlist) |Call AssociateAllowList API to associate the target instance to the specified IP allowlist. |
|[DisassociateAllowList](https://docs.byteplus.com/en/docs/mongodb/disassociateallowlist) |Call the DisassociateAllowList API to disassociate the target MongoDB instance from the specified IP allowlist. |
|[DeleteAllowList](https://docs.byteplus.com/en/docs/mongodb/deleteallowlist) |Call the DeleteAllowList API to delete the target allowlist. |

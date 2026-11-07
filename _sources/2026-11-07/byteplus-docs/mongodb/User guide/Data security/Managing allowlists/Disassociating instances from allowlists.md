---
title: "Disassociating instances from allowlists"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/disassociate-allowlist"
---

If you do not allow devices in an allowlist to access an instance, you can disassociate the allowlist from the instance. This topic describes how to disassociate instances and allowlists through the console.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

After an instance is disassociated from an allowlist, none of the devices in that allowlist can access the instance. Ensure that the IP addresses of devices that still require access to the current instance are added to other allowlists first. For more information about how to set IP allowlists, refer to [Editing allowlist](https://docs.byteplus.com/en/docs/mongodb/edit-allowlist).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5pa55rOV5LiA77ya5bCG5b2T5YmN5a6e5L6L5LuO55m95ZCN5Y2V6Kej57uR"></span>
### Disassociate instance from allowlist


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. In the left navigation bar, choose **NoSQL Database \> MongoDB \> Allowlists**.

4. You can choose any of the following methods to disassociate the instances from a specified allowlist.

   
   <Tabs>
   <Tab zoneid="yyOmX7Za1d" title="Disassociation method 1">
   <TabTitle>Disassociation method 1</TabTitle>
   
   1. On the **Allowlists** page, click  **...**   **\>**  **Disassociate instance** in the Actions column on the right side of the target allowlist.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can first select the project to which the allowlist belongs from the Affiliated project drop\-down list above the allowlist list. Then, in the search box on the right, quickly filter out the target allowlist by allowlist name, ID, description, or IP address.   </div>
      
   
   2. In the pop\-up panel, find the instances that need to be disassociated from the instance list, and click **Disassociate instance** in the **Actions** column on the right side.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To disassociate multiple instances, select the instances to be disassociated from the list, and then click <strong>Disassociate instance</strong> in the lower\-left corner of the list.   </div>
      
   
   3. In the pop\-up dialog box, click **OK**.
   
   
   </Tab>
   <Tab zoneid="ORyEifsAPq" title="Disassociation method 2">
   <TabTitle>Disassociation method 2</TabTitle>
   
   1. On the **Allowlists** page, click the name of the target allowlist.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can first select the project to which the allowlist belongs from the Affiliated project drop\-down list above the allowlist list. Then, in the search box on the right, quickly filter out the target allowlist by allowlist name, ID, description, or IP address.   </div>
      
   
   2. In the **List of associated instances** area of the pop\-up panel, click **Disassociate instance**.
   
   3. In the pop\-up panel, find the instances that need to be disassociated from the instance list, and click **Disassociate instance** in the **Actions** column on the right side.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To disassociate multiple instances, select the instances to be disassociated from the list, and then click <strong>Disassociate instance</strong> in the lower\-left corner of the list.   </div>
      
   
   4. click **OK**.
   
   
   </Tab>
   </Tabs>
   


<span id=".5pa55rOV5LqM77ya5bCG55m95ZCN5Y2V5LuO5b2T5YmN5a6e5L6L6Kej57uR"></span>
### Disassociate allowlist from instance


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Security** tab.

6. In the allowlist list under the **Allowlist** sub\-tab, locate the target allowlist and click **Disassociate allowlist** in the **Actions** column.

7. In the pop\-up dialog box, click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) |Call the DescribeAllowLists API to query all IP allowlists for the account in the specified region. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/mongodb/describeallowlistdetail) |Call the DescribeAllowListDetail API to query the details of the target allowlist group, including the IP addresses and the details of associated instances. |
|[DisassociateAllowList](https://docs.byteplus.com/en/docs/mongodb/disassociateallowlist) |Call the DisassociateAllowList API to disassociate the target MongoDB instance from the specified IP allowlist. |

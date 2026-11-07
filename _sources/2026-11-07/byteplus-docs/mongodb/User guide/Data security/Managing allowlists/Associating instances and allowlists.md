---
title: "Associating instances and allowlists"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/associate-allowlist"
---

After creating a MongoDB instance, you need to set allowlists for the instance to allow access to the instance from external devices. This topic describes how to associate instances and allowlists through the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

Allowlist has been created. For more information about how to create allowlists, refer to [Creating allowlist](https://docs.byteplus.com/en/docs/mongodb/create-allowlist).

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

<span id="bpC1mZXs"></span>
### Associate instances to current allowlist


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. In the left navigation bar, choose **NoSQL Database \> MongoDB \> Allowlists.** 

4. You can choose any of the following methods to associate instances with a specified allowlist.

   
   <Tabs>
   <Tab zoneid="OiUchdDLdm" title="Association mode 1">
   <TabTitle>Association mode 1</TabTitle>
   
   1. On the **Allowlists** page, click **Associate instance** in the **Actions** column on the right side of the target allowlist.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can first select the project to which the allowlist belongs from the Affiliated project drop\-down list above the allowlist list. Then, in the search box on the right, quickly filter out the target allowlist by allowlist name, ID, description, or IP address.   </div>
      
   
   2. In the pop\-up panel, check the instances that need to be added to the current allowlist.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can first select the project to which the instance belongs from the <strong>Affiliated project</strong> drop\-down list above the instance list, and then quickly filter out the target instance by instance name or ID in the search box on the right.   </div>
      
   
   3. click **OK**.
   
   
   </Tab>
   <Tab zoneid="FGu1fpa66Y" title="Association mode 2">
   <TabTitle>Association mode 2</TabTitle>
   
   1. On the **Allowlists** page, click the name of the target allowlist.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can first select the project to which the allowlist belongs from the Affiliated project drop\-down list above the allowlist list. Then, in the search box on the right, quickly filter out the target allowlist by allowlist name, ID, description, or IP address.   </div>
      
   
   2. In the pop\-up panel, in the **List of associated instances** area, click **Associate instance**.
   
   3. In the pop\-up panel, check the instances that need to be added to the current allowlist.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can first select the project to which the instance belongs from the <strong>Affiliated project</strong> drop\-down list above the instance list, and then quickly filter out the target instance by instance name or ID in the search box on the right.   </div>
      
   
   4. click **OK**.
   
   
   </Tab>
   </Tabs>
   


<span id="YUgkiPHx"></span>
### Associated allowlist to current instance


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Security** tab.

6. Under the **Allowlist** sub\-tab, click **Associate allowlist**.

7. In the pop\-up control panel, first confirm the Instance name and Project information, then complete the subsequent operations based on the selected association mode.

   
   <Tabs>
   <Tab zoneid="b45iFA4A0z" title="Association method: Existing allowlist">
   <TabTitle>Association method: Existing allowlist</TabTitle>
   
   1. In the **Existing allowlist** list, select the allowlists to be associated.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can first select the project to which the allowlist belongs from the <strong>Affiliated project</strong> drop\-down list above the allowlist list. Then, in the search box on the right, quickly filter out the target allowlist by allowlist name, ID, description, or IP address.   </div>
      
   
   2. click **OK**.
   
   
   </Tab>
   <Tab zoneid="MTxmxBIJRw" title="Association method: New allowlist">
   <TabTitle>Association method: New allowlist</TabTitle>
   
   1. Select the project to be added to the allowlist from the **Affiliated project** drop\-down list. By default, the **default** project will be added.
   
   2. Enter a new allowlist name, description (optional), and IP address.
   
   3. click **OK**.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For more information on configuring the name, description, and IP address when creating an allowlist, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/create-allowlist">Creating allowlist</a>.   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you use the MongoDB cloud service through IAM user, you can only see the allowlist information under the projects that have been authorized for the current IAM user. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/using_mongodb_services_with_subusers">Using MongoDB with IAM users</a>.   </div>
      
   
   
   </Tab>
   </Tabs>
   


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) |Call the DescribeAllowLists API to query all IP allowlists for the account in the specified region. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/mongodb/describeallowlistdetail) |Call the DescribeAllowListDetail API to query the details of the target allowlist group, including the IP addresses and the details of associated instances. |
|[AssociateAllowList](https://docs.byteplus.com/en/docs/mongodb/associateallowlist) |Call AssociateAllowList API to associate the target instance to the specified IP allowlist. |

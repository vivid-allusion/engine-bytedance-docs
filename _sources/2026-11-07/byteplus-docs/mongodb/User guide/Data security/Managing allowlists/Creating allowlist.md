---
title: "Creating allowlist"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/create-allowlist"
---

After the Document Database for MongoDB instance is created successfully, you can set allowlist for the instance to allow devices to access the instance. This topic describes how to create allowlist via the console.

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


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. In the left navigation bar, choose **NoSQL Database \> MongoDB \> Allowlists**.

4. On the **Allowlists** page, click **Create allowlist**.

5. In the **Create allowlist** panel, set the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Project |Select the project to be added to the allowlist from the drop\-down list. By default, the **default** project will be added.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you use the MongoDB cloud service through IAM user, you can only see the allowlist information under the projects that have been authorized for the current IAM user. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/using_mongodb_services_with_subusers">Using MongoDB with IAM users</a>.</div><br> |
   |Allowlist name |Enter the name of the allowlist, which must meet all the following requirements:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 1 to 128 characters. |
   |Description |Enter remarks on the allowlist, which must not exceed 200 characters. |
   |IP address |Enter IP addresses or IP address segments in CIDR format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Each allowlist can contain up to 1000 IP addresses or IP address segments in CIDR format.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Duplicate addresses are not allowed. Separate multiple addresses with commas (,).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set to <code>0.0.0.0/0</code> to allow access from all addresses.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Setting <code>127.0.0.1</code> blocks access from all addresses.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Setting both <code>0.0.0.0/0</code> and <code>127.0.0.1</code> allows access from all addresses.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Setting <code>192.168.1.0/24</code> allows access from IP addresses within that network segment.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Setting <code>192.168.1.1</code> allows access from only this IP address.</div><br> |
   |Default allowlist |Select whether to set the new creation allowlist to the default allowlist. If set as the default allowlist, it is automatically selected when creating new instances.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Each BytePlus account can allow up to one default allowlist per region. A newly created default allowlist will automatically override the existing default allowlist. That is, the existing default allowlist will automatically become a non\-default allowlist. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/product-limit">Constraints and limits</a>.</div><br> |
   

6. click **OK**.


<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent operations

After creating allowlists, you can associate the allowlist with target instances. For more information on how to associate allowlists, refer to [Associating instances and allowlists](https://docs.byteplus.com/en/docs/mongodb/associate-allowlist).

<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[CreateAllowList](https://docs.byteplus.com/en/docs/mongodb/createallowlist) |Call the CreateAllowList API to create a new IP allowlist. |
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) |Call the DescribeAllowLists API to query all IP allowlists for the account in the specified region. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/mongodb/describeallowlistdetail) |Call the DescribeAllowListDetail API to query the details of the target allowlist group, including the IP addresses and the details of associated instances. |

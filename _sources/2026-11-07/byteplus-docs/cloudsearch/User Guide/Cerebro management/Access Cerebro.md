---
title: "Access Cerebro"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Access_Cerebro"
---

You can use Cerebro to visually manage Elasticsearch and OpenSearch instances and monitor cluster load, node resources, index distribution, and other information. This article explains how to access Cerebro.

<span id="hUvOOC7e"></span>
## Prerequisites


* Cerebro created. For specific operations, see [Create Cerebro](https://docs.byteplus.com/en/docs/cloudsearch/Create_Cerebro).

* If you want to access Cerebro via a public address, you need to turn on Cerebro's public network access first. For specific operations, see [View Cerebro details](https://docs.byteplus.com/en/docs/cloudsearch/View_Cerebro_details).

* The default port for the Cerebro access address is 9000. You need to open this port in the security group. For the procedure to add a security group, refer to [Adding a security group](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).


<span id="4oVBhcLp"></span>
## Procedure


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. Select **Cerebro** in the left navigation bar, then click the link after **Public network access address** or **Private network access address**.

4. Enter Username and Password on the Cerebro login page, then click **Login**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The username is <code>admin</code>, and the password is the one you set when creating the instance. If you forget your login password, you can reset it on the <strong>Cerebro</strong> page. For details, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/View_Cerebro_details">View Cerebro details</a>.   </div>

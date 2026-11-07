---
title: "Enabling or disabling public network resolution"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/set-public-network-resolution"
---

Document Database for MongoDB supports resolving private domain addresses to private IP addresses in a public network environment. This topic describes the procedure for enabling and disabling public network resolution.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

After a Document Database for MongoDB instance is successfully created, a private network connection address is provided by default for you to access the instance. When accessing MongoDB instance using private network address, private domains must be resolved. By default, private domains can only be successfully resolved to private IP addresses within the BytePlus private network environment. However, in certain non\-production scenarios (such as directly connecting to Document Database for MongoDB instances in a test environment, or personal devices accessing private domains), it may be necessary to resolve private domains via a public network. In such cases, you can enable the public network resolution feature for instance. Once enabled, private domains can be successfully resolved to private IP addresses, even in a public network environment.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

Only the private network addresses of the following instances or nodes support public network resolution:


* Private network addresses of replica set instances.

* Private network address of Mongos node in sharding cluster instance


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Due to the complex public network environment, the accuracy and timeliness of domain name resolution cannot be guaranteed, so this function is limited to non\-production environments. For production environments, it is strongly recommended to use a DNS Forward solution by configuring your local DNS server to forward to BytePlus DNS, where `100.96.0.2` and `100.96.0.3` are the DNS servers used by BytePlus, to achieve domain name resolution in a private network environment.

* For sharding cluster instances, if you add Mongos nodes after public network resolution is enabled, you must first disable and then re\-enable the public network resolution feature after the instance configuration changes are complete. Otherwise, the private network address domain name corresponding to the newly added Mongos node will not be resolved as a private network.


<span id=".5byA5ZCv5YWs572R6Kej5p6Q"></span>
## Enable public network resolution


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click on the **Connectivity** tab.

6. On the **Connectivity** tab, perform corresponding operations based on the node type of the private network address.

   * Private network addresses of replica set instances

      In the **Private network access** section, click **Enable public network resolution** next to **Public network resolution**.

   * Private network address of Mongos node in sharding cluster instance

      In the **Connect to Mongos** section, click **Enable public network resolution** next to **Public network resolution**.

7. In the pop\-up dialog box, confirm the private network domain name that requires public network resolution, and click **OK**.


<span id=".5YWz6Zet5YWs572R6Kej5p6Q"></span>
## Disable public network resolution


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click on the **Connectivity** tab.

6. On the **Connectivity** tab, perform corresponding operations based on the node type of the private network address.

   * Private network addresses of replica set instances

      In the **Private network access** section, click **Disable public network resolution** next to **Public network resolution**.

   * Private network address of Mongos node in sharding cluster instance

      In the **Connect to Mongos** section, click **Disable public network resolution** next to **Public network resolution**.

7. In the pop\-up dialog box, click **OK**.


<span id="05pXNAP0"></span>
## Relevant APIs


|API |Description |
|---|---|
|[ModifyDBEndpointPrivateDNSVisibility](https://docs.byteplus.com/en/docs/mongodb/modifydbendpointprivatednsvisibility) |Call the ModifyDBEndpointPrivateDNSVisibility API to enable or disable public network resolution function for target MongoDB instance. |

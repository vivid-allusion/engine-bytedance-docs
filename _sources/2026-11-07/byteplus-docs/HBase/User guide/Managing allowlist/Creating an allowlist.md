---
title: "Creating an allowlist"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Creating_an_allowlist"
---

After creating a Table Storage for HBase instance, you can set an allowlist for the instance to allow devices to access it. This article describes how to create an allowlist from the console.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

To ensure the security and stability of your HBase database, the system blocks all IP addresses from accessing HBase instances by default. Before using an HBase instance, you must create an allowlist and add the client's IP address or IP address range to it to allow the client to access the HBase instance. We recommend that you regularly maintain and manage the allowlist to enhance the access secu

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before setting up an allowlist, you need to obtain the client IP address.


|Access method |IP address acquisition method |
|---|---|
|BytePlus ECS private network access |In ECS, run the `ifconfig` command to view network card information. |
|Public access from a local client |Choose the appropriate method based on your operating system:<br><br><br>* Linux OS: Run the `curl ipinfo.io \| grep ip` command to obtain the public IP address.<br><br>* Windows OS: Access the [query network](https://www.ip138.com/) on the local client to obtain the public IP address. |


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Precautions


* Each BytePlus account can create a maximum of 100 allowlists in each region. Each allowlist can contain a maximum of 300 IP addresses or IP address segments.

* Each allowlist can be associated with up to 200 instances. You can associate up to 50 instances in a single batch.

* Each instance can be associated with up to 100 allowlists. You can associate up to 100 allowlists in a single batch.

* If an instance is not associated with any allowlist, access from all addresses is denied. For instructions on how to associate allowlists, see [Associating allowlist and instance](https://docs.byteplus.com/en/docs/HBase/Associating_allowlist_and_instance).

* Each BytePlus account can set one default allowlist per region. Setting a new default allowlist automatically replaces the previous one. The previous default allowlist becomes a regular allowlist.

* When using a Table Storage for HBase instance, ensure that the ECS network security configuration allows access from the IP addresses and port numbers specified for HBase. The port numbers for each component are as follows:

   
   |**Component** |**Port** |**Example** |**Description** |
   |---|---|---|---|
   |Zookeeper |2181 |2181 |Zookeeper connection port. |
   |Master |3000、3001 |3000、3001 |Master and master\-backup each occupy a port. |
   |RegionServer |5000~5\*\*\* |5000、5001、5002、5003 ...<br><br> |Each RegionServer node occupies a separate port, as follows:<br><br><br>* RegionServer\-0 : 5000<br><br>* RegionServer\-1 : 5001<br><br>* RegionServer\-2 : 5002<br><br><br>The port number increases sequentially for additional RegionServer nodes. |
   |MetaProxy |7000、7001<br><br> |7000、7001 |Private network access: 7000.<br><br>Public network access: 7001. |
   |ThriftServer |9090 |9090 |A Thrift access address must be enabled. For details, see [Enabling high-availability Thrift connection address](https://docs.byteplus.com/en/docs/HBase/Enabling_or_disabling_high-availability_Thrift_connection_address). |
   |DFSProxy |8020 |8020 |You must apply for an underlying file system address. For details, see [Underlying file access guide](https://docs.byteplus.com/en/docs/HBase/Underlying_file_access_guide).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Underlying file access is an invitation\-only beta feature. To use it, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to apply for technical support.</div><br> |
   


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the top menu bar, select the project and region for the instance.

3. Click **Allowlists** in the left\-side navigation bar.

4. On the **Allowlists** page, click **Create allowlist**.

5. In the **Create allowlist** control panel, set the following configuration.

   
   |Name |Description |
   |---|---|
   |Allowlist settings |Enter the allowlist name, which must also meet the following requirements:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length is 1~32 characters. |
   |Description |Enter the comment information for the allowlist, and the length should not exceed 200 characters. |
   |IP address |Enter an IP address or an IP address range in CIDR format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Each allowlist supports a maximum of 300 IP addresses or IP address segments in CIDR format.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Duplicate addresses are not allowed. Separate multiple addresses with commas (,).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set <code>127.0.0.1</code> to disable all address access.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Setting CIDR <code>192.168.1.0/24</code> means that IP addresses within this network segment are allowed to access.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set to <code>192.168.1.1</code> to allow access from this IP address only.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Disable settings <code>0.0.0.0/0</code>.</div><br> |
   |Default allowlist |Select whether to set as the default allowlist. Each BytePlus account can set one default allowlist per region. After an allowlist is set as the default, it will be pinned to the top when you associate an instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Setting a new default allowlist automatically replaces the previous one. The previous default allowlist becomes a regular allowlist.</div><br> |
   

6. Click **OK**.


<span id=".5ZCO57ut5q2l6aqk"></span>
## Next steps

After creating an Allowlist, you can associate it to the target instance. For instructions on how to associate allowlists, see [Associating allowlist and instance](https://docs.byteplus.com/en/docs/HBase/Associating_allowlist_and_instance).

<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[CreateAllowList](https://docs.byteplus.com/en/docs/HBase/CreateAllowList) |Call the CreateAllowList interface to create a new allowlist. |

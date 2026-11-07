---
title: "Modifying an allowlist"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Modifying_an_allowlist"
---

After creating a Table Storage for HBase instance, you can set an allowlist for the instance to allow devices to access it. This article describes how to edit an allowlist, including modifying names and IP addresses.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instances associated to the target allowlist must be in the **Running** state. For more information about instance statuses, see [Instance status description](https://docs.byteplus.com/en/docs/HBase/Instance_status_description).

* Before setting up an allowlist, you need to obtain the client IP address.

   
   |Access method |IP address acquisition method |
   |---|---|
   |BytePlus ECS private network access |In ECS, run the `ifconfig` command to view network card information. |
   |Public access from a local client |Choose the appropriate method based on your operating system:<br><br><br>* Linux OS: Run the `curl ipinfo.io \| grep ip` command to obtain the public IP address.<br><br>* Windows OS: Access the [query network](https://www.ip138.com/) on the local client to obtain the public IP address. |
   


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitation


* Each BytePlus account can create a maximum of 100 allowlists in each region. To create an allowlist, see [Creating an allowlist](https://docs.byteplus.com/en/docs/HBase/Creating_an_allowlist).

* Each allowlist can contain a maximum of 300 IP addresses or IP address segments.

* Each allowlist can be associated with up to 200 instances. You can associate up to 50 instances in a single batch.

* Each instance can be associated with up to 100 allowlists. You can associate up to 100 allowlists in a single batch.

* If an instance is not associated with any allowlist, access from all addresses is denied. For instructions on how to associate allowlists, see [Associating allowlist and instance](https://docs.byteplus.com/en/docs/HBase/Associating_allowlist_and_instance).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. Click **Allowlists** in the left\-side navigation bar.

4. On the **Allowlists** page, click **Edit** in the allowlist actions column.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Alternatively, you can click the name of the target allowlist. In the panel that appears, click <strong>Edit</strong> next to <strong>Allowlist information</strong>.   </div>
   

5. In the **Modify allowlist information** control panel, set the following configuration.

   
   |Parameter |Description |
   |---|---|
   |Allowlist name |Enter the allowlist name, which must also meet the following requirements:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length is 1~32 characters. |
   |Description |Enter the comment information for the allowlist, and the length should not exceed 200 characters. |
   |IP address |Enter an IP address or an IP address range in CIDR format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Each allowlist supports a maximum of 300 IP addresses or IP address segments in CIDR format.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Duplicate addresses are not allowed. Separate multiple addresses with commas (,).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set <code>127.0.0.1</code> to disable all address access.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Setting CIDR <code>192.168.1.0/24</code> means that IP addresses within this network segment are allowed to access.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set to <code>192.168.1.1</code> to allow access from this IP address only.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Disable settings <code>0.0.0.0/0</code>.</div><br> |
   |Default allowlist |Choose whether to set it as the default allowlist. Each BytePlus account can set up one default allowlist per region. Once set as the default allowlist, it will be displayed at the top when associating an instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Setting a new default allowlist automatically replaces the previous one. The previous default allowlist becomes a regular allowlist.</div><br> |
   

6. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyAllowList](https://docs.byteplus.com/en/docs/HBase/ModifyAllowList) |Call the ModifyAllowList API to modify a specified allowlist, such as its name and associated IP addresses. |

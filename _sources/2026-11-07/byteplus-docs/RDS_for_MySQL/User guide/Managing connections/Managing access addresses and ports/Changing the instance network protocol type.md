---
title: "Changing the instance network protocol type"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Changing_the_instance_network_protocol_type"
---

RDS for MySQL supports modifying the network protocol type of an instance. This topic describes the steps.

<span id="wy43AJhK"></span>
## Prerequisites

An instance has been created, and its state is **Running**.

<span id="31UOR93z"></span>
## Precautions


* You cannot modify the network configuration of an instance that is connected using PrivateLink.

* Modifying the network protocol type does not change the private network or public service area domain names, but the IP addresses for the private network and public service area will change. Ensure that your services connect using the domain name.

* The switch operation is irreversible. It only supports switching from IPv4 to an IPv4+IPv6 dual stack, and the change cannot be rolled back.

* To perform the switch, the instance must use a virtual private cloud that has IPv6 enabled.

* The modification process will cause a transient disconnection lasting for minutes. Perform the operation during off\-peak hours.

* Check the database allowlists in advance to ensure that the new client address is included for a normal connection.

* This switch only applies to the virtual private cloud. The public network does not support IPv4+IPv6 dual\-stack.

* Changing the network protocol type of the instance will affect services that are accessing the database through the existing addresses. Exercise caution.


<span id="RLNnP8R0"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the Instances page, click the target instance name.

4. On the **Summary** tab, click the edit icon to the right of **Network protocol type**.

5. In the **Confirm conversion to dual\-stack (IPv4+IPv6 protocol)?**  dialog box that appears In the dialog box, confirm the affected connection address, read and select the risk warning, and then click **OK**.

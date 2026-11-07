---
title: "Modifying an instance's private network and subnet"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_instance_network_configuration"
---

RDS for MySQL supports modifying the network configuration of an instance, such as changing the Virtual Private Cloud and subnet. This topic describes the steps to modify the instance network configuration.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance has been created, and its state is **Running**.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You cannot modify the network configuration of an instance that is connected using PrivateLink.

* Modifying the network configuration may cause one to two brief service interruptions. Proceed with caution. It is recommended that you add a reconnection mechanism to the application, which can greatly reduce the impact of database disconnection on the business. Confirm the following risks before the operation:

   * Confirm the following risks before executing the operation: Modifying the VPC and subnet does not change the private domain name, but the private IP address will change.

   * Modifying the VPC and subnet can temporarily affect the use of ecosystem database products such as Database Transmission Service (DTS) and Database Workbench (DBW).

   * Promptly clear the client cache, or else read/write exceptions may occur.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.</div>



3. On the Instances page, click the target instance name.

4. On the **Summary** tab, click the edit icon after **Virtual Private Cloud/Subnet**.

5. In the pop\-up **Modify network information** dialog box, complete the following settings and then click **OK**.

   1. Confirm the domain name involved in the network configuration modification.

   2. Select a new Virtual Private Cloud and Subnet.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only Virtual Private Clouds and Subnets under the project specified in the top navigation bar can be selected.      </div>
      

   3. Read the data risks involved in modifying network configuration and check the box for the risk prompt.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After clicking <strong>OK</strong>, the instance status changes to<strong> Network changing</strong>. After the execution of the network configuration of the instance to be modified, the instance state changes to <strong>Running</strong>.</div>

---
title: "Modifying VPC and subnet"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_VPC_and_subnet"
---

NDB for MySQL support modifying the network information of an instance, such as the Virtual private cloud and subnet, after the instance is created. This article describes how to modify the network information of an instance.

<span id="iv3hc1Zd"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

<span id="fF9C2Jdy"></span>
## Precautions


* This feature is in gray\-scale release. If you need to use it, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support to apply for usage.

* Modifying the network configuration may cause one to two brief service interruptions. Proceed with caution. It is recommended that you add a reconnection mechanism to the application, which can greatly reduce the impact of database connection flashes on the business. Confirm the following risks before the operation:

   * Confirm the following risks before executing the operation: Modifying the VPC and subnet does not change the private domain name, but the private IP address will change.

   * Modifying private networks and subnets will temporarily affect the use of database ecosystem products such as DTS and DBW.

   * Promptly clear the client cache, or else read/write exceptions may occur.

   * After modifying the virtual private cloud and subnet, the associated IP addresses will be changed. The old IP resources will be released after 3 minutes. Once released, they may be occupied by other systems and cannot be selected again.


<span id="0TNUVE8t"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the instance name of the target instance to enter the **Summary** page.

4. In the **Basic information** section, click the edit icon to the right of **Virtual private cloud/Subnet**.

5. In the **Edit network information** dialog box, complete the following settings.

   
   |**Name** |**Description** |
   |---|---|
   |Affiliate project |Select the affiliated project for the virtual private cloud. |
   |Virtual private cloud |Select a new virtual private cloud. For details about virtual private clouds, refer to [Creating VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can only select a virtual private cloud that belongs to the specified affiliated project.</div><br> |
   |Subnet |Select a new subnet in the primary availability zone.<br><br>A subnet is an IP address block within a VPC. All cloud resources in the VPC must be deployed within a subnet. The subnet allocates private IP addresses to cloud resources. For detailed steps, refer to [Creating subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   

6. Read about the data risks of changing the network information, check the risk prompt, and then click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After clicking <strong>OK</strong>, the instance status changes to <strong>Network changing</strong>. After the network information of the instance is modified, its state changes to <strong>Running</strong>.   </div>

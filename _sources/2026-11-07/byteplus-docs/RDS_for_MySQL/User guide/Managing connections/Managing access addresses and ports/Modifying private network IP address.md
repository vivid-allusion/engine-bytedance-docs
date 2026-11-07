---
title: "Modifying private network IP address"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Modifying_private_network_IP_address"
---

Each RDS for MySQL connection endpoint provides a private network domain and a private network IP address for connecting to an instance. You can modify the private network IP address. This topic describes how to modify the private network IP address of a connection endpoint.

<span id="bsJV3vgg"></span>
## Prerequisites


* An instance has been created, and its state is **Running**. For more details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).


<span id="HaeBS1bN"></span>
## Precautions


* The private network IP of a connection endpoint cannot be modified if the instance uses PrivateLink for connection.

* Modifying the private network IP address impacts services that access the database through this address. Perform this operation with caution.

* Only the private network IP address of the connection endpoint can be modified.

* The target private network IP address must be a valid and unused IPv4 address, and it must be within the CIDR block of the subnet that the instance is using.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Each subnet has three system\-reserved IPs: the first, the second, and the last one. For example, for the subnet 192.168.2.0/24, the system\-reserved addresses are 192.168.2.0, 192.168.2.1, and 192.168.2.255.   </div>
   

<span id="pqjXYPeG"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

      3. Click **Instances** in the left\-side navigation bar.

3. Click the name of the target instance on the **Instances** page to go to the **Summary** page.

4. At the top of the page, click **Connectivity** to go to the **Connectivity** tab.

5. On the **Connectivity** tab, in the **Endpoints** list, click **Edit** in the **Actions** column for the target connection endpoint to go to the **Modify endpoint** page.

6. In the **Connection information** area of the **Modify endpoint** page, click Edit to the right of the Private network IP address.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3e04a235a7898f53e5b6dd8439920617.png)<sub> </sub></span>In the **Modify network information** window that appears, enter a new private network IP address. After reading and selecting the risk warning, click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After clicking <strong>OK</strong>, the instance status changes to <strong>Network changing</strong>. After the modification is complete, the instance state changes to <strong>Running</strong>.   </div>

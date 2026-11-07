---
title: "StarRocks UI usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/StarRocks_UI_usage"
---

<span id="ui链接"></span>
## UI link

On the StarRocks cluster page, the "Access Link" provides the address of the FE UI, which is only bound to the address of the master\-1\-1 node.

If a StarRocks cluster is deployed with multiple FE nodes, the service link will still only contain the address of the master\-1\-1 node.

In the above case, since master\-1\-1 is not bound to an elastic public IP, the access link is grayed out and unavailable. To use it, bind a public IP to master\-1\-1.

After binding, the access link turns blue and displays the public IP address.

<span id="安全组放开"></span>
## Open the security group

Port 8030 may not be open in the security group of the master\-1\-1 node, so you need to open the security group to allow public network access to this address.

<span id="67f50adb"></span>
### **procedure**


1. Click **Access Link** in the upper right corner, then **Configure Service Port**.

2. On the pop\-up page, click **Query Local IP** to obtain the local address on the Internet via the network, such as the 10.xx.xx.xx address in this example.

3. Enter the **CIDR Source Address**, and pay attention to the number of mask bits. For full IP access, enter /32 as shown in the example.

4. After selecting **Port Range**, the entered rule will be added to the **Access Rule**. Finally, click Confirm to activate the security group.

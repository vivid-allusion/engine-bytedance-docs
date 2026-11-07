---
title: "Modifying address prefix and port"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_address_prefix_and_port"
---

NDB for MySQL provides private and public network addresses to access instances. This article describes how to modify the prefix and port of the connection address.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only the private network connection address prefix can be modified, and the public network connection address prefix cannot be modified.

* After the new address takes effect, the old address will be closed three minutes later. Modify the connection configuration of the application synchronously, otherwise it may affect the business, so proceed with caution.

* Changing the port number will also change the port numbers of the private network and the public network simultaneously. After the new port takes effect, the old port will be closed immediately. Modify the connection configuration of the application synchronously, otherwise it may affect the business. Proceed with caution.

* Modifying the connection address prefix and port number will only take effect in the target connection endpoint and will not affect other connection endpoints. For example, if you change the default endpoint port number to 3307, the port number of the custom connection endpoint remains 3306.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the **Summary** page, click the **Connectivity** tab.

5. On the **Connectivity** tab, click **Edit** in the destination endpoint area.

6. In the **Connection information** area, click the **private address (ivolces.com) or private network port** after the <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png)<sub> </sub></span> icon, in the pop\-up dialog box to set the following parameters.

   
   |Name |Description |
   |---|---|
   |**Private network address** |In the private network address text box, enter the new private network address prefix. The connection address prefix rules are as follows:<br><br><br>* The connection address prefix must contain between 8 and 63 characters.<br><br>* The total length of the connection address cannot exceed 253 characters.<br><br>* Begin with a lowercase letter and end with a lowercase letter or number.<br><br>* Consists of lowercase letters, numbers, and hyphens (\-).<br><br>* The connection address prefix is not allowed to use the ID of other instances. |
   |**Modify port** |Enter a new port number in the private network port text box. The port number range is 1000 to 65534.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Changing the port number will also change the port numbers of the private network and the public network simultaneously. If the port number is modified before enabling public network access, the public network port number will automatically use the modified new port number after enabling public network access.</div><br> |
   

7. Click **OK**.

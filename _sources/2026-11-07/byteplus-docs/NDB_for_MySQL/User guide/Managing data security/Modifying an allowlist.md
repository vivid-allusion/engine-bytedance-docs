---
title: "Modifying an allowlist"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_an_allowlist"
---

This article describes how to modify the allowlist, including modifying the allowlist name, IP address, description, and other information.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* A single account in the same region can create up to 100 allowlists, each allowlist can contain up to 300 IP addresses or IP address segments, and each allowlist can bind up to 50 instances.

* A single instance can bind up to 100 allowlists and up to 1000 IP addresses.

* Supports setting IP segments in CIDR format, such as: `192.168.0.0/24`. When there are many IP addresses, it is recommended to merge the fragmented IPs into IP segments.

* Set `0.0.0.0/0` to allow all address access; set `127.0.0.1` to prohibit all address access. If you set `0.0.0.0/0` and `127.0.0.1` at the same time, all addresses are allowed to access.

* If you access the instance through a local device, you need to fill in the public IP of the local device.

* If you access the instance through the ECS server but the intranet connection conditions are not met, please fill in the public IP of the ECS instance; if the intranet connection conditions are met, fill in the private IP of the ECS instance.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. You can edit the allowlist in any of the following ways.

   * **Method 1**: Find the target allowlist directly in the **Allowlists**

      1. In the upper\-left corner of the top menu bar, select the project and region for the allowlist.

      2. Click **Allowlists** in the left\-side navigation bar.

      3. In the allowlist list, locate the target allowlist and click **Edit** for the actions column.

   * **Method 2**: Find the allowlist bound to the instance under the **Security** 

      1. In the upper\-left corner of the top menu bar, select the project and region to which the instance belongs.

      2. On the **Instances** page, click the target instance.

      3. At the top of the page, click the **Security** tab, and then click the target allowlist name.

      4. In the allowlist details panel that pops up, click **Edit** after the **Allowlist information**.

3. On the **Modify allowlist information** page, modify the allowlist information according to business needs.

   
   |Name |Description |
   |---|---|
   |Allowlist name |Enter allowlist name. The requirements are as follows:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* The length should be between 1 and 128 characters.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-). |
   |Description |The description of the allowlist, which cannot exceed 200 characters in length. |
   |IP address |Enter the IP address or address segment, support pasting the IP address or address segment, separated by Chinese and English commas, spaces or newline characters.<br><br><br>* Set an IP address such as: `192.168.0.1`, only that IP address is allowed to access.<br><br>* Set `0.0.0.0/0`, indicating that all addresses are allowed to access. At this time, if the public network connection address is opened or the database account password is not set, there will be a high security risk. Please set it carefully.<br><br>* When there are many IP addresses, it is recommended to merge the fragmented IPs into IP address segments in CIDR format, such as `192.168.0.0/32` (where any integer from 0 to 31 can be entered after `/`), which allows access from any IP address within that network segment. |
   |Security group |After associating an ECS security group, you can import the IP addresses of all ECS instances in that security group to the allowlist. This allows all these ECS instances to access the instance associated with the allowlist.<br><br>You can refer to the following steps to associate an ECS security group with the current allowlist:<br><br><br>1. Click **Select security group**.<br><br>2. In the pop\-up dialog box, select a security group to associate according to business needs from any security group association mode. Supports two association modes:<br><br>   * **Associated ECSIP**: Allows cloud servers within the security group to access the database. Currently, only the IP information of the primary network card is supported for import.<br><br>   * **Inbound IP**: Allows IP addresses involved in the TCP protocol and ALL protocol in the source addresses of the inbound direction of the security group to access the database. If the source address is configured as a security group, it will be ignored.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When associating with a security group, you can select any one of the association modes or both of the above association modes simultaneously, but it is required to ensure that there is at least one IP or IP address segment in the associated ECS security group.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Each allowlist can add up to 10 security groups.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">An allowlist supports at most 300 IPs or IP segments. If the number of IPs or IP segments involved in associating with a security group exceeds the limit, the association will fail. You can adjust the IPs in the security group and then re\-associate.   </div><br>   <br><br>3. Click **OK**.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To remove selected ECS Security groups from the current allowlist, click <strong>Disassociate</strong> in the <strong>Actions</strong> column on the right side of the Security group list.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After associating ECS Security groups, if the associated ECS Security groups are updated, you need to manually sync the ECS Security groups in the NDB for MySQL allowlist to retrieve the latest IP list from the ECS Security groups. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/6357/2550778">Synchronizing security group</a>.   </div><br>    |
   

4. Click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the allowlist has been associated with a security group before, after clicking <strong>OK</strong>, the system will determine whether the security group previously associated with the allowlist has been updated. If there are updates, the dialog box <strong>Updates detected in the associated security group. Do you want to synchronize?</strong> will pop up, and the IP changes of the security group (including added or removed IPs) will be listed in the dialog box. You can select <strong>Synchronize</strong> or <strong>Do not synchronize</strong> according to your needs, where:   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Synchronization</strong>: The system automatically identifies IP changes in the associated security group and updates the allowlist.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Do not synchronize</strong>: The system ignores these IP changes and retains the original IPs from the security group in the allowlist.   </div>
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyAllowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyAllowList) |Call the ModifyAllowList to modify the allowlist information. |

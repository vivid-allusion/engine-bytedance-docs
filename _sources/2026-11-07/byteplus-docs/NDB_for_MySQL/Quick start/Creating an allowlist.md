---
title: "Creating an allowlist"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_allowlist_1"
---


Allowlisting is a security measure for database connection. After an instance is created, all IP addresses are disabled from accessing the instance by default. This article describes how to manually add a client side IP address or address segment to a allowlist to successfully access the NDB for MySQL instance.

<span id="fbEpMDQq"></span>
## Background

Whether accessing the instance through the VPC intranet or the public network, you need to configure the allowlist of the instance before using it to ensure that the instance can be connected. Please maintain a allowlist regularly to clear the IP addresses of devices that do not need to access NDB for MySQL instances to ensure the security of database connections.

<span id="dmFJNThC"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

<span id="nH9IvSj2"></span>
## Precautions


* A single account in the same region can create up to 100 allowlists, each allowlist can contain up to 300 IP addresses or IP address segments, and each allowlist can bind up to 50 instances.

* A single instance can bind up to 100 allowlists and up to 1000 IP addresses.

* Supports setting IP segments in CIDR format, such as: `192.168.0.0/24`. When there are many IP addresses, it is recommended to merge the fragmented IPs into IP segments.

* Set `0.0.0.0/0` to allow all address access; set `127.0.0.1` to prohibit all address access. If you set `0.0.0.0/0` and `127.0.0.1` at the same time, all addresses are allowed to access.

* To access NDB for MySQL from a local device, fill in the public IP of the local device.

* If you access NDB for MySQL through the ECS server, but do not meet the conditions for intranet connection, please fill in the public IP of the ECS instance; if the conditions for intranet connection are met, fill in the private IP of the ECS instance.

* Each allowlist can add up to 10 security groups.

* After associating ECS Security groups, if the associated ECS Security groups are updated, you need to manually sync the ECS Security groups in the veDB MySQLNDB for MySQL allowlist to retrieve the latest IP list from the ECS Security groups. For specific procedures, refer to [Synchronizing security group](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Synchronizing_security_group).


<span id="GMTd0k3M"></span>
## Create allowlist


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. In the left navigation bar, choose **veDB\-MySQL** \> **Allowlists**.

4. On the **Allowlists** page, click **Create allowlist** and configure the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Affiliated project |Select the item to which the allowlist belongs, and depending on the item you selected in the upper left corner of the console, the following defaults will apply:<br><br><br>* If you select **All resources**, the newly created allowlist will be added to the **default** project by default, and other projects can also be selected according to business needs.<br><br>* If you select any specific project, the newly created allowlist will add that project by default, or you can select other projects based on your business needs. |
   |Allowlist name |Enter allowlist name. The requirements are as follows:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* The length should be between 1 and 128 characters.<br><br>* It can contain only Chinese characters, letters, digits, underscores ( _ ), and hyphens ( ). |
   |Description |Fill in the description of the allowlist, which must not exceed 200 characters in length. |
   |IP address |Enter the IP address or address segment, support pasting the IP address or address segment, separated by Chinese and English commas, spaces or newline characters.<br><br><br>* Set an IP address such as: `192.168.0.1`, only that IP address is allowed to access.<br><br>* Set `0.0.0.0/0`, indicating that all addresses are allowed to access. At this time, if the public network connection address is opened or the database account password is not set, there will be a high security risk. Please set it carefully.<br><br>* When there are many IP addresses, it is recommended to merge the fragmented IPs into IP address segments in CIDR format, such as: `192.168.0.0/24` (`/`You can enter any integer between 0 and 31 later) to allow IP address access within the network segment. |
   |Security group |After associating an ECS security group, you can import the IP addresses of all ECS instances in that security group to the allowlist. This allows all these ECS instances to access the instance associated with the allowlist.<br><br>You can refer to the following steps to associate an ECS security group with the current allowlist:<br><br><br>1. Click **Select security group**.<br><br>2. In the pop\-up dialog box, select a security group to associate according to business needs from any security group association mode. Supports two association modes:<br><br>   * **Associated ECSIP**: Allows cloud servers within the security group to access the database. Currently, only the IP information of the primary network card is supported for import.<br><br>   * **Inbound IP**: Allows IP addresses involved in the TCP protocol and ALL protocol in the source addresses of the inbound direction of the security group to access the database. If the source address is configured as a security group, it will be ignored.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When associating with a security group, you can select any one of the association modes or both of the above association modes simultaneously, but it is required to ensure that there is at least one IP or IP address segment in the associated ECS security group.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Each allowlist can add up to 10 security groups.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">An allowlist supports at most 300 IPs or IP segments. If the number of IPs or IP segments involved in associating with a security group exceeds the limit, the association will fail. You can adjust the IPs in the security group and then re\-associate.   </div><br>   <br><br>3. Click **OK**.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To remove selected ECS Security groups from the current allowlist, click <strong>Disassociate</strong> in the <strong>Actions</strong> column on the right side of the Security group list.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After associating ECS Security groups, if the associated ECS Security groups are updated, you need to manually sync the ECS Security groups in the veDB MySQLNDB for MySQL allowlist to retrieve the latest IP list from the ECS Security groups. For specific procedures, refer to <a href="https://www.volcengine.com/docs/6357/2550778">Synchronizing security group</a>.   </div><br>    |
   

5. Click **OK**.

   After the creation is successful, you can click on the target allowlist to enter the **Allowlist information** page to view the allowlist details.


<span id="aR6AdZiZ"></span>
## Subsequent Operations

[Associating allowlists and instances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Associating_allowlist_and_instance)

<span id="Iov7008w"></span>
## Related APIs


|API |Description |
|---|---|
|[CreateAllowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateAllowList) |Call the CreateAllowList to create a new allowlist. |
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAllowLists) |Call the DescribeAllowLists to query all allowlist information in the specified area under the current account. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAllowListDetail) |Call the DescribeAllowListDetail to query the detailed information of the allowlist. |

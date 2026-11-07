---
title: "Editing an allowlist"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/edit-allowlist"
---

After the Cache for Redis instance is created successfully, you can set allowlist for the instance to allow devices to access the instance. This topic describes how to edit the allowlist, including modifying the allowlist name, IP address, and whether or not to set it as the default allowlist.

## Precautions

* Each BytePlus account can create up to 1,000 allowlists per region.

* Each BytePlus account can allow up to one default allowlist per region. A newly created default allowlist will automatically override the existing default allowlist. That is, the existing default allowlist will automatically become a non\-default allowlist.

* Each allowlist can be associated with up to 200 instances at a time, and there is no limit to the total number of instances that can be associated.

* Each allowlist can be associated with up to 300 IP addresses or IP address segments in CIDR format.

* Each allowlist can be associated with up to 10 ECS security groups.

* Each instance can be associated with a maximum of 100 allowlists. A maximum of 100 allowlists can be associated at a time.

* Each instance can be associated with up to 1,000 IP addresses or IP address segments in CIDR format.

* If no allowlist is associated with an instance, its access is denied to all addresses.

* For data security reasons, it is not allowed to add the address `0.0.0.0/0` to the allowlist of the instance while enabling the password\-free access function. If you need to set address `0.0.0.0/0` in the allowlist, disable the instance's password\-free access feature first. To enable password\-free access, refer to [Password-free access](https://docs.byteplus.com/en/docs/redis/pwd-free-access).

* Cache for Redis can be used with [Database Transmission Service (DTS)](https://docs.byteplus.com/en/docs/DTS/about_database_transmission_service) and [Database Workshop (DBW)](https://docs.byteplus.com/en/docs/DBW/what-is-database-workbench). To ensure normal access between Redis and DTS or DBW, the system creates corresponding allowlists for them in the Redis allowlist. These system\-built allowlists cannot be edited, modified, or copied.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. In the left navigation bar, choose **NoSQL Database\> Redis \> Allowlists**.

4. On the **Allowlist** page, locate the target allowlist and perform the corresponding actions as needed.

   **Modify allowlist name**

1. Hover over the target allowlist name and click![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_0027dfc272db9b47beaa55ae5832abc6.jpg)icon next to the name.

   2. Enter a new name in the pop\-up dialog box.

      > **tip**

      > The name must meet the following requirements:

      * > It cannot start with a number or hyphen (\-).

      * > It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).

      * > The length should be 1 to 128 characters.

   3. Click **OK**.

   **Modify allowlist IP address**

1. Click the name of the target allowlist.

      > **tip**

      > You can also find the target allowlist on the **Security** tab of the Redis instance. The specific method is as follows:

      1. > Log in to the [Redis console](https://console.byteplus.com/db/redis).

      2. > In the top menu bar, select the project and region to which the instance belongs.

      3. > On the **Instances** page, click the target instance.

      4. > On the instance details page, click the **Security** tab.

      5. > In the allowlist under the **Allowlist settings** sub\-tab, find and click the name of the target allowlist.

   2. In the pop\-up panel, click **Edit** after **Allowlist information**.

   3. In the **IP address** dialog box of **Modify allowlist information** panel, enter an IP address or an address segment in CIDR format.

      > **tip**

      * > If you enter or paste an incorrect IP address or address segment, you can double\-click the IP address or address segment that needs to be modified, and then modify it to the correct IP address or address segment in the Edit IP pop\-up window.

      * > Duplicate addresses are not allowed. Separate multiple addresses with commas (,).

      * > Setting `0.0.0.0/0` indicates that all addresses are allowed to access. Setting `127.0.0.1` indicates that all addresses are denied access. If set both `0.0.0.0/0` and `127.0.0.1`, all addresses are allowed to access.

      * > Setting CIDR `192.168.1.0/24` indicates that IP addresses within this network segment are allowed to access. If set `192.168.1.1`, only this IP address is allowed to access.

   4. Click **OK**.

   5. In the pop\-up dialog box, click **OK**.

      > **tip**

      > This modification will be applied to all instances associated with this allowlist.

   **Set default aAllowlist**

1. Click the name of the target allowlist.

      > **tip**

      > You can also find the target allowlist on the **Security** tab of the Redis instance. The specific method is as follows:

      1. > Log in to the [Redis console](https://console.byteplus.com/db/redis).

      2. > In the top menu bar, select the project and region to which the instance belongs.

      3. > On the **Instances** page, click the target instance.

      4. > On the instance details page, click the **Security** tab.

      5. > In the allowlist under the **Allowlist settings** sub\-tab, find and click the name of the target allowlist.

   2. In the **Default allowlist** area of the **Modify allowlist information** panel, select whether to set the current allowlist as the default allowlist according to business needs.

      > **tip**

      * > If set as the default allowlist, it is automatically selected when creating new instances.

      * > Each BytePlus account can allow up to one default allowlist per region. A newly created default allowlist will automatically override the existing default allowlist. That is, the existing default allowlist will automatically become a non\-default allowlist. For more details, refer to [Constraints and limits](https://docs.byteplus.com/en/docs/redis/quota-and-limit#.5Yqf6IO954m55oCn6ZmQ5Yi2).

   3. Click **OK**.

   **Associate security group**

1. Click the name of the target allowlist.

   2. In the pop\-up panel, click **Edit** next to **Allowlist information**.

   3. In the **Security group** area of the **Modify allowlist information** panel, perform the following operations:

      1. Click **Select security group**.

      2. In the pop\-up dialog box, select a security group to associate according to business needs from any security group association mode.

         Redis allowlists support the following two association modes:

         * **Associated ECS IP**: Allows cloud servers within the security group to access the database. Currently, only the IP information of the primary network card is supported for import.

         * **Inbound IP**: Allows IP addresses involved in the TCP protocol and ALL protocol in the source addresses of the inbound direction of the security group to access the database. If the source address is configured as a security group, it will be ignored.

         > **tip**

         * > When associating with a security group, you can select any one of the association modes or both of the above association modes simultaneously, but it is required to ensure that there is at least one IP or IP address segment in the associated ECS security group.

         * > Each allowlist can be associated with at most 10 ECS security groups.

         * > An allowlist supports at most 300 IPs or IP segments. If the number of IPs or IP segments involved in associating with a security group exceeds the limit, the association will fail. You can adjust the IPs in the security group and then re\-associate.

      3. Click **OK**.

         > **tip**

         * > To remove selected ECS Security groups from the current allowlist, click **Disassociate** in the **Actions** column on the right side of the Security group list.

         * > After associating ECS Security groups, if the associated ECS Security groups are updated, you need to manually sync the ECS Security groups in the Redis allowlist to retrieve the latest IP list from the ECS Security groups. For specific procedures, refer to [Synchronizing security group](https://docs.byteplus.com/en/docs/redis/synchronizing_the_security_group).

   4. Click **OK**.

      > **tip**

      > If the allowlist has been associated with a security group before, after clicking **OK**, the system will determine whether the security group previously associated with the allowlist has been updated. If there are updates, the dialog box **Updates detected in the associated security group. Do you want to synchronize?** will pop up, and the IP changes of the security group (including added or removed IPs) will be listed in the dialog box. You can select **Synchronize** or **Do not synchronize** according to your needs, where:

      * > **Synchronize**: The system automatically identifies IP changes in the associated security group and updates the allowlist.

      * > **Do not synchronize**: The system ignores these IP changes and retains the original IPs from the security group in the allowlist.

   **Other operations**

For other operations on the allowlist, refer to:

   * [Associating instances and allowlists](https://docs.byteplus.com/en/docs/redis/associate-allowlist)

   * [Disassociating instances from allowlists](https://docs.byteplus.com/en/docs/redis/disassociate-allowlist)

   * [Copying allowlist](https://docs.byteplus.com/en/docs/redis/copying_a_allowlist)

   * [Deleting allowlist](https://docs.byteplus.com/en/docs/redis/delete-allowlist)

## Relevant APIs

|API |Description |
|---|---|
|[ModifyAllowList](https://docs.byteplus.com/en/docs/redis/modifyallowlist) |Call the ModifyAllowList API to modify the target allowlist information (such as allowlist name, IP address, whether it is set as the default allowlist). |
|[AssociateAllowList](https://docs.byteplus.com/en/docs/redis/associateallowlist) |Call the AssociateAllowList API to associate the target instance to the specified IP address allowlist. |
|[DisassociateAllowList](https://docs.byteplus.com/en/docs/redis/disassociateallowlist) |Call the DisassociateAllowList API to disassociate the target instance from the specified IP address allowlist. |
|[DeleteAllowList](https://docs.byteplus.com/en/docs/redis/deleteallowlist) |Call the DeleteAllowList API to delete the target allowlist. |

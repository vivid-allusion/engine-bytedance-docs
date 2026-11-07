---
title: "Synchronizing security group"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Synchronizing_security_group"
---

After associating an ECS security group with the allowlist, if the associated ECS security group has been updated, you can manually synchronize the ECS security group in the allowlist to obtain the latest IP list in the ECS security group. This topic describes the procedure for synchronizing the security group.

<span id="BinHvWg7"></span>
## Prerequisites


* The ECS security group has been created. For specific procedure, refer to [Creating security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).

* The ECS security group has been associated with the allowlist. You can associate the ECS security group when creating or editing the allowlist. For specific procedure, refer to [Creating allowlist](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_allowlist) or [Editing allowlist](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_an_allowlist).

* If the allowlist associated with the security group has been bound to an instance, the status of all instances needs to be **Running**.


<span id="VksyXTqq"></span>
## Precautions


* After confirming the synchronization of the security group, the system will automatically identify the IP changes in the security group associated with the allowlist and update the IP information in the allowlist (such as adding or reducing IPs). Confirm whether the removal of the reduced IPs from the allowlist affects the business.

* An allowlist supports a maximum of 300 IPs or IP segments. If the IPs or IP segments involved in the associated security group exceed the limit, the synchronization will fail (that is, none of the IPs involved in this task will be synchronized). You can adjust the IPs in the security group and resynchronize.


<span id="YEM3dQ3I"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the allowlist.

3. Click **Allowlists** in the left\-side navigation bar.

4. On the **Allowlists** page, find the target allowlist and click **Sync** in the **Associated security** groups column of the target allowlist.

5. In the popped\-up dialog box, confirm the IP changes before and after synchronization (such as added or reduced IPs or IP segments), and click **OK** after confirming that there are no errors.

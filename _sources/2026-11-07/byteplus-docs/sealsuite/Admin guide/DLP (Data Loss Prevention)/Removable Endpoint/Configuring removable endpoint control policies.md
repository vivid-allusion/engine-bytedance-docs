---
title: "Configuring removable endpoint control policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-peripheral-control-rules"
---

You can configure detection policies in the Removable Endpoint function for DLP. The policy is mainly used to detect and restrict the access permissions of peripherals on user devices and supports sending message notifications to remind users when there is a peripheral connection action on user devices. In addition, you can view the alert events triggered by the policy in the SealSuite Admin Console.

<span id="064dedd7"></span>
# Creating a policy


1. Log in to the Admin Console.

2. In the left navigation bar, click **DLP** \> **Removable Endpoint**.

3. On the **Removable Endpoint** page, click the **Policy Management** tab.

4. On the **Policy Management** tab, click **New Policy**.

5. On the **Add Detection Policy** page, complete the following configurations and click **Confirm**.

   
   |**Item** |**Description** |
   |---|---|
   |**Policy Name** |Create a custom name to identify the policy. |
   |**Priority** |Configure the priority of the current policy. The range of values is from 0 to 100, with a higher value indicating a higher priority. You can have multiple policies in effect at the same time. When SealSuite detects users' devices, it matches the policies in order according to the priority value. Once a matching policy is found, SealSuite stops the detection process. If no matching policy is found, SealSuite stops the detection process after executing all policies. If there are two policies with the same priority value, the one with the latest modification time will be executed first. |
   |**Control equipment type** |Select the types of external devices to be detected by the current policy. You can choose from **Thumb Drive**, **Portable Hard Disk**, **CD\-ROM**, **USB wired network interface card**, and **USB wireless network interface card**. Multiple selection is supported. |
   |**Access Control** |To set access control policies for connected peripheral devices, select one of the following modes.<br><br><br>* **Read and write mode**: No restrictions on reading and writing, only background alerts.<br><br>* **Read\-only mode**: Allows reading data from peripherals, and does not allow writing data to peripherals.<br><br>* **Disable mode**: Peripherals are not allowed to access the computer.<br><br>* **Audit mode**: When peripherals are connected, it is allowed, but an alert is reported. |
   |**Notification** |Whether to enable message notifications. After you have enabled this feature, the SealSuite client will send notifications to users when they are connecting a peripheral device to a computer.<br><br>In the **Notification** area, toggle the switch to enable this option. To view default notification content and obtain a preview of the notification, click **Edit notification template**. You can also modify the notification content yourself.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Notifications are displayed in both Chinese and English. When modifying the configuration of notifications, you need to synchronize changes to notification contents in both languages to avoid inconsistent configurations in a multilingual environment.</div><br> |
   |**Scope** |Limit the scope in the dimension of **Employee** or **Device**.<br><br><br>* When selecting **Employee**, you need to limit the range by **Department** or **Role**.<br><br>* When selecting **Device**, you need to limit the range by **Device**, **Operating System (OS)** , and **Group**. |
   


<span id="50549891"></span>
# Enabling or disabling a policy


1. Log in to the Admin Console.

2. In the left navigation bar, click **DLP** \> **Removable Endpoint**.

3. On the **Removable Endpoint** page, click the **Policy Management** tab.

4. Locate your target policy, and toggle the switch as shown in the picture below to enable or disable the specified policy.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b389b9e47da43adbf4dbcdb41d7d703~tplv-goo7wpa0wc-image.image) </span>

   * When this switch is turned on, the current policy is activated, and SealSuite will enforce removable endpoint control according to the policy's configuration.

   * When this switch is turned off, the current policy is deactivated, and SealSuite will not apply this policy.


<span id="941470e9"></span>
# Editing a Removable Endpoint policy


1. Log in to the Admin Console.

2. In the left navigation bar, click **DLP** \> **Removable Endpoint**.

3. On the **Removable Endpoint** page, click the **Policy Management** tab.

4. On the right side of your target policy, click **Edit**.

5. On the editing page, adjust the configuration items and click **Confirm**.

   For instructions on how to configure each item, please refer to [Creating a removable device policy](https://docs.byteplus.com/docs/sealsuite/docs-configuring-peripheral-control-rules#064dedd7).


<span id="43d211e2"></span>
# Deleting a Removable Endpoint policy

Please proceed with caution when deleting a Removable Endpoint policy, because the policy will no longer take effect on user devices after being deleted.


1. Log in to the Admin Console.

2. In the left navigation bar, click **DLP** \> **Removable Endpoint**.

3. On the **Removable Endpoint** page, click the **Policy Management** tab.

4. On the right side of your target policy, click **More** \> **Delete**.

5. In the **Warning** dialog box, click **Confirm delete**.


<span id="ddd8c2e4"></span>
# Related operations


* To view existing Removable Endpoint alert events, please refer to [Viewing peripheral control alerts](https://docs.byteplus.com/docs/sealsuite/docs-viewing-peripheral-control-events).

* To prevent Removable Endpoint policies from taking effect on specified peripheral devices, set an allowlist for these specified peripheral devices. For more information on this, please refer to [Configuring removable endpoint control policy allowlist](https://docs.byteplus.com/docs/sealsuite/docs-configuring-peripheral-control-rules-allowlist).

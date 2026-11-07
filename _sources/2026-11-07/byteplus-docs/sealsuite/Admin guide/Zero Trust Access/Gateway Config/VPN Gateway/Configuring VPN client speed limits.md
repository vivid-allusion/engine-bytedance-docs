---
title: "Configuring VPN client speed limits"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-vpn-client-speed-limits"
---

You can set upload and download speed limits for your VPN clients, either by applying a global limit to an entire VPN node or by creating granular, policy\-based limits for specific users and devices.

<span id="a3494ac9"></span>
# Why Configure Speed Limits?

By implementing speed limits, you can achieve more granular control over your network's bandwidth allocation. This allows you to prioritize critical business traffic, ensure a smooth experience for key users, and prevent non\-essential activities from impacting overall network performance and stability.


* **Node Speed Limit:**  Apply a baseline upload and download speed limit to all clients connected to a specific VPN node.

* **Employee Speed Limit:**  Create targeted policies to assign different speed limits to different groups. For example, you can grant higher bandwidth to a department that frequently handles large file transfers while applying a lower limit to general administrative staff. You can also set different limits based on device type, such as a lower speed for mobile devices to conserve cellular data.


<span id="7c0bedd7"></span>
# How to Configure Speed Limits


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Zero Trust Access** \> **Gateway Config** \> **VPN Gateway**.

3. Click the card for the VPN node you want to configure.

4. Go to the **Client Speed Limit** tab and enable the main toggle switch.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/631051da960447f6b646827266ce81a6~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Once enabled, you must configure at least one type of speed limit for the feature to have an effect. You can apply a general limit to the entire node, create specific limits using policies, or use both together.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Understanding the Priority:</strong>   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The node\-level limit acts as the default for all users connected to this node.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A policy\-based limit will <strong>override</strong> the node\-level limit for any user or device that matches the policy's scope.   </div>
   

5. Configure a Speed Limit. Choose one or both of the following methods:

   * **Method A: Set a Node Speed Limit**

      Use this method to apply a single, baseline speed limit to every user connected to this node.

      In the **Node Speed Limit Configuration** section, click **Edit**. Set the **Client upload speed limit (Kb/s)**  and **Client download speed limit (Kb/s)** . A value of `0` means no limit. Click **Confirm**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cda1e6d2bb9f4a40a6251afcaf0ae06c~tplv-goo7wpa0wc-image.image) </span>

   * **Method B: Create an Employee Speed Limit Policy**

      Use this method to set granular speed limits for specific users, departments, or device types.

      In the **Employee Speed Limit Policy** section, click  **+ Add New Policy**. Configure the following and click **Confirm**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf3595c4a1534b6da9ba875e797b483f~tplv-goo7wpa0wc-image.image) </span>

      
      |**Parameter** |**Description** |
      |---|---|
      |**Policy Name** |A user\-friendly name to identify the policy. |
      |**Priority** |The policy's execution order (0\-100). Higher numbers have higher priority. If a user matches multiple policies, only the one with the highest priority is applied. |
      |**Upload speed limit Kb/s** |The custom upload speed limit in Kb/s (0\-65525). `0` means no limit. |
      |**Download speed limit Kb/s** |The custom download speed limit in Kb/s (0\-65525). `0` means no limit. |
      |**Scope** |Define who or what this policy applies to. You can target by **User** (scoped by **Department** or **Role**) or by **Device** (scoped by **Device** or **Device Group**). |
      

6. (Optional) To manage existing policies:

   From the policy list, you can perform the following actions:

   * **Change Priority:**  Click the priority number for a policy and select a new value from the drop\-down.

   * **Edit:**  Click **Edit** in the **Action** column to modify a policy's settings.

   * **Delete:**  Click **Delete** in the **Action** column, or select multiple policies and use the **Batch Delete** button.

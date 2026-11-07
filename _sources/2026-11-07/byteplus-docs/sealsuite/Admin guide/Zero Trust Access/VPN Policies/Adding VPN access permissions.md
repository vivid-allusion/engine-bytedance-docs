---
title: "Adding VPN access permissions"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-adding-vpn-access-permissions_2"
---

By default, the newly integrated VPN gateway is not automatically accessible to all users. To enable access, you need to grant access permissions to users and set effective periods for the access permissions. Upon expiration, the permissions are automatically revoked. This feature caters to the needs of temporary remote work scenarios, ensuring secure and time\-bound access to the VPN gateway.

<span id="操作步骤"></span>
# Procedure


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Zero Trust Access** \> **VPN** \> **ACL Policy**.

3. In the upper\-right corner of the **Permissions** page, click **Add Permissions**.

4. In the **Add VPN Access Permissions** dialog box, complete the following configuration and click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5dca4eabddb3453984f00ad48d4822b5~tplv-goo7wpa0wc-image.image) </span>

   The description of each configuration item is as follows:

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Scope** |You can assign permissions to specific users by **Department** or **Role**. |
   |**Expiration** |Available options include:<br><br><br>* **Permanent**<br><br>* **7 days**<br><br>* **30 days**<br><br>* **90 days**<br><br>* **180 days**<br><br>* **Custom**<br><br><br>Please note for **Custom** option, you will need to specify the exact number of days for this option to be effective. |
   

   All the newly created access permissions will be listed under the **Access Group View** tab. You can view and manage permissions through the tab. Also, you can take the following actions in the **Action** column:

   * To adjust the effective period of permissions, click **Update Expiration**.

   * To revoke permissions for designated users, click **Remove**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f40d2201f9394c548b7fe378f02c01f5~tplv-goo7wpa0wc-image.image) </span>

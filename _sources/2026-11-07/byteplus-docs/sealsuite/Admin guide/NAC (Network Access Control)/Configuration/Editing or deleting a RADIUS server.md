---
title: "Editing or deleting a RADIUS server"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-editing-or-deleting-a-radius-server"
---

On the **RADIUS server** page, you can edit the RADIUS server's name, IP address, and status, as well as download server logs or delete the server.

<span id="9ee536f3"></span>
# Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, click **NAC** \> **Config**.

3. Under the **RADIUS server** tab, locate and click your target server to go to the server details page.

   In the Details page, you can perform the following operations:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b6a1191ead44f96bbddb3a7ba8505e6~tplv-goo7wpa0wc-image.image) </span>

   * As shown in area 1 in the above image, you can switch to another RADIUS server details page.

   * As shown in area 2 in the above image, you can view and edit the following information of the RADIUS server.

      
      |**Configuration Item** |**Description** |
      |---|---|
      |**Name** |Edit the name of the RADIUS server. |
      |**Status** |Switch the status of the RADIUS server to **Publish** or **Offline**. |
      |**IP address** |Edit the IP address of the RADIUS server. To edit the IP address, the RADIUS server must be offline first. |
      |**Employee Wi\-Fi authentication port** |Edit the port used for client employee Wi\-Fi identity authentication, which is set to 1812 by default or has been customized. |
      |**Employee Wi\-Fi accounting port** |Edit the port used for client employee Wi\-Fi billing, which is set to 1813 by default or has been customized. |
      |**Guest Wi\-Fi authentication port** |Edit the port used for client guest Wi\-Fi identity authentication, which is set to 3812 by default or has been customized. |
      |**Guest Wi\-Fi accounting port** |Edit the port used for client guest Wi\-Fi billing, which is set to 3813 by default or has been customized. |
      |**Wired network authentication port** |Edit the port used for client wired network identity authentication, which is set to 2812 by default or has been customized. |
      |**Wired network accounting port** |Edit the port used for client wired network billing, which is set to 2813 by default or has been customized. |
      |**App ID** |Each RADIUS server has a unique component ID that can be copied to the RADIUS installation package for service verification. |
      |**App Secret** |Each RADIUS server has a unique component secret that can be copied to the RADIUS installation package for service verification. |
      |**Custom Attributes** |The SealSuite RADIUS server includes a built\-in portal server, which is mainly used for guest Wi\-Fi portal authentication. To configure the guest portal authentication, please refer to [Managing guest portal server](https://docs.byteplus.com/docs/sealsuite/docs-managing-guest-portal-server). |
      

   * As shown in area 3 in the above image, you can download the RADIUS server logs or delete the server.

      * **Log download**: You can choose to download all available logs from the past 24 hours, or logs from the past 72 hours.

      * **Delete**: If you delete the RADIUS server, new users cannot connect to the enterprise Wi\-Fi, and existing users will be disconnected automatically. After deletion, you need to delete the RADIUS configuration in the wireless router or switch.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Please proceed with caution when deleting the servers, because they cannot be restored after being deleted.         </div>

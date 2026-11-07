---
title: "Configuring removable endpoint control policy allowlist"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-peripheral-control-rules-allowlist"
---

If there are external devices that need to be connected to the users' devices for work purposes, you can configure an allowlist for removable endpoint policies and add the specified external devices to the allowlist. Peripheral devices in the allowlist will not be affected by the removable endpoint policy.

<span id="437e7306"></span>
# Instructions for use

This article mainly introduces how to configure a removable endpoint policy allowlist for external devices. If you want to configure a removable endpoint policy allowlist for specific users or devices, you need to configure a global allowlist. For the instructions, please refer to [Configuring global allowlist](https://docs.byteplus.com/docs/sealsuite/docs-configuring-global-allowlist).

<span id="6b494dd6"></span>
# Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, click **DLP** \> **Removable Endpoint**.

3. On the **Removable Endpoint** page, click the **Allowlist Settings** tab.

4. On the Allowlist Settings tab, click **Add to Allowlist**, you can choose **Add manually** or **Import**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fae3a9b60219443588aea67a0df34e9a~tplv-goo7wpa0wc-image.image) </span>

   * **Add manually**

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86bd8738dbe143fcb45bc1ffe7cddb41~tplv-goo7wpa0wc-image.image) </span>

      On the **Manually Add Whitelist** page, configure the relevant parameters as described in the table below.

      
      |**Parameter** |**Description** |
      |---|---|
      |User information |(Optional) Specify the department, user, or role to which this allowlist policy applies. If no user information is specified, the allowlisted device can be used by any user.<br><br>Example: Allow John Doe to use USB flash drives and memory cards. |
      |Device information |(Optional) Specify the device information for which this allowlist policy is effective. You can specify a single device, a device group, or an operating system.<br><br>Example: Allow John Doe's macOS device, Device A, to use USB flash drives and memory cards. |
      |Peripheral type |Select the type of removable endpoint from the drop\-down list. |
      |Add type |The add types include:<br><br><br>* **Without**: Does not specify a particular external device. For example, if you want to allowlist an entire category of external devices, you can select **Without** for the Add Type.<br><br>* **Add a single device**: Requires you to provide the external device's VID, PID, Serial Number, and remarks.<br><br>* **Add multiple devices**: If the external devices are procured in the same batch, you can add them in bulk by providing only their VID, PID, and remarks, without needing to enter individual serial numbers. |
      |VID |The Vendor ID (VID) of the device. |
      |PID |The Product ID (PID) of the device. |
      |Serial number |Required when adding a device individually; not required for bulk additions. |
      |Whitening time |The duration for which the external device is allowlisted. After the expiration date, the device will no longer be permitted. The default is permanent. |
      |Remarks |Remarks for the device for easy identification. |
      

   * **Import**

      1. On the **Import** page, download the Template.

      2. Fill in the template with the relevant parameters according to the instructions provided.

      3. Return to the **Import** page in the admin console and **upload** the completed template.

5. After you complete the configuration, click **OK**.

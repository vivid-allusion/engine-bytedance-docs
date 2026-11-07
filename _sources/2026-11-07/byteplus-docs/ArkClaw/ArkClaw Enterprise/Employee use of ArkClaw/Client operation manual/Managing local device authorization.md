---
title: "Managing local device authorization"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Revoking_local_device_authorization"
---

When the ArkClaw client needs to access and manage local files in , authorize the local device in **Device management**. You can also configure and manage ArkClaw's permissions to access local files. You can also view the authorization status of the current device on this page and process pending authorization requests for the local device.

## Application scenarios

* View the list and status of client devices authorized for the current instance.

* Re\-pair the local device when it connects to ArkClaw for the first time or when its credentials are abnormal.

* Revoke other devices' authorization for the current instance when the devices are no longer in use.

## Authorize a device

1. Log in to the ArkClaw client locally.

2. switch to the target ArkClaw instance.

3. Click the "Enter project space \> Add project \> Pair" button at the bottom of the chat box.

   > This step does not actually add a project. It only navigates to the device authorization page.

4. In the **Pending local authorization request** section **,**  verify that the device information is correct, and click "Click to authorize and enable read\-write access to local computer files" **.**

5. In the dialog box that appears, click "Authorize" to authorize the local device.

   > This operation authorizes only the current device. The local capability plugin has taken over command approval, so you do not need to rewrite the OpenClaw gateway configuration, and the instance does not restart because of configuration changes. Keep the ArkClaw client and this page open during authorization until the process is complete.

6. After authorization is complete, the current device is ready for subsequent file operations only when the page shows the "Local device is connected" message and the device status is **Authorized** and **Online**.

   > **tip**

   > After the device goes offline, the authorization relationship is retained, but directory permissions cannot be synchronized while the device is offline. You can click "Re\-pair Local Device" to restart the pairing process.

   7. (Optional) Click "Go to Security management" at the bottom of the page to open the Security management page, where you can configure file access permissions, command risk control, and other security policies. For details, see [Managing local file access permissions](https://docs.byteplus.com/en/docs/ArkClaw/Managing_local_file_access_permissions).

## Revoking local device authorization

> **warning**

> Revoking authorization immediately disconnects the device from the current instance and removes the authorization relationship. To use it again, you need to [re\-authorize](https://docs.byteplus.com/en/docs/ArkClaw/Installing_and_using_the_client?lang=en#ZJ0j4Jsu) it on that device.

1. Log in to the ArkClaw client locally.

2. Switch to the target ArkClaw instance, and click the more icon in the upper\-right corner.

3. Click the "Device management" button.

4. In the **Local device** section, click the "Delete" button.

5. In the dialog box that appears, click "Confirm removal" to complete the operation.

---
title: "Disabling UAC"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Disable-UAC"
---

UAC (User Account Control) prompts you when a program attempts to make changes that require administrator permissions, and it also blocks certain program actions. Before migration, you need to disable the UAC feature on your migration source server to prevent migration failures.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the instance as your migration source server using an account with administrator permissions.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This topic uses an instance running Windows Server 2022 Datacenter Edition 64 bit operating system as an example to describe how to disable UAC.   </div>
   

2. Right\-click the "Start" button and select "Run".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_34f4398fdd336368595a86960e4aa34c.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_34f4398fdd336368595a86960e4aa34c.png) </span>

3. In the "Run" dialog box, enter the following content, and click the "OK" button.

   ```Plain Text
   UserAccountControlSettings
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8eba64d6a1c5b9cdc1bc212f069edf36.png) </span>

4. In the "User Account Control Settings" dialog box, adjust the slider to the lowest level.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7792a0f38b3564a2272140aabd35d780.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7792a0f38b3564a2272140aabd35d780.png) </span>

5. Click the "OK" button to save the change and then restart the server for the change to take effect.

6. Subsequently, you can continue to complete other [preparations](https://docs.byteplus.com/en/docs/smc/Preparations) or [perform migration pre-check](https://docs.byteplus.com/en/docs/smc/Perform-a-migration-precheck) again.

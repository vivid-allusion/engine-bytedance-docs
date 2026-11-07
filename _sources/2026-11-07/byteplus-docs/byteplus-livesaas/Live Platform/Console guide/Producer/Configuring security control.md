---
title: "Configuring security control"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/configuring-security-control"
---

BytePlus Live places great emphasis on the security of live content and the protection of viewer's personal information. On the **Security control** page, you can:


* Enable the full\-screen watermark feature to prevent leakage of live content. You can also trace the source based on the watermark content.

* Enable the features of repeated login prevention, nickname modification, and anonymous comments to protect the privacy of viewers and foster interactive communication in the live room.

* Enable the comment report feature to allow viewers to report comments suspected of advertising promotion, regulation violations, and other issues.


<span id="afb6449e"></span>
## Prerequisite

A BytePlus account or an IAM user with Producer \> Edit permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="b716c5af"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. On the left navigation pane, click **Producer** \> **Security control**.

4. On the **Basic settings** tab, you can perform the following operations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5613d0c501b545d68cbf991eb794dba6~tplv-goo7wpa0wc-image.image) </span>

   * Turn on the **Repeated login prevention** switch to prevent viewers from logging in repeatedly to the same live room with the same account. The previous login will be forced to log out as soon as the subsequent login succeeds. For example, if a viewer logs in to the live room with a phone number on a PC, and then logs in to the same live room with the same phone number on a mobile device, the login on the PC will be forced to log out.

   * Turn on the **Nickname modification** switch to allow viewers to modify their nicknames in the live room.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Viewers must log in to the live room before modifying their nicknames. However, if <strong>Public</strong> is set as the comment restriction on the <strong>Producer</strong> \> <strong>Viewing restrictions</strong> page, viewers can modify their nicknames directly.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Nicknames cannot exceed 60 characters and cannot contain sensitive words.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Viewers can only modify their nicknames once within a 7\-day period in this live room.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The modified nickname only applies to this live room. However, if viewers log in to the live room by using their phone numbers, the modified nickname applies to all the live rooms under the current account.      </div>
      

   * Turn on the **Anonymous comments** switch to only display the first and last characters of a viewer's nickname, with the middle characters replaced by \*\*\*, in the chat area of the viewing page. For example, the nickname Viewer A is displayed as V\*\*\*A.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If a nickname has only one character, then \*\*\* is added after that character.      </div>
      

   * Turn on the **Comment report** switch to allow viewers to report comments sent by other viewers in the live room.

5. On the **Full\-screen watermark** tab, turn on the **Full\-screen watermark** switch to add watermark to the full screen of the viewing page.

   * For viewers without logging in, use **All rights reserved.**  as the watermark.

   * For logged\-in viewers, use their nicknames as watermarks, except for the following viewing restrictions:

      * Phone number: Use "nickname + the last four digits of the phone number" as the watermark.

      * Allowlist: Use allowlist information as the watermark.


<span id="d5f4846e"></span>
## What your viewers see


|Feature |On PCs |On mobile devices |Description |
|---|---|---|---|
|Repeated login prevention |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55d2cf8eb639424095ee76e87c44c155~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/142252a5488c4c38951b00060189a8ef~tplv-goo7wpa0wc-image.image) </span> |None. |
|Nickname modification |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd629b76378b4bf295a2d447740f41c3~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/532b644f5def41d39ae57c39838c5674~tplv-goo7wpa0wc-image.image) </span> |None. |
|Full\-screen watermark |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c792989f6fab4592ab188b9e70725e13~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72fbd419d88442d0ae9efc36ee96e843~tplv-goo7wpa0wc-image.image) </span> |None. |
|Anonymous comments |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e94bd2c2b5dd472888ddd8e5e3086e9c~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/625cb6a988cf44658474ed0b20559b05~tplv-goo7wpa0wc-image.image) </span> |None. |
|Comment report |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31e099ea3aad4edbb330082da77d848d~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b1d74df8a8f4ded89754fc32caf6dd0~tplv-goo7wpa0wc-image.image) </span> |Viewers can right\-click the comment on PCs or tap the comment on mobile devices, and then select **Report**. In the **Report comments** dialog box or on the **Report comments** page that appears, they can select a reason and then click **Submit**. |

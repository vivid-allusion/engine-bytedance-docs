---
title: "Custom authentication login"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions"
---

BytePlus Live supports the custom authentication login method. That is, with the viewing restriction set to **Custom**, users must log in to your own account system before watching a live stream, sending comments, and more.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To use this feature, make sure that you have developer sources.</div>


<span id="bec9a05f"></span>
## Prerequisite

A BytePlus account or an IAM user with Producer \> Edit permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="3a98c42f"></span>
## Scenarios


* [Solution A](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions#71eea3ee): This solution applies to live scenarios where confidentiality is a certain requirement or product promotion scenarios. If a user enters a live room without logging in, they can be redirected to the login page of your own account system. Once the user logs in to your own account system, they can be redirected to the viewing page for watching a live stream, sending comments, and more.

* [Solution B](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions#29214805): This solution applies to scenarios where you want to avoid a second login after a user logs in to your own account system. After the user logs in to your own account system, they can click the corresponding URL (the viewing page address with authentication parameters that you have concatenated) in the system to enter the live room for watching a live stream, sending comments, and more.


<span id="a5b00644"></span>
## Note

If your live room is embedded into your own page through iframe, you must customize the domain name of the viewing page by adding an alias record (CNAME record), thereby ensuring your page's domain name is the same as the viewing page's domain name. This helps avoid the issue of browsers prohibiting third\-party cookies from being written. To add a CNAME record, contact your sales representative.

<span id="5dd85fad"></span>
## Process

<span id="71eea3ee"></span>
### Solution A

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a96b8fae4fd04bcc827b6c5d3f8b2ef8~tplv-goo7wpa0wc-image.image) </span>


1. A user visits the viewing page of BytePlus Live.

2. BytePlus Live carries the `ActivityId`, `Timestamp`, and `RedirectUrl` parameters to redirect the user to the login page (the login link configured in [Procedure](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions#447f1c83)) of your own account system.

   * If the authentication type is set to **Custom**: After the user visits the viewing page, BytePlus Live carries the preceding parameters to redirect the user to the login page of your own account system.

   * If the comment restriction is set to **Custom**: When the user sends comments or participates in interactive activities such as lucky draws on the viewing page, BytePlus Live carries the preceding parameters to redirect the user to the login page of your own account system.

3. The user logs in to your own account system on the system login page.

4. Your own account system calculates the signature using relevant parameters after having verified the user identity.

5. Your own account system carries parameters `UserId`, `Nickname`, `Timestamp`, and `Sign`, as well as other parameters to redirect the user to the authentication page (`RedirectUrl`) of BytePlus Live.

6. BytePlus Live verifies the signature (`Sign` value) on the authentication page to determine whether to allow the user to watch a live stream, send comments, and more.

7. If the verification is passed, that is, the signature calculated by BytePlus Live is the same as the `Sign` value carried by your own account system, the user can then watch a live stream, send comments, and more.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the verification is not passed, the custom authentication verification failure page is displayed.   </div>
   

<span id="29214805"></span>
### Solution B

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ab6141b635541edab7cea45d39ef37c~tplv-goo7wpa0wc-image.image) </span>


1. A user logs in to your own account system on the system login page.

2. Your own account system calculates the signature using relevant parameters after having verified the user identity.

3. Add parameters `Sign`, `Nickname`, `UserId`, and`Timestamp`, as well as other parameters as authentication parameters to the viewing page address. For example, `https://live.byteplus.com/xxx/xxx?Sign=xx&Nickname=xx&UserId=xx&Timestamp=xxx`.

   You can also add the `Sign`, `Nickname`, `UserId`, and `Timestamp` parameters to your cookies. Then, the user can directly watch a live stream, send comments, and more after visiting the viewing page address.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If <code>extra</code> and <code>forceCheck</code> parameters are not necessary for you, ignore steps 4 to 6. If they are necessary for you, you must add them as authentication parameters to the viewing page address and then follow steps 4 to 6.   </div>
   

   The sample for adding parameters to your cookies is as follows.

   ```Plain
   Cookie: Sign=98d3e2f51c0a8a452be60484aed15ca0; Nickname=ZGFkYQ%3D%3D; Timestamp=1714307542226; UserId=222
   ```
   

4. The user visits the viewing page address with the preceding authentication parameters.

5. BytePlus Live verifies the signature (`Sign` value) according to the information in the authentication parameters to determine whether to allow the user to watch a live stream, send comments, and more.

6. If the verification is passed, that is, the signature calculated by BytePlus Live is the same as the `Sign` value in the authentication parameters, the user can then watch a live stream, send comments, and more.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the authentication type is set to <strong>Custom</strong> and the verification is not passed, the custom authentication verification failure page is displayed.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the comment restriction is set to <strong>Custom</strong> and the verification is not passed, the custom authentication verification failure page is not displayed. The user can watch live videos, previews, and playbacks on the viewing page without logging in to the live room, but cannot send comments or participate in interactive activities such as lucky draws.   </div>
   


<span id="ffe87359"></span>
## Parameters

<span id="5dc6dbef"></span>
### Redirect parameters

BytePlus Live carries the following parameters to redirect users from the viewing page to the login page of your own account system.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions#71eea3ee">Solution A</a> needs these parameters.</div>



|Name |Data type |Description |Sample value |
|---|---|---|---|
|ActivityId |Integer |The activity ID of the live room. |17475526787325 |
|Timestamp |Integer |The current time in Unix timestamp format. Unit: milliseconds. |1669808399000 |
|RedirectUrl |String |The authentication page address of BytePlus Live. On this page, BytePlus Live verifies the signature (`Sign` value) to determine whether to allow the user to watch a live stream, send comments, and more. |liveDomain/xxx/xxx |


<span id="40e48cc1"></span>
### Callback parameters


* [Solution A](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions#71eea3ee): Your own account system carries the following parameters to redirect users from the system login page to the authentication page of BytePlus Live.

* [Solution B](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions#29214805): You can add the following parameters as authentication parameters to the viewing page address.



|Name |Data type |Required |Description |Sample value |
|---|---|---|---|---|
|UserId |String |Yes |The unique identifier of the user in your own account system. This parameter is only used to associate your own account system with BytePlus Live, and is not used for data analysis.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend that you do not use information such as a phone number as the unique identifier of the user in your own account system to avoid personal information leakage.</div><br> |`14039` |
|Nickname |String |Yes |The nickname of the user in your own account system. You need to first UTF\-8 encode, then Base64 encode, and finally URL encode the nickname. For example, if the nickname is Employee😁 ABC, then the parameter value is `RW1wbG95ZWXwn5iBIEFCQw%3D%3D`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend that you do not use information such as a phone number as the nickname of the user in your own account system to avoid personal information leakage.</div><br> |`RW1wbG95ZWXwn5iBIEFCQw%3D%3D` |
|Timestamp |Integer |Yes |The current time in Unix timestamp format. Unit: milliseconds. |`1669808499000` |
|Sign |String |Yes |The signature for verification.<br><br>To get the `Sign` value, you must complete the following steps:<br><br><br>1. Concatenate a string in the `SecretKeyUserIdTimestamp` format. You can get the secret key on the BytePlus Live console. For more information, see [Procedure](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions#447f1c83).<br><br>2. Encrypt the concatenated string in MD5 (32\-bit lowercase).<br><br><br>In this example, assume that the `SecretKey` value is `h/macd/b/a`. The concatenated string would then be `h/macd/b/a140391669808499000`, with the `Sign` value as `2708f2f2969e38ff5d1863fde50e7b64`. |`2708f2f2969e38ff5d1863fde50e7b64` |
|extra |String |No |The extra parameter synchronized to BytePlus Live and can be used to associate with the user. For example, you can synchronize the user's department in your own account system to BytePlus Live. |`Sales department` |
|forceCheck |Boolean |No |Specifies whether to clear the last login status. Default value: `false`.<br><br><br>* `true`: Clears the last login status. This applies to scenarios where multiple users use the same browser or device. For example, if User A and User B visit the viewing page using the same browser on the same device. To ensure that they can visit the viewing page with their own identity, User B must log in to your own account system again after User A visits the viewing page.<br><br>* `false`: Does not clear the last login status. This applies to scenarios where each user uses their own browser or device. For example, if User A visits the viewing page multiple times using the same browser on the same device, they do not need to log in to your own account system again within the period when browser cookies are not cleared. |`true` |


<span id="447f1c83"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. On the left navigation pane, click **Producer** \> **Viewing restrictions**.

4. Set the authentication type or comment restriction to **Custom** and complete the following configurations.

   * Set the authentication type to **Custom**: Users must log in to your own account system before entering the live room to watch a live stream and more.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90c6142a0b3a4107add065e34f8b1053~tplv-goo7wpa0wc-image.image) </span>

   * Set the comment restriction to **Custom**: Users must log in to your own account system before sending comments or participating in interactive activities such as lucky draws.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df19b2bc674f42928af2d888ec04fe60~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You must set the authentication type to <strong>None</strong> before setting the comment restriction to <strong>Custom</strong>.      </div>
      

   
   |Configuration |Description |
   |---|---|
   |App for account login |The name of your own account system. |
   |Login link |The login page address of your own account system. The link must have a protocol header, such as `http://myDomain/auth`.<br><br><br>* Set the authentication type to **Custom**: BytePlus Live carries the `ActivityId`, `Timestamp`, and `RedirectUrl` parameters to redirect users to the link after they visit the viewing page.<br><br>* Set the comment restriction to **Custom**: BytePlus Live carries the `ActivityId`, `Timestamp`, and `RedirectUrl` parameters to redirect users to the link after they send comments or participate in interactive activities such as lucky draws.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions#29214805">Solution B</a>, users do not need to be redirected to the link.</div><br> |
   |Secret Key |After you enter the app for account login and login link, and then save the configurations, the secret key is automatically generated. The secret key is used to calculate the signature (`Sign` value). For how to calculate the signature, see [Callback parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions#40e48cc1). |
   |Full\-screen watermark |Specifies whether to display a user's nickname as the full\-screen watermark in the live room. |
   |Nickname modification |Specifies whether to allow users to modify their nicknames in the live room.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Users can only modify their nicknames once within a seven\-day period in the live room.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The modified nickname applies only to this live room.</div><br> |

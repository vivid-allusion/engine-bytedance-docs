---
title: "OAuth 2.0"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-oauth-2-0"
---

OAuth 2.0 can be used to allow users in your own account system to access multiple applications with one set of login credentials. With OAuth 2.0 set as the viewing restriction, users must log in to your own account system before entering the live room to perform actions such as watching live videos or sending comments.

<span id="1746671a"></span>
## Prerequisites


* A BytePlus account or an IAM user with Producer \> Edit permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

* Contact your sales representative to get the redirect URI. If you do not have a sales representative, click [here](https://www.byteplus.com/en/contact) to fill in the form so that the BytePlus sales team can contact you later.

* Complete the registration for BytePlus Live in your own account system. The redirect URI is required during the registration process. After the registration is complete, a client ID and a client secret are generated, which are used to identify BytePlus Live.


<span id="aa6a6a14"></span>
## Context

OAuth 2.0 is an open, standardized authorization protocol that allows third\-party applications to access user resources using tokens, without the need for usernames and passwords. In this topic, the third\-party application refers to BytePlus Live.

OAuth 2.0 defines the following four authorization grant types for getting tokens: Authorization Code Grant, Implicit Grant, Password Grant, and Client Credentials Grant. BytePlus Live uses the Authorization Code Grant, which involves requesting an authorization code first and then exchanging it for an access token. This grant type offers the highest level of security among all the authorization grant types. For more information about this grant type, see [Process](https://docs.byteplus.com/docs/byteplus-livesaas/docs-oauth-2-0#Process).

<span id="ae3f70e6"></span>
## Process

With the Authorization Code Grant, BytePlus Live can get user data from your own account system. The detailed process is as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e67a4a4a707e43cfa8a71c364a22bca8~tplv-goo7wpa0wc-image.image) </span>


1. Users access the viewing page of BytePlus Live via a link or QR code.

2. BytePlus Live requests an authorization code from the resource owner and provides the resource owner with the client ID and scope. Users are redirected to the login page of your own account system.

3. After users log in to your own account system, the resource owner returns the authorization code to BytePlus Live. Users are redirected to the redirect URI provided by the sales representative.

4. BytePlus Live proves its identity using the client ID and client secret and uses the authorization code to request an access token from your authorization server.

5. The authorization server verifies BytePlus Live's identity and the authorization code. After the verification is successful, the authorization server issues an access token to BytePlus Live.

6. BytePlus Live requests protected user data from your resource server and provides the access token for identity verification.

7. The resource server verifies the access token. After the verification is successful, the resource server provides the user data to BytePlus Live.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If a non\-standard OAuth 2.0 login mode is used, the authorization server will return the protected user data to BytePlus Live when the authorization server issues an access token in step 5.</div>


* <div data-tips="true" data-tips-type="tip">If a user's browser stores the login status of your own account system, the resource owner will directly return the authorization code to BytePlus Live after BytePlus Live requests an authorization code, without the need for the user to log in.</div>



<span id="aad845fb"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. On the left navigation pane, click **Producer** \> **Viewing restrictions**.

4. Set **OAuth2.0** as the authentication type and complete the following configurations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02cf75b685284b28982255c0eb737495~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter Name |Description |
   |---|---|
   |Login platform name |The platform name of your own account system. We recommend that you enter the name in English. |
   |Redirect URI |The callback address that receives the authorization code, which is the same as the authorization callback address entered when BytePlus Live is registered in your own account system. |
   |Authorization endpoint |The URL used to get the authorization code. |
   |Token endpoint |The URL used to get the access token. |
   |UserInfo endpoint |Select **URL** or **Identifier field**.<br><br><br>* **URL**: Enter the URL used to get user information.<br><br>* **Identifier field**: Enter the identifier field used to parse user information. Select this option if a non\-standard OAuth 2.0 login mode is used. BytePlus Live can get protected user data when the authorization server issues an access token to BytePlus Live. |
   |Username field |The field that corresponds to the username in your own account system, which is used to parse username.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To prevent the disclosure of personal information, do not use information such as phone numbers as usernames in your own account system.</div><br> |
   |User ID field |The field that corresponds to the user ID in your own account system, which is used to parse user ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To prevent the disclosure of personal information, do not use information such as phone numbers as user IDs in your own account system.</div><br> |
   |Client id |The client ID that identifies BytePlus Live, which is generated after BytePlus Live is registered in your own account system. |
   |Client secret |The client secret that identifies BytePlus Live, which is generated after BytePlus Live is registered in your own account system. |
   |Scope |The authorization scope. BytePlus Live can only access resources within the specified scope.<br><br>This parameter is required if the `Scope` does not have a default value in your own account system. |
   |Trial watch |Turn on the switch and select a duration. During the trial watch duration, viewers can watch live videos or playbacks without logging in to the live room. |

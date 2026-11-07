---
title: "Feishu user authentication and authorization"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Feishu_user_authentication_and_authorization"
---

The Alert Center of Observability Platform is deeply integrated with Feishu, allowing Feishu user authentication and authorization via the "BytePlus Observability Alerting" application and enabling the retrieval of user identities and group information. This makes it easy to configure notification settings quickly and accurately. This topic describes how to perform Feishu user authentication and authorization.

<span id="qzf8V7kd"></span>
## Background

Common scenarios for Feishu user authorization are as follows:


* Feishu user authentication and authorization are required when you associate a contact with a Feishu user.

* Feishu user authentication and authorization are required when you associate a Feishu application bot with a Feishu group.


<span id="beDUdNil"></span>
## Procedure

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The permission to use the "BytePlus Observability Alerting" application only needs to be obtained or requested once and remains permanently valid.</div>


<span id="SIyFf68K"></span>
### Step 1: Enterprise administrator obtains the application


1. Log in to your Feishu account as an enterprise administrator.

2. Search for **App Directory** in Feishu or visit the [Feishu App Directory](https://app.feishu.cn/all) directly in a browser to access it.

3. In the Feishu App Directory, search for **BytePlus Observability Alerting**. After you find the application, click **Get** to obtain permission to use the application.

4. Open the [Feishu admin console](https://ecnczee95qqe.feishu.cn/admin/appCenter/manage/cli_a68c28beb273900b?lang=zh-CN) and configure application permissions for the **BytePlus Observability Alerting** application bot. Add member accounts under **Contact Data Scope Covered by the Preceding Permissions**. Accounts with the permission can view operator information when receiving alert notifications.


<span id="sm6Epl40"></span>
### Step 2: Enterprise employee requests access to the application


1. Log in to your Feishu account as an enterprise employee.

2. Search for **App Directory** in Feishu or visit the [Feishu App Directory](https://app.feishu.cn/all) directly in a browser to access it.

3. In the Feishu App Directory, search for **BytePlus Observability Alerting**. After you find the application, click **Request Access** and wait for the administrator to approve the request.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you cannot find the application bot, or cannot request access after finding it, contact your Feishu administrator.   </div>
   

<span id="zdX5qr7j"></span>
### Step 3: Feishu user authentication and authorization


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In scenarios that require Feishu configuration, such as contact or callback URL creation, click **To authorize** in the prompt to be redirected to the authorization page.

3. Verify that the account and permissions to be granted are correct, and then click **Authorize** in the lower\-right corner to complete Feishu user authentication and authorization.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After the authorization is complete, you can go to <a href="https://accounts.feishu.cn/accounts/security/page/apply_authorization">App authorization management</a> to cancel the authorization based on your needs.   </div>

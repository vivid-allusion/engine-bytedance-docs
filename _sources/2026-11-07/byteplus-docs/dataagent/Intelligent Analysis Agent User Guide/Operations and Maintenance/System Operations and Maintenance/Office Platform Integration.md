---
title: "Office Platform Integration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Office_Platform_Integration"
---

<span id="7bc38e87"></span>
# 1. Overview

The product provides office platform integration functionality, allowing enterprise domain administrators to configure application integration and email service settings for scenarios such as message notifications, alarm subscriptions, and connecting to Lark data sources. This article introduces office platform integration for private deployment.

**Common application scenarios**

Provides office platform application configuration capabilities, enabling users to configure settings autonomously based on their application scenarios and the supported features of the office platform. After configuring the office platform, the following features can be enabled:


* Message notifications for dataset synchronization SLA alarms

* Message notifications for project authorization\-related notifications

* Enable Lark documents as a data source to create datasets

* Lark mobile app


<span id="1f3ae32d"></span>
# 2. Quick start

 **(1) SaaS version**

**Step 1:**  The enterprise domain administrator goes to the enterprise domain management page, clicks the [Office Platform] tab on the left, and fills in the relevant enterprise IM configuration items.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e61f8f70a0224d1dae121693dd4a3c58~tplv-goo7wpa0wc-image.image) </span>

**Step 2:**  After completing the configuration, perform a configuration test and click Submit to save the settings. For details on each enterprise IM configuration item, see "3. Feature introduction."

 **(2) Private deployment version**

**Step 1:**  Click the avatar in the upper right corner of the product interface, then select System Management, which is the BytePlus Console (Portal).

**Step 2:**  Click Office Platform and fill in the relevant enterprise IM configuration items. For details on each enterprise IM configuration item, see "3. Feature introduction."

<span id="13440156"></span>
# 3. Feature introduction

<span id="f8518b01"></span>
## 3.1 Email service

 **(1) Common application scenarios**


* Allows individual users to use the enterprise email for password recovery and reset.

* When an account is created, the account information and password are automatically sent via email notification.

* Subscribe to product messages and send them to designated users of the enterprise email.


 **(2) Basic configuration**

You can go to the office platform page, click "Connect new platform," select "Enterprise Email," and complete the following configuration:


* Platform logo: You can use the default logo. Clicking the default logo also allows you to upload a custom local logo.

* Platform name: You can use the default platform name or modify it.

* Email server: Please enter the email server address using the SMTP protocol.

* Port number: Enter the port number

* Encryption protocol: Supports no encryption, and also allows selection of the mail server's TLS or SSL encryption protocol

* Allowlist management: Enter email suffixes with @; supports multiple groups, separated by commas

* Enable status: Enabled by default; to disable, configure here


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b7ba41cb78e4d9cb9f3b3fa85b1231b~tplv-goo7wpa0wc-image.image) </span>

 **(3) Message sending**

After configuration, product subscription information can be sent to designated users via email.


* Sender email address: Enter the sender address; subscription product information will be sent via this address

* Username: Enter the username for logging in to the sender email address

* Authorization code/password: Enter the authorization code or password for logging in to the sender email address

* Sender alias: This field is optional.

* Available products: The selected products can use this sending channel.

* Test recipient email address: Enter a test email address

* Verification code: Enter the verification code received by the test recipient to ensure that this sending channel is available.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73b72c0fedcb4136835d0ac43c2ac6dc~tplv-goo7wpa0wc-image.image) </span>

Caution

Enabling email services requires the customer's network environment to support network connectivity.

<span id="018d94c9"></span>
## 3.2 WeCom

On the office platform page, click "Connect new platform" and select "WeCom", then complete the following configuration:


* Platform logo: You can use the default WeCom logo; clicking the default logo also allows uploading a custom local logo

* Platform name: You can use the default platform name or modify it


**Required**


* Corp ID

* Corp Secert

* Agent ID

* Enable status: Enabled by default; to disable, configure here


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12e53bee846e45f4a9c8e5dc5e21780d~tplv-goo7wpa0wc-image.image) </span>

Agent ID (application ID) and Secret (key) can be obtained as shown in the following diagram.

Company ID (enterprise ID) can be obtained as shown in the following diagram.

<span id="969ec4d9"></span>
## 3.3 Feishu

On the office platform page, click "Connect new platform" and select "Feishu", then complete the following configuration:


* Platform logo: You can use the default Feishu logo; clicking the default logo also allows uploading a custom local logo

* Platform name: You can use the default platform name or modify it


**Required**


* App ID: Application ID

* App Secret: Application authorization code

* Enable status: Enabled by default; to disable, configure here


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85d5a6ad7bd745fbb0453fc2d5452596~tplv-goo7wpa0wc-image.image) </span>

<span id="8fe230d7"></span>
## 3.4 DingTalk

On the office platform page, click "Connect to a new platform," select "DingTalk," and complete the following configuration:


* Platform logo: You can use the default DingTalk logo. Clicking the default logo also allows you to upload a custom local logo.

* Platform name: You can use the default platform name or modify it as needed.


**Required**


* Agent ID: When creating an application, the system automatically generates an Agent ID, which can be used for scenarios such as sending enterprise conversation messages.

* App Key: When creating an application, the system automatically assigns a pair of AppKey and AppSecret. The AppKey is the unique identifier during application development.

* App Secret: When creating an application, the system automatically assigns a pair of AppKey and AppSecret. Use the AppKey and AppSecret to obtain the access_token.

* Status: Enabled by default. To disable, configure here.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e86ce1a2f3248598e632c572ac385ec~tplv-goo7wpa0wc-image.image) </span>

<span id="686bdfea"></span>
## 3.5 WebEx

**Required**


* Access Token

* Status: Enabled by default. To disable, configure here.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc6235c4d0c749ee84efbd9a7c3abc17~tplv-goo7wpa0wc-image.image) </span>

Access Token: The BOT's access token.

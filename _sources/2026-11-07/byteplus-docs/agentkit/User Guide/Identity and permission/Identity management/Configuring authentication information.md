---
title: "Configuring authentication information"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/configure-authentication-information"
---

Authentication configuration determines which credentials users can use to access your application. You can configure the login method and registration method separately.

## Prerequisites

* A user pool has been created. For related operations, see [Creating user pools](https://docs.byteplus.com/en/docs/agentkit/create-user-pool).

* To use the SMS service configuration, you must create a message group for sending SMS messages in advance. For related operations, see [Adding message groups](https://docs.byteplus.com/en/docs/byteplus-sms/docs-creating-a-message-group).

* To configure a hook function, you need to create an HTTP/S event function in veFaaS in advance. For related operations, see [Creating event functions](https://docs.byteplus.com/en/docs/faas/Creating_event_functions).

## Procedure

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, click "Identity and Permission" \> "User pool management". On the page that appears, click the name of the target user pool.

3. On the user pool details page, switch to the "Identity authentication" tab.

4. Specify authentication\-related parameters.

   * **SMS configuration**: Configure the SMS channel that the user pool uses to send SMS verification codes.

      > **warning**

      > Using the SMS service incurs corresponding fees. For details, see [SMS pricing](https://docs.byteplus.com/en/docs/byteplus-sms/docs-pricing).

      |SMS configuration |Description |
      |---|---|
      |SMS channel/provider |Select which SMS sending link this user pool uses. Currently, only the platform built\-in SMS service channel, "BytePlus \- SMS service", is supported, which is suitable for production environments with large sending volumes and provides high availability. |
      |Applicable regions |Regions where the SMS service is applicable:<br><br><br>* **Regions in the Chinese mainland**: Sends SMS messages to the Chinese mainland.<br><br>* **Regions outside the Chinese mainland**: Sends SMS messages to regions outside the Chinese mainland. |
      |Message group |Message groups are mainly used for resource isolation. You can use different message groups to distinguish SMS types and business lines. Signatures, templates, and sending data are isolated among different message groups.<br><br>Select the message group prepared that is described in Prerequisites. If no message groups are available, create a message group.  For related operations, see [Adding message groups](https://docs.byteplus.com/en/docs/byteplus-sms/docs-creating-a-message-group). |
      |SMS signature |You need to configure an SMS signature for SMS messages sent to the Chinese mainland. The SMS signature is the signature placed in `【】` before the SMS body and identifies the company or business. For related operations, see  [Statistics](https://docs.byteplus.com/en/docs/byteplus-sms/Statistics). |
      |Sender |You need to configure a sender for SMS messages sent to regions outside the Chinese mainland. It is similar to the SMS signature. Enter the sender of the SMS message, such as the sender company name. |

   * **Login method management**: Configure which methods users can use to log in to your application.

      |Login method |Description |
      |---|---|
      |Log in via password |Logging in via password is the most fundamental login method. Users can log in using "username/mobile number/email address + password". To ensure the basic availability of the account system, it is enabled by default and cannot be disabled.<br><br>> **tip**<br><br><br>> "Log in via password" is enabled by default and cannot be manually disabled. Contact the administrator if you need to disable it.<br> |
      |Log in via SMS verification code |AgentKit enables SMS verification code login by default. After this feature is enabled, users can log in by entering their mobile number and receiving a verification code (password\-free). |

   * **Registration management**: Control how new users enter your application ecosystem.

      |Registration method |Description |
      |---|---|
      |Self\-registration |* **When enabled**: Public application. Any visitor who accesses the login page can create an account.<br><br>* **When disabled**: Closed application. The login page hides the registration entry. An administrator must manually create users in a **user pool** in the AgentKit console or import them through an API. |
      |Automatic verification during registration |The automatic registration verification feature is mainly used to verify whether the target mobile number is used by the registrant. This prevents attackers from registering in bulk with random mobile numbers or the mobile numbers of other people, effectively reducing bot registrations.<br><br>After you enable automatic registration verification, a new user must receive an SMS verification code and enter the correct code during registration to register successfully.<br><br>> **tip**<br><br><br>> To enable automatic registration verification, you need to configure the SMS service.<br> |

   * **Password management**: Configure password recovery capabilities.

      |Parameter |Description |
      |---|---|
      |Recover password via SMS |After "Recover password via SMS" is enabled, users can click "Forgot password" on the login page, verify their identity via a verification code sent to their mobile number or email address, and then set a new password themselves without contacting an administrator.<br><br>> **tip**<br><br><br><br>* > To enable "Recover password via SMS", you need to configure the SMS service.<br><br><br>* > Make sure that the user account is linked to a mobile number or email address for password recovery.<br><br><br>* > If "Log in via password" is enabled, we recommend enabling "Recover password via SMS". Otherwise, users who forget their passwords can only ask the administrator to reset their passwords, resulting in high operational costs.<br> |

   * **Extension capability**: Configure more authentication extension capabilities for the user pool.

      |Extension capability |Description |
      |---|---|
      |Hook function management |A hook function is a piece of custom code attached to the user authentication flow. When a user registers, logs in, or is about to be issued a token, AgentKit synchronously calls your function. This helps you implement capabilities beyond the standard product features.<br><br><br>* **Capability**:<br><br>   * Dynamically add claims: After a user logs in, the hook function queries the HR system or CRM of your company for the department, role, and membership level of the user in real time, and writes them into the ID Token or Access Token. Downstream agents can directly use these fields for permission decisions.<br><br>   * Login risk control: Based on the login IP, device fingerprint, historical behavior, and risk control engine, the hook function directly denies token issuance to high\-risk users.<br><br>   * Login audit: The hook function records an event in your own logging platform/SIEM on every login/token issuance.<br><br>   * Protocol and field conversion: The hook function changes the names, formats, and values for claims as required by downstream systems.<br><br>* **Configuration procedure**:<br><br>   1. Create an event function in the [Function Service Console](https://console.byteplus.com/vefaas), and select a language you are familiar with, such as Node.js, Python, and Go. For related operations, see [Creating event functions](https://docs.byteplus.com/en/docs/faas/Creating_event_functions).<br><br>   2. Configure an **APIG trigger** for the function to obtain a publicly accessible HTTPS endpoint. For related operations, see [Creating APIG triggers](https://docs.byteplus.com/en/docs/faas/Creating_a_API_Gateway_trigger).<br><br>   3. On the "Identity authentication" tab of the target user pool in the [AgentKit console](https://console.byteplus.com/agentkit), click Add hook function, select the hook function type, select the event function created in veFaaS, and save the configuration. |

## Recommended configuration combinations

|**Scenarios** |**Self\-registration** |**Log in via SMS verification code** |**Other suggestions** |
|---|---|---|---|
|Internal employees (integrated with enterprise SSO such as Feishu and DingTalk) |Disable |Disable |* Accounts are automatically created through SSO.<br><br>* Password login is retained as a fallback.<br><br>* Password recovery can be enabled. |
|External partner/supplier |Disabled (registered by administrators) |Optional |* Use a separate user pool for isolation.<br><br>* Bind IAM roles and authorize by group. |
|B2C product user |Enable |Enable |* Automatic verification during registration must be enabled.<br><br>* We recommend enabling the password recovery feature.<br><br>* You can attach a Pre\-Token Hook to inject membership levels. |
|POC/Testing |Optional |Optional |The SMS service can be omitted to reduce SMS\-related costs. |

---
title: "Managing user information masking"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Managing_user_information_masking"
---

In the ‌Users module of the ArkClaw console, sensitive fields such as email and phone numbers are ‌displayed in plain text by default. Enterprise administrators may enable the ‌masking toggle‌ to prevent direct exposure of this information. If this feature is enabled, sensitive fields will appear in masked format on both list and detail pages. Administrators can click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_82f91926b31905ac56810d38017fc446.png) </span> icon to view unmasked data for individual users on demand. All sensitive data access events are recorded in ‌audit logs‌ for post\-incident tracing.

This topic explains how to enable or disable the user information masking toggle and view sensitive data for individual users.

<span id="3H9cfB5Q"></span>
## Scenarios


* Clients with strict data security requirements seeking to prevent direct exposure of user contact details.

* Organizations where multiple accounts or IAM users can access the ArkClaw console need to restrict control over plaintext display of sensitive user information to a few administrators, preventing regular users from toggling the setting and weakening sensitive data protection.


<span id="fjuVftn4"></span>
## Enable or disable user information masking

<span id="bmOP6qAG"></span>
### Prerequisites

Only **BytePlus root users** or authorized IAM users can enable or disable this configuration. To attach a custom permission policy to grant feature access, see [Authorizing IAM users to use the ArkClaw user information masking feature](https://docs.byteplus.com/en/docs/ArkClaw/Authorizing_IAM_users_to_use_ArkClaw_user_information_masking).

<span id="zTDx6Zkc"></span>
### Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. In the upper\-right corner of the page, click "Masking" to enable or disable it. This controls whether sensitive fields such as email and phone numbers appear in masked or plaintext format across user list and detail pages.


<span id="q4MYa7Mh"></span>
## View **plaintext sensitive user information**

‌When user information is displayed in masked format, accessing plaintext sensitive information requires no additional authorization. However, for security traceability, all plaintext access operations are recorded in ArkClaw audit logs.

<span id="f1yiqXa5"></span>
### Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. To the right of the masked field, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_82f91926b31905ac56810d38017fc446.png) </span> icon to view the plaintext of the sensitive user information.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">‌Viewing plaintext sensitive user information will be recorded in audit logs. For more information, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_audit_logs">Viewing ArkClaw audit logs</a>.   </div>

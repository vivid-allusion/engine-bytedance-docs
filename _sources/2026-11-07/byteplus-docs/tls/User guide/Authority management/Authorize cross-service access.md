---
title: "Authorize cross-service access"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Authorizing_cross-service_access"
---

Torch Log Service (TLS) can play the ServiceRoleForTLS role to achieve cross\-service access to other cloud service resources. This topic describes how to grant permissions to allow TLS to access other BytePlus services.

<span id="dd4b2e1d"></span>
## Background

A corresponding service role is an IAM role that a trusted entity uses for BytePlus services, aiming to solve cross\-service authorization access issues. The ServiceRoleForTLS role in TLS is a corresponding service role with a series of preset permission policies, allowing TLS to access specified cloud service resources under your account. For example, when using the TLS shipping function, TLS will play the ServiceRoleForTLS role to access TOS and obtain information such as the TOS bucket list.

<span id="注意事项"></span>
## Precautions


* After you grant the permissions on a BytePlus service to TLS, TLS can access the service resources until you revoke the permissions by removing the corresponding service role.

* The permissions of a service role are delegated by the system, and you cannot modify the permissions. If you want to revoke the permissions, remove the service role.

* Functions such as scheduled SQL analysis tasks, subscription dashboards, and TOS shipping all involve the authorization of the ServiceRoleForTLS role. Once you create the ServiceRoleForTLS role in any function module, other function modules do not need to create it again.

* We recommend that you use the credentials of your BytePlus account to grant cross\-service access permissions.

   If you use the credentials of an IAM user to grant cross\-service access permissions, attach the IAMFullAccess system policy to the IAM user before you use it. For more information, refer to the documentation of [Identity and Access Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3).


<span id="操作步骤"></span>
## Procedure

This topic takes the creation of the ServiceRoleForTLS role on the TLS shipping page as an example.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Data processing** \> **Log shipping**.

3. On the **Log shipping** Page, click **Create TOS shipping configuration**.

4. On the **Cross\-service access request** page, confirm the information about the service role and the trust relationship, then click **Authorize Now**.

   After you grant cross\-service permissions to an IAM user, you can view the added service role ServiceRoleForTLS in the IAM role list.

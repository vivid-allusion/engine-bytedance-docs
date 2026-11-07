---
title: "Root user permission management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/managing-permissions-of-a-main-account"
---

After successfully registering a BytePlus account, when you first use Database Workshop DBW, you need to grant DBW access to other cloud service resources to ensure normal functionality within DBW. This topic describes the procedure to authorize Database Workshop (DBW) to access other cloud service resources.

<span id="vFNVSxQg"></span>
## Prerequisites

A BytePlus account has been registered with real name authentication completed.    

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. In the left navigation bar, click **Operations observability**.

3. On the **Cross\-service access request** page, click **Authorize now** to allow Database Workshop DBW to access other cloud service resources under your account.

   Authorized successfully, the system will create a role `ServiceRoleForDbw` for you by default. You can Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user) and view the role on the **Role** page. The policy syntax in this role is as follows:

   ```json
           {
         "Statement": [
           {
             "Effect": "Allow",
             "Action": [
               "Volc_Observe:GetMetricData",
               "Volc_Observe:CreateRule",
               "Volc_Observe:DeleteRulesByIds",
               "Volc_Observe:UpdateRule",
               "Volc_Observe:ListRulesByIds"
             ],
             "Resource": [
               "*"
             ]
           }
         ]
       }
   ```
   


<span id=".5o6I5p2D5pWw5o2u5bqT5bel5L2c5Y-wLWRidy3orr_pl67ml6Xlv5fmnI3liqEtdGxz"></span>
## Authorize Database Workshop (DBW) to access Torch Log service (TLS)

When using the audit log feature of DBW for the first time, since the storage of audit logs is provided and billed by BytePlus's Torch Log Service (TLS), you also need to authorize DBW to access TLS.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the **Observation and Diagnosis** page, click **Audit Log**.

4. On the **Audit Log** tab, click **Click Authorize** to grant Database Workshop DBW access to Torch Log Service TLS.

5. In the **Are you sure to authorization?**  dialog box, click **OK**.

   After authorized successfully, the system will default create a role named `DBWAuditLogArchiveTLSRole`. You can Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user) and view the role on the **Role** page. The policy syntax in this role is as follows:

   ```json
   {
     "Statement": [
       {
         "Effect": "Allow",
         "Action": [
           "tls:*"
         ],
         "Resource": [
           "*"
         ]
       }
     ]
   }
   ```

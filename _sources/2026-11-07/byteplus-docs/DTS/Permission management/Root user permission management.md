---
title: "Root user permission management"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/primary_account_permission_management"
---

After successfully registering a Volcanic Engine account, you need to grant DTS permission to access other cloud service resources when using the Database Transmission Service (DTS) to ensure full functionality. This topic describes the steps for authorizing DTS to access other cloud service resources.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A BytePlus account has been registered with real name authentication completed. For more information, refer to [Create account](https://docs.byteplus.com/en/docs/6261/64925) and [Verify account](https://docs.byteplus.com/en/docs/6261/64935).

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

During data transmission, DTS requires access to other cloud resources. To simplify your authorization, DTS provides a default system role called `ServiceRoleForDTS`. This role allows DTS to access other service resources under your account. When using DTS for the first time, you need to bind this role to your account as prompted.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The permissions included in the `ServiceRoleForDTS` role are coarse\-grained. If you need more fine\-grained permissions, you can grant the account other roles and related permission policies.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. In the left navigation bar, click **Data migration**, **Data subscription**, or **Data synchronization**.

3. On the **Data migration list**, **Data subscription list**, or **Data synchronization list** page, click **Create task**.

4. On the **Cross\-service access request** page, click **Authorize now** to grant DTS access to other cloud service resources under your account.


After the authorization succeeds, the system automatically creates a role for you named `ServiceRoleForDTS`. You can log on to the [IAM](https://console.byteplus.com/iam/identitymanage/user) console and view the role on the **Roles** page. The trust policy syntax within the role is as follows:

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "sts:AssumeRole"
            ],
            "Principal": {
                "Service": [
                    "dts"
                ]
            }
        }
    ]
}
```

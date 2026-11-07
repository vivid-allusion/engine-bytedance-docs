---
title: "Client IAM permission management"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Client_IAM_permission_management"
---

RUM provides permission management based on IAM (Identity and Access Management) to control the access of different identities.

## Background

The  IAM service provides fine\-grained access control capabilities for resources. You can log in as a  root user to create IAM users and assign them permission policies to enable multi\-user collaboration or secure access in various scenarios. For example, O&M personnel have permission to manage all resources, while operations personnel have permission to view specified resources.

## Prerequisites

* An IAM user has been created.

* (Optional) If you apply a custom authorization policy, you can go to the RUM management page to obtain the resource ID of each client in the target application.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a4f027bbcd56ce3c445d85aa590bcf87.png)

## Limits

Currently, RUM provides two authorization management systems: IAM and self\-built permission management. **IAM is recommended**. In addition, a single user is subject to only one permission system, and IAM takes precedence over self\-built permission management. For example, if two sets of permission settings are configured for the same user at the same time, only the IAM takes effect.

## System preset policies

RUM provides the following system preset policies, which can be used to directly authorize IAM users.

|**Policy** |**Description** |Project\-level authorization |
|---|---|---|
|APMPlusClientFullAccess |APMPlus \- Full RUM permissions. |Supported |

You can refer to the following steps to authorize IAM users using system preset policies:

1. Log in to the [IAM console](https://console.byteplus.com/iam), and in the left navigation pane, select **User management** \> **User**.

2. In the **User list**, click **Add permission** in the **Actions** column on the right of the target IAM user.

3. Configure the authorization as needed. After completion, click **Submit** to finish the authorization.

|Parameter |Description |
|---|---|
|Identity |Displays information about users to be authorized. |
|Policy |Select authorization policies as needed. You can filter by policy type, associated service, policy name, or remarks. |
|Limit to project resources |Whether the permissions take effect when accessing resources within the project.  .<br><br><br>* **No** (default): does not grant permissions by project. When you select this option, authorization takes effect globally.<br><br>* **Yes**: grants permissions by project. When you select this option, you need to specify projects to which the authorization applies. |

## User custom policies

The Actions and Resources supported by RUM are as follows.

> **tip**

* > The Resource element contains the resource scope defined by the permission statement. It is defined using a TRN expression and consists of information such as service, region, account, and resource path. The format is `trn:{service}:{region}:{account}:{resourceType}/{id}`.

* > In RUM, `{id}` represents the resource ID, which is the resource ID for each client in the application. You go to the RUM management page to obtain it, as described in the prerequisites.

|**Action** |**Resource** |**Description** |
|---|---|---|
|AppCreate |trn:apmplus:{region}:{account}:monitor/{resourceid} |Create an application and activate the client. |
|AppEdit |trn:apmplus:{region}:{account}:monitor/{resourceid} |Edit application\-related information, such as icon and name. |
|AppDelete |trn:apmplus:{region}:{account}:monitor/{resourceid} |Delete applications and client. |
|SDKConfig |trn:apmplus:{region}:{account}:monitor/{resourceid} |Reporting configurations, such as SDK reporting configuration for apps, project settings for WebPro, project settings for Mini Pro, and project settings for different RUM differentiated by parameters. |
|RequestConfig |trn:apmplus:{region}:{account}:monitor/{resourceid} |Request settings. |
|BuyAndSeviceOpen |trn:apmplus:{region}:{account}:monitor/{resourceid} |Purchase resource packages and activate pay\-as\-you\-go permissions. |
|OpenPostPaid |trn:apmplus:{region}:{account}:monitor/{resourceid} |Enable automatic switch to pay\-as\-you\-go. If enabled, the service will automatically switch to pay\-as\-you\-go after the resource package is exhausted or expires. The service will not be suspended. |
|DataCollectorSwitch |trn:apmplus:{region}:{account}:monitor/{resourceid} |Pause/restart data reporting. |

You can follow the steps below to create a custom policy and authorize IAM users:

1. Log in to the [IAM console](https://console.byteplus.com/iam). In the left navigation pane, select **Permission policy**.

2. Click **Create custom policy** and switch to the **JSON editor** tab. Set the policy name and policy content, and click **Submit**.

    A JSON example of a RUM custom policy is shown below. You can add or remove Action and Resource as needed.

   ```JSON
   {
     "Statement": [
       {
         "Effect": "Deny",
         "Action": [
           "apmplus:AppCreate",
           "apmplus:AppEdit",
           "apmplus:AppDelete",
           "apmplus:SDKConfig",
           "apmplus:RequestConfig",
           "apmplus:BuyAndSeviceOpen",
           "apmplus:OpenPostPaid",
           "apmplus:DataCollectorSwitch"
         ],
         "Resource": [
           "trn:apmplus:cn-beijing:0000000000:monitor/bj-000000-*"
         ]
       }
     ]
   }
   ```

3. Return to the **Permission policy** page, filter the newly created custom policy, and click **Authorize** in the Actions column on the right side of the policy.

4. Configure the authorization according to actual needs. After completion, click **Submit** to finish the authorization.

|Parameter |Description |
|---|---|
|Policy |Displays the custom policies to be authorized. |
|Limit to project resources |Whether the permissions take effect when accessing resources within the project.  .<br><br><br>* **No** (default): does not grant permissions by project. When you select this option, authorization takes effect globally.<br><br>* **Yes**: grants permissions by project. When you select this option, you need to specify projects to which the authorization applies. |
|Identity |Select authorization identities as needed. Provides 3 authorization methods: user, user group, and role. It also supports filtering by identity name, display name, or remarks. |

## Validate results

Log in to the RUM console as an IAM user with the configured permissions. Under normal circumstances, the authorized operations can be performed without errors. Unauthorized operations will be denied and will cause an error due to insufficient permissions.

---
title: "Configuring IAM policies"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-configuring-an-iam-policy"
---

This topic describes how to customize an Identity and Access Management (IAM) policy.

<span id="e8b5045e"></span>
## Background


* For more information about policies and scenarios, see [Overview](https://docs.byteplus.com/tos/docs/overview_6?version=1.0.0).

* For more information about operations, see [Supported actions](https://docs.byteplus.com/en/docs/tos/docs-overview_6#be435332).


<span id="b44eacd5"></span>
## Procedure


1. Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user).

2. In the left navigation pane, click **Policy management**.

3. On the **Policy management** page, click the **Create Policy**.

4. In the pop\-up dialog box, set the following policy parameters.

   * Basic policy information

   
   |**Parameter** |**Required** |**Description** |**Example** |
   |---|---|---|---|
   |Policy name |Yes |A policy name must conform to the following rules:<br><br><br>* It can contain letters, digits, and the following symbols: `+ = , . @ - \ _`.<br><br>* It must contain 1\-64 characters. |TOStest |
   |Description |No |The description must conform to the following rules:<br><br><br>* It can contain Chinese characters, letters, digits, and special characters.<br><br>* It must contain 0\-128 characters. |test |
   

   * Policy parameters

   
   |**Parameter** |**Required** |**Description** |**Example** |
   |---|---|---|---|
   |Version |No |The version number, which is **1.0** by default. |```Plain```<br>```"Version": "1.0"```<br> |
   |Statement |Yes |The authorization information about the policy, which contains **Effect**, **Action**, and **Resource**. |```Plain```<br>```{ "Statement": [```<br>```        {```<br>```            "Effect": "Allow",```<br>```            "Action": [```<br>```                "tos:List*"```<br>```            ],```<br>```            "Resource": [```<br>```                "trn:tos:::bucket"```<br>```      ]```<br>```        }```<br>```    ]```<br>```    }```<br> |
   |Effect |Yes |Specifies whether to allow or deny an operation. Valid values:<br><br><br>* **Allow**<br><br>* **Deny** |```Plain```<br>```"Effect": "Allow"```<br> |
   |Action |Yes |The list of operations allowed or denied by the policy. For more information about the list of operations supported by Torch Object Storage (TOS), see [Supported actions](https://docs.byteplus.com/en/docs/tos/docs-overview_6#be435332).<br><br><br>* It is a case\-insensitive string in the format of `"Action":["tos:Action name"]`.<br><br>* The wildcard asterisk ( `*` ) is supported, indicating all operations that can be performed on the resource. For example, `"Action":["tos:List*"]`. |```Plain```<br>```"Action": ["tos:List*"]```<br> |
   |Resource |No |The list of resources on which specified operations can be performed. If this parameter is not specified, no resource can be manipulated.<br><br><br>* It is a case\-insensitive string in the format of `"Resource": ["trn:tos:::{BucketName}/{ObjectName}"]`.<br><br>* To manipulate a bucket, specify the bucket name only, for example, `"Resource": ["trn:tos:::{BucketName}"]`.<br><br>* To manipulate objects in a bucket, specify the objects, for example, `"Resource": ["trn:tos:::{BucketName}/{ObjectName}"]`.<br><br>* You can use the wildcard asterisk ( `*` ) to indicate all buckets or objects. |```Plain```<br>```"Resource": [```<br>```        "trn:tos:::bucket/*",```<br>```        "trn:tos:::bucket",```<br>```        "trn:tos:::bucket*/*"```<br>```      ]```<br> |
   

5. Then, click **Submit**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When granting account or role permissions using IAM, it is expected to wait for 1 minute for the changes to take effect.   </div>
   

<span id="1f44fe65"></span>
## Further operations


* **Managing an IAM policy**: On the **Policy management** tab, click **Authorization** in the **Actions** column of the target policy to view its details or modify its name and description.

* **Editing an IAM policy**: On the **Policy management** tab, click **Edit** in the **Actions** column to modify the policy name and content.

* **Deleting an IAM policy**: On the **Policy management** tab, click **Delete** in the **Actions** column of the target policy and click **Delete** in the pop\-up dialog box.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Deleting a policy will invalidate the policy. Proceed with caution.   </div>

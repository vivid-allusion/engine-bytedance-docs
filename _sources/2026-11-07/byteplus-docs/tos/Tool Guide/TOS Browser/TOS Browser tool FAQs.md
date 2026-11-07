---
title: "TOS Browser tool FAQs"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Tos-browser-tool-faq"
---

This article introduces common issues encountered when using the TOS Browser tool.

<span id=".aWFtLeeUqOaIt--8iOWtkOi0puWPt--8ieeZu-W9lS10b3MtYnJvd3Nlci3miYDpnIDopoHnmoTmnIDlsI_mnYPpmZDmmK_ku4DkuYjvvJ8="></span>
## What are the minimum permissions required for an IAM user (sub\-account) to log in to TOS Browser?

The minimum permissions for an IAM user logging in to TOS Browser include basic object operations such as uploading and downloading objects, as well as bucket query operations. The specific permission policy content is as follows:

```Plain Text
{
        "Statement": [{
                "Effect": "Allow",
                "Action": [
                        "tos:GetObject",
                        "tos:PutObject",
                        "tos:DeleteObject",
                        "tos:GetObjectAcl",
                        "tos:PutObjectAcl",
                        "tos:GetObjectVersion",
                        "tos:DeleteObjectVersion",
                        "tos:AbortMultipartUpload",
                        "tos:ListMultipartUploadParts",
                        "tos:ListBucket",
                        "tos:HeadBucket",
                        "tos:ListBuckets",
                        "tos:ListBucketVersions",
                        "tos:GetBucketVersioning"
                ],
                "Resource": [
                        "*"
                ]
        }]
}
```


You can add more actions based on the above permission policy to grant the IAM user additional permissions according to your actual needs. For supported actions in IAM policies, please refer to [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

After confirming the permissions to grant, you need to use the [IAM Console](https://console.byteplus.com/iam/) to create a custom policy with the permission policy and then assign the policy to the IAM user. For detailed steps, see [Configure IAM Policy](https://docs.byteplus.com/docs/tos/docs-configuring-an-iam-policy) .

<span id=".d2luZG93cy3ns7vnu5_kuIvvvIzkvb_nlKgtdG9zLWJyb3dzZXIt5peg5rOV5q2j5bi45ouW5ou95paH5Lu25oiW5paH5Lu25aS577yM5ouW5ou95pe25Ye6546w56aB5q2i5Zu-5qCH5piv5LuA5LmI5Y6f5Zug77yf"></span>
## Why does dragging files or folders fail with a prohibited icon in TOS Browser on Windows?

On Windows, running TOS Browser with administrator privileges prevents file drag\-and\-drop; please run TOS Browser with standard user privileges.

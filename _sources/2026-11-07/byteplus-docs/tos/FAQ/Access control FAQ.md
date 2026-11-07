---
title: "Access control FAQ"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Permission-configuration"
---

###

|Category |FAQ |
|---|---|
|Bucket policy |* [How to configure bucket policy? Does the JSON configuration passed through the interface seem incorrect?](https://docs.byteplus.com/en/docs/tos/Permission-configuration?lang=en#3jkP42L4)<br><br>* [What is the relationship between bucket policies and access control lists (ACLs) for buckets and objects? Can they coexist?](https://docs.byteplus.com/en/docs/tos/Permission-configuration?lang=en#sDVCCmle)<br><br>* [Does TOS support granting permissions to a specific directory inside a bucket?](https://docs.byteplus.com/en/docs/tos/Permission-configuration?lang=en#rLEKNwEt)<br><br>* [How can I view the permissions for an existing bucket?](https://docs.byteplus.com/en/docs/tos/Permission-configuration?lang=en#KbvbOvOr) |
|IAM policy |* [How can I give an IAM user permission to view only a specific bucket?](https://docs.byteplus.com/en/docs/tos/Permission-configuration?lang=en#0KwXFs9Z)<br><br>* [How can I grant an IAM user permissions for cross-region replication?](https://docs.byteplus.com/en/docs/tos/Permission-configuration?lang=en#Rwud56KT)<br><br>* [If I skip configuring role permissions when creating an IAM role, does IAM assign default permissions to the role?](https://docs.byteplus.com/en/docs/tos/Permission-configuration?lang=en#i5M7aMZ7) |
|ACL |[How can I make a private bucket publicly readable?](https://docs.byteplus.com/en/docs/tos/Permission-configuration?lang=en#1fIg0DmM) |
|Others |* [Why can't I view the bucket's usage statistics and other information? I receive a message saying that I lack the necessary permissions.](https://docs.byteplus.com/en/docs/tos/Permission-configuration?lang=en#uBjY9Q9u)<br><br>* [Can I grant different IAM users access permissions to different objects via API?](https://docs.byteplus.com/en/docs/tos/Permission-configuration?lang=en#.6IO95ZCm6YCa6L-HLWFwaS3nu5nkuI3lkIznmoTlrZDnlKjmiLfmjojkuojkuI3lkIzlr7nosaHnmoTorr_pl67mnYPpmZDvvJ8=)<br><br>* [Why aren't the configured permissions taking effect?](https://docs.byteplus.com/en/docs/tos/Permission-configuration?lang=en#.5Li65LuA5LmI6YWN572u5LqG5p2D6ZmQ5LmL5ZCO5rKh5pyJ55Sf5pWI77yf) |

## Bucket policy

### How to configure bucket policy? Does the JSON configuration passed through the interface seem incorrect?

Bucket policy configuration is relatively complex. It is recommended to configure it through the TOS console’s visual view. If you need to create a bucket policy via JSON view, refer to [IAM Policy Management](https://docs.byteplus.com/docs/tos/docs-overview_6) for details.

### What is the relationship between bucket policies and access control lists (ACLs) for buckets and objects? Can they coexist?

* A [bucket policy](https://docs.byteplus.com/en/docs/tos/docs-overview_5?_vtm_=a78999.b69280.0_0.0_0.0.82_7696430788414752309) is a flexible authorization method that allows you to grant specific permissions to Identity and Access Management (IAM) accounts, users, or anonymous users for certain resources.

* In contrast, [bucket and object ACLs](https://docs.byteplus.com/en/docs/tos/docs-overview_4) are a convenient, coarse\-grained authorization method that allows you to grant public read or write access to a bucket, or public read access to an object.

Both can coexist. When both are configured, the bucket policy takes precedence.

### Does TOS support granting permissions to a specific directory inside a bucket?

Yes. You can grant users read and write permissions to specific directories through bucket policies. For detailed steps, see [Bucket Policy Description](https://docs.byteplus.com/docs/tos/docs-creating-a-bucket-policy-with-a-template).

### How can I view the permissions for an existing bucket?

When creating a bucket, if you set the bucket permission to **public read**, a bucket policy that allows access to all users is automatically generated.

## IAM policy

### How can I give an IAM user permission to view only a specific bucket?

You can do so using an IAM policy. For more information, see [IAM policy examples](https://docs.byteplus.com/docs/tos/docs--common-iam-policies).

### How can I grant an IAM user permissions for cross\-region replication?

You can do so using an IAM policy. For more information, see [IAM policy](https://docs.byteplus.com/docs/tos/docs-overview_6).

### If I skip configuring role permissions when creating an IAM role, does IAM assign default permissions to the role?

IAM does not assign default permissions to a role. You must manually add the required permissions to the role. For more information, see [IAM policy overview](https://docs.byteplus.com/en/docs/tos/docs-overview_6).

## ACL

### How can I make a private bucket publicly readable?

You can set bucket permissions using a bucket ACL. For more information, see [Configure Bucket ACL](https://docs.byteplus.com/docs/tos/docs-configuring-a-bucket-acl).

## Others

### Why can't I view the bucket's usage statistics and other information? I receive a message saying that I lack the necessary permissions.

To view usage statistics, you must have read\-only access to Cloud Monitor. For authorization steps,  see [Granting read-only access to Cloud Monitor](https://docs.byteplus.com/en/docs/tos/Grant_read-only_permission_for_account_cloud_monitoring?_vtm_=a78999.b69280.0_0.0_0.0.82_7696430788414752309).

### Can I grant different IAM users access permissions to different objects via API?

No. Currently, granting permissions in batches via API is not supported. For this purpose, you can use bucket policies or IAM policies. For more information, see [Bucket policy](https://docs.byteplus.com/docs/tos/docs-overview_5) and [IAM policy](https://docs.byteplus.com/docs/tos/docs-overview_6).

### Why aren't the configured permissions taking effect?

If a configured permission does not take effect, we recommend that you retry later, as there is a delay.

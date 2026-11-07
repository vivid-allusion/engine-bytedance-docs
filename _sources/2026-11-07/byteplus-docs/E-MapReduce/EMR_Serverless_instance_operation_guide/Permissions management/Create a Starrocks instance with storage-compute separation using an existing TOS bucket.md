---
title: "Create a Starrocks instance with storage-compute separation using an existing TOS bucket"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Use_an_existing_TOS_bucket_to_create_a_Starrocks_instance_with_separated_compute_and_storage"
---

<span id="96ac8a0b"></span>
# Verify the created role

When creating a storage\-compute separated Starrocks instance using an existing TOS bucket, you need to grant the required permissions on the target TOS bucket to BytePlus the preset EMR Serverless role **TOSAccessForEMROLAPVEECSRole**.

In BytePlus the account's access control (IAM), search for **TOSAccessForEMROLAPVEECSRole** role and confirm that this role already exists.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fcef0b1670f4f29b4bc61a18e4debdf~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the <strong>TOSAccessForEMROLAPVEECSRole</strong> role does not exist, go to the product page of StarRocks or Doris in EMR Serverless to authorize and enable the service. The system will automatically create the role.</div>


<span id="a7333064"></span>
# Create Customer managed

Use the JSON editor mode to customize access to the TOS bucket in Customer managed.

Replace `{{bucket_name}}` in the following content with the name of the bucket or path to be authorized.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The "\*" in the content is essential.</div>


```YAML
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tos:Get*",
                "tos:List*",
                "tos:HeadBucket",
                "tos:PutObject",
                "tos:DeleteObject"
            ],
            "Resource": [
                "trn:tos:::{{bucket_name}}*",
                "trn:tos:::{{bucket_name}}*/*"
            ]
        }
    ]
}
```


For example, if your bucket name is olap, your Customer managed statement is as follows:

```C++
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tos:Get*",
                "tos:List*",
                "tos:HeadBucket",
                "tos:PutObject",
                "tos:DeleteObject"
            ],
            "Resource": [
                "trn:tos:::olap*",
                "trn:tos:::olap*/*"
            ]
        }
    ]
}
```


<span id="07b5ca9b"></span>
# Grant Customer managed to the preset role

Authorize the newly created Customer managed to the system preset role TOSAccessForEMROLAPVEECSRole.

Then return to the creation page, enter the TOS path, and perform a connection test.

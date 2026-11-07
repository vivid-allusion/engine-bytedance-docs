---
title: "Using NotPrincipal, NotResource, and NotAction"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Typical-authorization-scenarios-for-notprincipal-notresource-and-notaction"
---

This article introduces typical authorization scenarios and operation instructions for NotPrincipal, NotResource, and NotAction, allowing you to complete authorization based on your situation.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

`NotPrincipal` and `NotResource` must be used with `"Effect":"Deny"`; `NotAction` can be used with `"Effect":"Deny"` or `"Effect":"Allow"`. The meanings are explained as follows:


|**Parameter** | **"Effect":"Deny"**  | **"Effect":"Allow"**  |**Authorization scenarios** |
|---|---|---|---|
|`NotPrincipal` |Deny certain permissions to all users except those specified by `NotPrincipal`. |Not supported. |[Using NotPrincipal to deny access to all users except those specified](https://docs.byteplus.com/docs/tos/Typical-authorization-scenarios-for-notprincipal-notresource-and-notaction#.5L2_55SoLW5vdHByaW5jaXBhbC3lrp7njrDpmaTkuobmjIflrprnlKjmiLfku6XlpJbvvIzmi5Lnu53lhbbku5bnlKjmiLforr_pl64=) |
|`NotResource` |Deny users permission to access all resources except those specified by `NotResource`. |Not supported. |[Using NotResource to deny users access to any resource except those specified](https://docs.byteplus.com/docs/tos/Typical-authorization-scenarios-for-notprincipal-notresource-and-notaction#.5L2_55SoLW5vdHJlc291cmNlLeWunueOsOmZpOS6huaMh-Wumui1hOa6kOS7peWklu-8jOaLkue7neiuv-mXruWFtuS7lui1hOa6kA==) |
|`NotAction` |Deny users permission to perform all actions except those specified by `NotAction`. |Allow users to perform all actions except those specified by `NotAction`. |[Using NotAction to allow users to perform any action except those specified](https://docs.byteplus.com/docs/tos/Typical-authorization-scenarios-for-notprincipal-notresource-and-notaction#b1f8880f) |


For detailed information on `NotPrincipal`, `NotResource`, and `NotAction`, see [Bucket policy templates and parameters](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters).

<span id=".5L2_55SoLW5vdHByaW5jaXBhbC3lrp7njrDpmaTkuobmjIflrprnlKjmiLfku6XlpJbvvIzmi5Lnu53lhbbku5bnlKjmiLforr_pl64="></span>
## Using NotPrincipal to deny access to all users except those specified

This example shows how to deny access to all users except user aaa for objects with the prefix `test/`.

This example itself does not grant permissions to user aaa but only denies access to all other users except aaa. After denying permissions to other users, you need to create a corresponding bucket policy with `"Effect":"Allow"` to grant user aaa access to the specified objects.

<span id="1pWGS79Z"></span>
### Scenario


* Account: User `aaa` .

* Resource: Objects in the `test` directory within the "example" bucket.

* Actions: GetObject, PutObject, DeleteObject, GetObjectVersion, and DeleteObjectVersion.


<span id="p6NtHKDO"></span>
### Recommended configuration method

Bucket policy is recommended for this scenario.

<span id="IV2kIf7w"></span>
### Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation panel, click **Buckets**, then click the target bucket name on the **Buckets** page.

3. In the left navigation panel, select **Permissions \> Bucket policies**.

4. Choose the authorization method as needed.

* Visual view

   1. Click **Create policy**.

   2. At the bottom of the **Create Bucket Authorization Policy** page, select **Custom Policy** and click **Next**.

   3. Set the following parameters.

      * **Policy name**: Click **Basic configuration** and set the policy name.

      * **Effect**: Select **Deny.** 

      * **Authorized user**: Select **Specified account**.

      * **Other accounts**: Select **Current main account**, click **Add Field**, then choose the sub\-user from the **Sub account name** dropdown; here it is set to aaa.

      * **User Policy**: Select **Exclude the above users**.

      * **Resource scope**: Check **Objects in bucket**, choose **Specified objects**, click **Add Field**, and set the **Resource Path** to `test/*`.

      * **Resource strategy**: Select **Including the above resources**.

      * **Object Action**: Select **GetObject**, **PutObject, DeleteObject**, **GetObjectVersion**, and **DeleteObjectVersion**.

      * **Operational strategy**: Select **Including the above actions**.

      * **Condition**: Click the **Add Field** icon to set the required conditions and values. For parameter descriptions about conditions, refer to [Conditions](https://docs.byteplus.com/docs/tos/docs-templates-and-parameters#conditions). No condition setting is required for this scenario.

   4. After completing the setup, click **Next**.

   5. After confirming the policy is correct, click **Create**.

* JSON view

   Click **Edit**, copy the following content into the text box, then click **Save**.

   ```json
   {
     "Statement": [
       {
         "Sid": "Custom policy-1e31",
         "Effect": "Deny",
         "NotPrincipal":["210000****/aaa"],
         "Action": [
           "tos:GetObject",
           "tos:PutObject",
           "tos:DeleteObject",
           "tos:GetObjectVersion",
           "tos:DeleteObjectVersion"
         ],
         "Resource": [
           "trn:tos:::example/test/*"
         ]
       } 
     ]
   }
   ```
   


<span id="9dVZXLVJ"></span>
### Subsequent actions

After denying access to other users, you must grant user aaa the corresponding permissions to ensure that only user aaa can access objects with the prefix `test/`, while other users are denied access. For detailed steps, refer to [Creating a custom bucket policy in JSON view](https://docs.byteplus.com/docs/tos/docs-customizing-a-bucket-policy-in-the-json-view). The corresponding policy content is as follows:

```json
{
  "Statement": [
    {
      "Sid": "Custom policy-1e32",
      "Effect": "Allow",
      "Principal":["210000****/aaa"],
      "Action": [
        "tos:GetObject",
        "tos:PutObject",
        "tos:DeleteObject",
        "tos:GetObjectVersion",
        "tos:DeleteObjectVersion"
      ],
      "Resource": [
        "trn:tos:::example/test/*"
      ]
    } 
  ]
}
```


<span id=".5L2_55SoLW5vdHJlc291cmNlLeWunueOsOmZpOS6huaMh-Wumui1hOa6kOS7peWklu-8jOaLkue7neiuv-mXruWFtuS7lui1hOa6kA=="></span>
## Using NotResource to deny user access to all resources except specified ones

This example demonstrates how user aaa can be denied access to all resources except those under `test/` by using NotResource.

This example does not grant user aaa permissions to `test/` but only denies permissions to resources other than `test/`. After denying permissions to other resources, you must create a bucket policy with `"Effect":"Allow"` to grant user aaa permissions to the `test/` resources.

<span id="8Qo0rq7g"></span>
### Scenario


* Account: User aaa.

* Resources: Objects in the `test` directory within the "example" bucket.

* Actions: GetObject, PutObject, DeleteObject, GetObjectVersion, and DeleteObjectVersion.


<span id="z2Tvxfab"></span>
### Recommended configuration method

Bucket policy is recommended for this scenario.

<span id="i7ith3Bu"></span>
### Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation panel, click **Buckets**, then click the target bucket name on the **Buckets** page.

3. In the left navigation panel, select **Permissions \> Bucket policies**.

4. Choose the authorization method as needed.

* Visual view

   1. Click **Create policy**.

   2. At the bottom of the **Create Bucket Authorization Policy** page, select **Custom Policy** and click **Next**.

   3. Set the following parameters.

      * **Policy name**: Click **Basic configuration** to set the policy name.

      * **Effect**: Select **Deny.** 

      * **Authorized User**: Select **Specified Account**.

      * **Other Account**: Select **Current main account**, click **Add Field**, and choose a sub\-user from the **Sub account name** dropdown. This example uses aaa.

      * **User Policy**: Select **Include the above users**.

      * **Resource Scope**: Check **Objects in bucket**, select **Specified objects**, click **Add Field**, and set the **Resource Path** to `test/*`.

      * **Resource Strategy**: Select **Exclude the above resources**.

      * **Object Action**: Select **GetObject, PutObject, DeleteObject**, **GetObjectVersion** and **DeleteObjectVersion.** 

      * **Operational strategy**: Choose **including the above actions**.

      * **Condition**: Click the **Add field** icon, then set the required conditions and values. For parameter details of conditions, refer to [Conditions](https://docs.byteplus.com/docs/tos/docs-templates-and-parameters#conditions). No conditions need to be set for this scenario.

   4. After setup, click **Next**.

   5. After confirming the policy is correct, click **Create**.

* JSON view

   Click **Edit**, paste the following content into the text box, and click **Save**.

   ```Bash
   {
     "Statement": [
       {
         "Sid": "Custom policy-1e33",
         "Effect": "Deny",
         "Principal":["210000****/aaa"],
         "Action": [
           "tos:GetObject",
           "tos:PutObject",
           "tos:DeleteObject",
           "tos:GetObjectVersion",
           "tos:DeleteObjectVersion"
         ],
         "NotResource": [
           "trn:tos:::example/test/*"
         ]
       } 
     ]
   }
   ```
   


<span id="YBbKKZJA"></span>
### Subsequent operations

After denying other users access to all resources except the `test/` resource, you also need to grant user aaa permissions for the `test/` resource to ensure that user aaa cannot access any other resources except `test/`. For detailed operations, see [Creating a custom bucket policy in JSON view](https://docs.byteplus.com/docs/tos/docs-customizing-a-bucket-policy-in-the-json-view). The corresponding policy content is as follows:

```json
{
  "Statement": [
    {
      "Sid": "Custom policy-1e34",
      "Effect": "Allow",
      "Principal":["210000****/aaa"],
      "Action": [
        "tos:GetObject",
        "tos:PutObject",
        "tos:DeleteObject",
        "tos:GetObjectVersion",
        "tos:DeleteObjectVersion"
      ],
      "Resource": [
        "trn:tos:::example/test/*"
      ]
    } 
  ]
}
```


<span id="b1f8880f"></span>
## Use NotAction to grant users permission to perform all actions except specified ones

This example shows how to use NotAction to grant users permission to perform all actions except DeleteBucket and DeleteObject

<span id="hTvHPPES"></span>
### Scenario


* Account: User aaa

* Resource: Objects in the `test` directory within the "example" bucket.

* Actions: All except DeleteBucket and DeleteObject


<span id="iypO2pAG"></span>
### Recommended configuration method

Bucket policies are recommended in this scenario.

<span id="5YZ83ds7"></span>
### Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation panel, click **Buckets**, then click the target bucket name on the **Buckets** page.

3. In the left navigation panel, select **Permissions \> Bucket policies**.

4. Choose the authorization method as needed.

* Visual view

   1. Click **Create policy**.

   2. At the bottom of the **Create Bucket Authorization Policy** page, select **Custom Policy** and click **Next**.

   3. Set the parameters as follows.

      * **Policy Name**: click **Basic configuration** to set the strategy name.

      * **Effect**: select **Allow.** 

      * **Authorized User**: select **Specified Account**.

      * **Other Account**: select **Current main account**, click **Add Field**, then choose a sub\-user from the **Sub account name** dropdown; here it is set as aaa.

      * **Resource Scope**: check **Objects in bucket**, choose **Specified object**, click **Add Field**, and set the **Resource Path** to `test/*`.

      * **Object Action**: select **DeleteBucket, DeleteObject**.

      * **Operational strategy**: select **Exclude the above actions**.

      * **Condition**: click the **Add Field** icon to set the required conditions and values. For parameter details on conditions, please refer to [Conditions](https://docs.byteplus.com/docs/tos/docs-templates-and-parameters#conditions). Conditions do not need to be set for this scenario.

   4. After completing the setup, click **Next**.

   5. After confirming the policy is correct, click **Create**.

* JSON view

   Click **Edit**, copy the following content into the text box, then click **Save**.

   ```Bash
   {
     "Statement": [
       {
         "Sid": "Custom policy-0de9",
         "Effect": "Allow",
         "Principal": [
           "214748****/aaa"
         ],
         "NotAction": [
           "tos:DeleteBucket",
           "tos:DeleteObject"
         ],
         "Resource": "trn:tos:::example/test/*"
       }
     ]
   }
   ```

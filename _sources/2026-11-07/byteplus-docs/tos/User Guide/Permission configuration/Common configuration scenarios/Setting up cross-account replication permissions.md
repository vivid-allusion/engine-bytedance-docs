---
title: "Setting up cross-account replication permissions"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Permission-configuration-for-cross-account-replication"
---

Before using cross\-account same\-region replication and cross\-account cross\-region replication, you need to configure permissions so that TOS has the corresponding rights to execute cross\-account replication rules. Otherwise, cross\-account replication will fail. This document describes the steps to configure permissions for cross\-account replication.

<span id="e12bd974"></span>
## Permissions required

Before creating cross\-account same\-region and cross\-account cross\-region replication rules, you need to grant TOS read permission on the source bucket and write permission on the target bucket. After authorization, TOS can execute cross\-account replication rules through the ServiceRoleforReplicationAccessTOS role to copy files from the source bucket to the target bucket.

<span id="818320f8"></span>
## Allowing TOS to read from the source bucket

When creating cross\-account replication rules for the first time, you need to grant TOS read permission on the source bucket. If the **CRR** or **SRR** page shows **You have authorized TOS to read and write objects in your bucket**, it indicates that you have completed the source bucket read permission authorization and do not need to perform the following steps.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. 

3. In the top menu bar, select the project of the bucket you want to manage.

4. In the Buckets list, click the bucket you want to manage.

5. In the left navigation pane, select **Fault tolerance and disaster recovery** ** \> CRR**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also grant read permission on the TOS source bucket on the <strong>SRR</strong> page.   </div>
   

6. Click **Authorize**, then click **Confirm** in the pop\-up dialog.

   After authorization, TOS automatically creates the ServiceRoleforReplicationAccessTOS role, which has read permission on the source bucket.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If your bucket is configured with an SSE\-KMS encryption rule, you must also grant TOS permission to access the KMS service; otherwise, cross\-account replication rules cannot be executed.To authorize TOS to use KMS, go to the <strong>Cross\-Region Replication</strong> or <strong>Same\-Region Replication</strong> page, click <strong>Authorize</strong> under the KMS authorization section, and then click <strong>Confirm</strong> in the pop\-up dialog to complete the KMS service authorization.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Your account must have the following IAM permissions to create the ServiceRoleforReplicationAccessTOS role:iam:ListAttachedRolePolicies,iam:CreateRole,iam:AttachRolePolicy.If the replication configuration page displays "Insufficient permissions" when granting TOS read access to the source bucket, you must first assign the above IAM permissions to your account to enable it to create the ServiceRoleforReplicationAccessTOS role. For detailed instructions, refer to <a href="https://docs.byteplus.com/docs/tos/docs-configuring-an-iam-policy">Configuring an IAM Policy</a>.   </div>
   


<span id="c76ac11d"></span>
## Allowing TOS to write to the destination bucket

You need to grant the ServiceRoleforReplicationAccessTOS role write permission on the destination bucket, allowing TOS to write to the destination bucket through this role.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. 

3. In the top menu bar, select the project of the bucket you want to manage.

4. In the Buckets list, click the bucket you want to manage.

5. In the left navigation pane, select **Permissions \> Bucket policies**

6. Select the authorization method as needed.

   
   <Tabs>
   <Tab zoneid="bL4eWpFUuH" title="Visual view">
   <TabTitle>Visual view</TabTitle>
   
   1. Click **Create policy.** 
   
   2. On the **Create Bucket Authorization Policy** page, select the **Folder Read and Write** template, then click **Next**.
   
   3. Set the following parameters.
   
      * **Policy name**: Click **Basic configuration** to set the policy name.
   
      * **Authorized user**: Select **Specified account**.
   
      * **Other account**: Select **Other main account**, then enter the **Main account ID** of the source bucket.
   
         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
         
   
         <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">This article determines permissions based on account ID and rolename. even if your source bucket was created by a sub\-account, you only need to enter the main<strong> </strong>account ID of the sub\-account’s parent when authorizing; there is no need to enter the sub\-user name.      </div>
         
   
      * **Resources**: Select **Current bucket** and **Objects in bucket**, then click **All objects**.
   
      * **Action**: Set bucket actions and object actions.
   
         * **Bucket actions**: ListBucket, HeadBucket, GetBucketVersioning, ListBucketVersions, ListBucketMultipartUploads, and GetBucketObjectLockConfiguration
   
         * **Object actions**: GetObject, PutObject, GetObjectAcl, PutObjectAcl, GetObjectVersion, AbortMultipartUpload, and ListMultipartUploadParts
   
      * **Condition**: Click **Add Field**, set **Key** to **rolename**, **Condition operator** to **Equal to**, and **Value** to **ServiceRoleforReplicationAccessTOS**.
   
   4. After setting, click **Next**.
   
   5. After confirming the policy is correct, click **Create**.
   
   
   </Tab>
   <Tab zoneid="OtWWAvMCA4" title="JSON view">
   <TabTitle>JSON view</TabTitle>
   
   Click **Edit**, copy the following content into the text box, modify the `Principal` account ID and the `Resource` bucket name according to the actual authorization, and click **Save** to complete the setup.
   
   ```JSON
   {
     "Statement": [
       {
         "Sid": "Folder Read and Write-b39e",
         "Effect": "Allow",
         "Principal": [
           "200000****"
         ],
         "Action": [
           "tos:ListBucket",
           "tos:HeadBucket",
           "tos:ListBucketVersions",
           "tos:ListBucketMultipartUploads",
           "tos:GetBucketObjectLockConfiguration",
           "tos:GetBucketVersioning",
           "tos:AbortMultipartUpload",
           "tos:GetObject",
           "tos:PutObject",
           "tos:GetObjectAcl",
           "tos:PutObjectAcl",
           "tos:GetObjectVersion",
           "tos:ListMultipartUploadParts"
         ],
         "Resource": [
           "trn:tos:::test",
           "trn:tos:::test/*"
         ],
         "Condition": {
           "StringEquals": {
             "tos:rolename": [
               "ServiceRoleforReplicationAccessTOS"
             ]
           }
         }
       }
     ]
   }
   ```
   
   
   
   
   
   </Tab>
   </Tabs>

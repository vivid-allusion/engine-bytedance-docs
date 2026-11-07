---
title: "Configuring access point policies"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Configuring_access_point_policies"
---

Access point policies allow for precise and flexible control over file system permissions. They enable you to define exact access rights for different identities to specified directories. This topic outlines the notes and steps for configuring access point policies.

<span id="uMPJgqmp"></span>
## Prerequisites


1. You have created an access point. For instructions, see [Creating an access point](https://docs.byteplus.com/en/docs/nas/efs_managing_access_points#8DplUcqW).

2. You have obtained the access point ID. For instructions, see[ Viewing access point details](https://docs.byteplus.com/en/docs/nas/efs_managing_access_points#1YLRe7NU).


<span id="8uy3n4tr"></span>
## Notes


* When you enable an access point policy, it denies all accounts (including the master account, IAM users, and IAM roles) from mounting and accessing data through the access point. To grant access, you must configure an access point client policy and explicitly assign the policy to authorized accounts.

* Enabling the access point policy for access points already in use may lead to business interruptions.

* To avoid affecting existing business access, it is recommended that you perform incremental mounting after disabling the access point policy.


<span id="jT9oHpIW"></span>
## Step 1: Enable the access point policy.


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, select **Access** **Point**.

6. On the Access point page, click the access point you want to manage.

7. In the **Access point policy** section of the access point details panel, toggle on the **IAM policy** switch.

8. In the box that appears, click **OK**.


<span id="WmaDDG4B"></span>
## Step 2: Create permission policies for the access point


1. Log in to the [IAM console](https://console.byteplus.com/iam/).

2. In the left navigation pane, click **Permission policy**.

3. On the permission policy page, click **Create Policy**.

4. On the **Create Policy** page, enter the policy name and description.

5. Click the **JSON editor** tab, and configure the access point permission policy based on your business needs.

   Here are examples of access point permission policies: Access point read\-only policy and access point read/write policy.

   
   <Tabs>
   <Tab zoneid="HCwtE49s" title="Access point read-only policy">
   <TabTitle>Access point read-only policy</TabTitle>
   
   ```JSON
   {
           "Statement": [
               {
                   "Effect": "Allow",
                   "Action": [
                       "efs:ClientMount",
                       "efs:ClientRootAccess"
                   ],
                   "Resource": ["trn:efs:<RegionId>:<AccountId>:filesystem/<FilesystemId>"],
                   "Condition": {
                       "StringEquals": {
                           "volc:RequestTag/accesspoint": "<Access point ID>"
                       }
                   }
               },
               {
                   "Effect": "Allow",
                   "Action": [
                       "efs:VerifyAccessPoint",
                       "efs:DescribeAccessPoints",
                       "efs:CreateAccessPoint",
                       "efs:ModifyAccessPoint",
                       "efs:DeleteAccessPoint"
                   ],
                   "Resource": [
                       "*"
                   ]
               }
           ]
         }
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="M3PZxw7o" title="Access point read/write policy">
   <TabTitle>Access point read/write policy</TabTitle>
   
   ```JSON
   {
           "Statement": [
               {
                   "Effect": "Allow",
                   "Action": [
                       "efs:ClientMount",
                       "efs:ClientWrite",
                       "efs:ClientRootAccess"
                   ],
                   "Resource": ["trn:efs:<RegionId>:<AccountId>:filesystem/<FilesystemId>"],
                   "Condition": {
                       "StringEquals": {
                           "volc:RequestTag/accesspoint": "<Access point ID>"
                       }
                   }
               },
               {
                   "Effect": "Allow",
                   "Action": [
                       "efs:VerifyAccessPoint",
                       "efs:DescribeAccessPoints",
                       "efs:CreateAccessPoint",
                       "efs:ModifyAccessPoint",
                       "efs:DeleteAccessPoint"
                   ],
                   "Resource": [
                       "*"
                   ]
               }
           ]
       }
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

   Key parameter description:

   
   |Parameter |Parameter description |
   |---|---|
   |Action |Defines the scope of actions for permissions:<br><br><br>* `efs:ClientMount`: Allows mounting file systems with read\-only access.<br><br>* `efs:ClientWrite`: Grants write access to file system data. Must be combined with `ClientMount` (provides mount and read permissions).<br><br>* `efs:ClientRootAccess`: Grants root\-level access privileges. Must be combined with both `ClientMount` and `ClientWrite`.<br><br>   * If ClientRootAccess is not granted, root user access will be automatically mapped to the 'nobody' user account.<br><br>   * If an access point is bound to a POSIX user, `the ClientRootAccess` permission also applies to the POSIX user. For example, when a POSIX user is bound as root but `ClientRootAccess` is not granted, all IO operations through the access point will automatically remap the user to 'nobody'.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The 'nobody' user is a default Linux user. It can only access public content on the server, providing a secure lowest\-privilege baseline for system operations.   </div><br>   <br><br>* `efs:VerifyAccessPoint`: Allows verifying IAM permissions of access points based on a specified account ID.<br><br>* `efs:DescribeAccessPoints`: Allows viewing access points.<br><br>* `efs:CreateAccessPoint`: Allows creating access points.<br><br>* `efs:ModifyAccessPoint`: Allows modifying access points.<br><br>* `efs:DeleteAccessPoint`: Allows deleting access points. |
   |Resource |Defines the scope of resources for permissions:<br><br><br>* If resource scope control is not required, enter `*` to grant permissions to all EFS resources.<br><br>* To give an account root directory access for an access point, enter its TRN. For more information, see [Viewing access point details](https://docs.byteplus.com/en/docs/nas/efs_managing_access_points#1YLRe7NU). |
   |Condition |Defines the conditions under which permissions take effect. |
   

6. Click **Submit**.


<span id="ufqQZwl5"></span>
## Step 3: Grant access point permissions to IAM users, IAM roles, or IAM user groups

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="default">IAM roles do not have permanent credentials and can only access EFS temporarily through an STS temporary AK/SK + token. Once these credentials expire, the IAM role can no longer access EFS.</div>


* <div data-tips="true" data-tips-type="default">Once a policy is linked to a user group, all users in that group receive the same policy permissions.</div>


* <div data-tips="true" data-tips-type="default">Authorization changes for IAM users, roles, and user groups take some time to propagate and take effect.</div>




<Tabs>
<Tab zoneid="BUHqD5Efij" title="Authorize IAM users">
<TabTitle>Authorize IAM users</TabTitle>

1. Create an IAM user. For instructions, see [Creating a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Skip this step if the IAM user already exists.   </div>
   

2. Grant access point permissions to the IAM user.

   1. Log in to the [IAM console](https://console.byteplus.com/iam/).

   2. In the left navigation pane, click **User management** \> **User**.

   3. On the **User** page, click the user you want to manage.

   4. On the **Policy** tab, click **Authorize**.

   5. On the **Add authorization** page, select a policy for the access point.

   6. Click **Submit**.


</Tab>
<Tab zoneid="g029BTqdlk" title="Authorize IAM roles">
<TabTitle>Authorize IAM roles</TabTitle>

1. Create an IAM user and grant this user the **STSAssumeRoleAccess** permission. For instructions, see [Creating a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user).

2. Create an IAM role. For instructions, see [Creating a role](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-role).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Skip this step if the IAM role already exists.   </div>
   

3. Specify authorized users in the IAM role trust policy.

   1. Log in to the [IAM console](https://console.byteplus.com/iam/).

   2. In the left navigation pane, click **Role Management**.

   3. On the **Role Management** page, click the role you want to manage.

   4. On the **Role detail** page, click the **Trust relationship** tab, and then click **Edit trust policy**.

   5. Change the root user in the Principal to the username created in Step 1.

   6. Click **Save**.

4. Grant access point permissions to the IAM role.

   1. On the **Role detail** page, click the **Policy** tab, and then click **Authorize**.

   2. On the **Authorize** page, select a policy for the access point.

   3. Click **Submit**.

5. Obtain the temporary credentials through the **AssumeRole** API. 


</Tab>
<Tab zoneid="ZrAQfOYNK8" title="Authorize IAM user groups">
<TabTitle>Authorize IAM user groups</TabTitle>

1. Create an IAM user group. For instructions, see [Creating a user group](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-group).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Skip this step if the IAM user group already exists.   </div>
   

2. Grant access point permissions to the IAM user group.

   1. Log in to the [IAM console](https://console.byteplus.com/iam/).

   2. In the left navigation pane, click **User management** \> **User group**.

   3. On the **User group** page, click the user group you want to manage.

   4. On the **Policy** tab, click **Authorize**.

   5. On the **Add authorization** page, select a policy for the access point.

   6. Click **Submit**.


</Tab>
</Tabs>


<span id="BZWLKqtA"></span>
## Appendix

<span id="xhefraan"></span>
### Mapping between TOS permissions and access point mount permissions of file systems

Mapping between TOS permissions and access point mount permissions of file systems is as follows:


|File system mount permissions |TOS bucket policy |TOS Bucket ACL |IAM policy |
|---|---|---|---|
|ClientMount |HeadBucket, ListBucket, and GetObject |Read permissions |* Preset policies: TOSReadOnlyAccess<br><br>* Custom policies: HeadBucket, ListBucket, and GetObject |
|ClientMount and ClientWrite |* HeadBucket and PutObject<br><br>* HeadBucket and DeleteObject |* Write permissions<br><br>* Read and write permissions |* Preset policies: TOSFullAccess, AdministratorAccess<br><br>* Custom policies: HeadBucket and PutObject, or HeadBucket and DeleteObject |

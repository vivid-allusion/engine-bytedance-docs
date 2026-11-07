---
title: "Create Single-Region Access Point"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-single-region-access-point"
---

A single\-region access point not only provides an independent access domain name for the bucket, but also supports configuring permission policies for each access point. After delegating permissions to the access point, users accessing TOS resources through the access point are only allowed to perform operations explicitly authorized in the access point policy. This document describes the steps for creating a single\-region access point, creating an access point policy, and delegating permissions to the access point.

<span id="cb7debcd"></span>
## Notes


* Each access point only supports binding to one bucket, and once bound, it cannot be changed.

* Each account can create up to 100 access points per region.

* The total size of the JSON description for each primary account's access point policy must not exceed 20 KB.


<span id="0d82d9e6"></span>
## Scenario Description

Company A has 10 departments that need to collaboratively use a unified data lake for data training, model inference, and other tasks. Although these departments access data from the same bucket, the data and directories they need to access differ. For example:


* Departments 1–3 need to read and write files under databucket/raw.

* Departments 4–6 need to read files under databucket/processed; no write access is required.

* Departments 7–10 need to read and write files under databucket/features.


For the above scenario, the company can use the primary account (210015\*\*\*\*) of the bucket to create access points and access point policies for departments 1–3, 4–6, and 7–10 respectively, and delegate permissions to the access points. After permissions are successfully delegated, these departments can access the corresponding data through different access points.

<span id="38f125c1"></span>
## Step 1: Create Access Point


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, select **Access Point \> Single\-Region Access Point**.

3. On the **Single\-Region Access Point** page, click **Create a Single\-Region Access Point**.

4. On the **Create Single\-Region Access Point** page, configure the following parameters.

   
   |**Parameter** |**Description** |**Example Value** |
   |---|---|---|
   |Access Point Name |Enter the access point name. The naming rules are as follows:<br><br><br>* Only lowercase letters a–z, uppercase letters A–Z, hyphens (\-), and numbers are allowed.<br><br>* Length must be between 3 and 50 characters.<br><br>* Cannot start or end with a hyphen (\-), and cannot end with `-tosalias`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The access point name must be globally unique within each account and region.</div><br> |* Departments 1–3: ap1<br><br>* Departments 4–6: ap2<br><br>* Departments 7–10: ap3 |
   |Bucket |Select the bucket to be bound; only one bucket can be selected. |* Departments 1–3: databucket<br><br>* Departments 4–6: databucket<br><br>* Departments 7–10: databucket |
   |Network source |Instructions for selecting the network source of the access point are as follows:<br><br><br>* **Internet**: When accessing resources within TOS through the access point, requests from both external and internal networks are allowed.<br><br>* **VPC**: When accessing resources within TOS through the access point, only requests from the specified VPC are allowed. After selecting this option, you also need to choose the VPC name. |* Departments 1–3: Internet<br><br>* Departments 4–6: Internet<br><br>* Departments 7–10: Internet |
   

5. After completing the configuration, click **Select**.

   After successfully creating a single\-region access point, you can click the name of the single\-region access point and view information such as the TRN, alias, and external Endpoint under the **Overview** tab.


<span id="07da5241"></span>
## Step 2: Create an Access Point Policy

The access point policy supports creation via either the visual view or the JSON view, allowing you to choose flexibly according to your actual needs and usage habits.

<span id="7fc9a84b"></span>
### Create an Access Point Policy Using the Visual View


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, select **Access Point \> Single\-Region Access Point**.

3. On the **Single\-Region Access Point** page, click the name of the target single\-region access point.

4. On the single\-region access point details page, click the **Permission** tab.

5. Under the **Visual view** tab, click **Create policy**.

6. In the **Select template** configuration wizard, select a policy template and click **Next step**.

   In this scenario, Departments 1–3 and 7–10 select the **Folder Read and Write** template, while Departments 4–6 select the **Folder Read\-Only** template.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The resource scope and actions of the access point policy templates are the same as those of bucket policy templates. You may refer to the bucket policy template documentation to select an access point policy template. For details, see <a href="https://docs.byteplus.com/docs/tos/docs-templates-and-parameters#127974e6">Bucket Policy Templates</a>.   </div>
   

7. In the **Configure policy** configuration wizard, set the parameters and click **Next step**.

   
   |**Parameter** |**Note** |**Example Value** |
   |---|---|---|
   |Policy configuration method |Select **Visual view**. |Visual View |
   |Policy Name |Set the name of the access point policy. |* Departments 1–3: Folder read/write \- fb8e<br><br>* Departments 4–6: Folder read\-only \- b6ec<br><br>* Departments 7–10: Folder read/write \- yu3i |
   |Effect |Select the effect of the policy.<br><br><br>* **Allow**: Indicates that the permission created by this policy is to accept requests.<br><br>* **Deny**: Indicates that the permission created by this policy is to deny requests. |Allow |
   |Authorized user |* **Specified account**: Only the specified account has the permissions defined by the corresponding policy. Details are as follows:<br><br>   * **Current mian account**: Used to grant permissions to IAM users (sub\-users) under the current primary account. No need to enter the primary account ID. Click **Add row**, and you can select the sub\-user name from the **Sub account name** dropdown list.<br><br>   * **Other mian account**: Used to grant permissions to other primary accounts and IAM users (sub\-users) of other primary accounts. You need to enter the other primary account ID and the sub\-user name of the other primary account.<br><br>* **All users**: Users (including anonymous users) can execute the current access point policy without authentication. If your **Effect** is set to **Allow**, it may pose a data storage security risk. Please select with caution. |Select **current primary account**, click **Add a row**, and select the sub\-user name. The sub\-user names used by each department are as follows:<br><br><br>* Departments 1–3: ai\-dev<br><br>* Departments 4–6: data\-dev<br><br>* Departments 7–10: model\-dev |
   |User Policy |To set the user authorization method, you can only configure the **User Policy** parameter when **Effect** is set to **Deny**. When **Effect** is **Deny**, the parameter meanings are as follows:<br><br><br>* **Include the above users**: Deny specified users certain permissions.<br><br>* **Exclude the above users**: Deny all users except the specified ones certain permissions.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The 'Exclude the above users' function is only used to deny user permissions and does not grant any permissions itself. If you want to grant certain permissions to specified users, you also need to create the corresponding permission policy. For detailed instructions, see <a href="https://docs.byteplus.com/docs/tos/Typical-authorization-scenarios-for-notprincipal-notresource-and-notaction#.5L2_55SoLW5vdHByaW5jaXBhbC3lrp7njrDpmaTkuobmjIflrprnlKjmiLfku6XlpJbvvIzmi5Lnu53lhbbku5bnlKjmiLforr_pl64=">Using NotPrincipal to deny access to users other than those specified</a>.</div><br> |None |
   |Resource scope |* **Current Single\-Region Access Point**: Indicates that the scope of the policy is the bucket under the single\-region access point. You can configure bucket\-related actions in **Action**.<br><br>* **Objects in bucket**: Indicates that the scope of the policy is objects within the bucket. You can configure object\-related actions in **Action**.<br><br>   * **All objects**: Indicates that the scope of the policy is all objects within the bucket.<br><br>   * **Specified object**: After selecting **Specified object**, click the **Add row** icon to set the specified object field. |Select **Current Single\-region Access Point** and **Objects in Bucket**, click **Specify Object**, and enter the resource path. The resource paths required by each department are as follows:<br><br><br>* Departments 1–3: raw/\*<br><br>* Departments 4–6: processed/\*<br><br>* Departments 7–10: features/\* |
   |Resource strategy |Set the resource authorization method. Only when the **effect** is **deny** can the **resource strategy** parameter be set. When the **effect** is **deny**, the parameter meanings are as follows:<br><br><br>* **Include the above resources**: Deny the user's permission to the specified resources.<br><br>* **Exclude the above resources**: Except for the specified resources, deny the user's permission to all other resources.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The function to exclude the above resources is only used to deny the user's permission to certain resources and does not itself grant authorization. If you want the user to have permission to the specified resources, you also need to create the corresponding permission policy. For detailed instructions, please refer to <a href="https://docs.byteplus.com/docs/tos/Typical-authorization-scenarios-for-notprincipal-notresource-and-notaction#.5L2_55SoLW5vdHJlc291cmNlLeWunueOsOmZpOS6huaMh-Wumui1hOa6kOS7peWklu-8jOaLkue7neiuv-mXruWFtuS7lui1hOa6kA==">Using NotResource to deny user access to all resources except the specified ones</a>.</div><br> |None |
   |Action |Select the actions to be authorized. For detailed instructions, please refer to [Supported Actions](https://docs.byteplus.com/docs/tos/docs-templates-and-parameters#3817a80f). |Use the action selected by default in the template. |
   |Operation Policy |Set the action authorization method. The meaning varies depending on the policy effect.<br><br><br>* When **Effect** is **Deny**, the operation policy means:<br><br>   * **Include the above actions**: Deny the user permission to perform the specified actions.<br><br>   * **Exclude the above actions**: Except for the specified actions, deny the user permission to perform all other actions.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The 'Exclude the above actions' function is only used to deny users permission to perform certain actions; it does not itself grant permissions. If you want users to have permission to perform specified actions, you also need to create the corresponding permission policy.   </div><br>   <br><br>* When **Effect** is **Allow**, the operation policy means:<br><br>   * **Include the above actions**: Allow the user permission to perform the specified actions.<br><br>   * **Exclude the above actions**: Except for the specified actions, allow the user permission to perform all other actions.  |Include the above actions |
   |Condition |Click the **Add row** icon to set the conditions and values you require. For parameter descriptions of conditions, please refer to [Condition Description](https://docs.byteplus.com/docs/tos/docs-templates-and-parameters#eaa7b0fa). |None |
   

8. In the **Confirm policy** configuration wizard, click **Submit**.


<span id="deda8734"></span>
### Create an Access Point Policy Using the JSON View


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, select **Access Point \> Single\-Region Access Point**.

3. On the **Single\-Region Access Point** page, click the name of the target single\-region access point.

4. On the single\-region access point details page, click the **Permission** tab.

5. Click the **JSON view** tab.

6. Click **Edit** to set the content of the access point policy.

   Except for the `Resource` and `NotResource` parameters, the meanings of other parameters in the access point policy are the same as those in the bucket policy. For details, see [Bucket Policy Parameter Description](https://docs.byteplus.com/docs/tos/docs-templates-and-parameters#3ab0f186).

   
   |**Parameters** |**Description** |
   |---|---|
   |Resource |Specify the resource scope for the access point policy. The configuration rules are as follows:<br><br><br>* When performing operations on buckets under the access point policy, you need to set `Resource` to `Access Point TRN`. For example, `"Resource": "trn:tos:cn-beijing:214748****:accesspoint/bbb"`.<br><br>* When performing operations on objects in buckets under the access point policy, you need to set `Resource` to `<Access Point TRN>/object/<Resource path in bucket>`. For example, to perform operations on test/, `Resource` should be configured as `"trn:tos:cn-beijing:214748****:accesspoint/bbb/object/test/*"`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">On the <strong>Single Region Access Point</strong> page, click the single region access point name. Under the <strong>Overview</strong> tab, you can obtain the access point TRN.</div><br> |
   |NotResource |This parameter must be used together with "Effect":"Deny". When used with "Effect":"Deny", users will be denied access to all resources except those specified by NotResource. The configuration rules are as follows:<br><br><br>* When performing operations on buckets under the access point policy, you need to set `Resource` to `Access Point TRN`. For example, `"Resource": "trn:tos:cn-beijing:214748****:accesspoint/bbb"`.<br><br>* When performing operations on objects in buckets under the access point policy, you need to set `Resource` to `<Access Point TRN>/object/<Resource path in bucket>`. For example, to perform operations on test/, `Resource` should be configured as `"trn:tos:cn-beijing:214748****:accesspoint/bbb/object/test/*"`. |
   

   An example policy is as follows:

   
   <Tabs>
   <Tab zoneid="zMz2BRNbpV" title="Access Point Policy for Departments 1–3">
   <TabTitle>Access Point Policy for Departments 1–3</TabTitle>
   
   ```JSON
   {
     "Statement": [
       {
         "Sid": "Folder read and write-fb8e",
         "Effect": "Allow",
         "Principal": [
           "210015****/ai-dev"
         ],
         "Action": [
           "tos:ListBucket",
           "tos:HeadBucket",
           "tos:ListBucketVersions",
           "tos:ListBucketMultipartUploads",
           "tos:AbortMultipartUpload",
           "tos:GetObject",
           "tos:PutObject",
           "tos:GetObjectAcl",
           "tos:PutObjectAcl",
           "tos:GetObjectVersion",
           "tos:ListMultipartUploadParts"
         ],
         "Resource": [
           "trn:tos:cn-beijing:210015****:accesspoint/ap1",
           "trn:tos:cn-beijing:210015****:accesspoint/ap1/object/raw/*"
         ],
       }
     ]
   }
   ```
   
   
   
   </Tab>
   <Tab zoneid="fdcWFdVWrS" title="Access Point Policy for Departments 4–6">
   <TabTitle>Access Point Policy for Departments 4–6</TabTitle>
   
   ```JSON
   {
     "Statement": [
       {
         "Sid": "Folder read-b6ec",
         "Effect": "Allow",
         "Principal": [
           "210015****/data-dev"
         ],
         "Action": [
           "tos:ListBucket",
           "tos:HeadBucket",
           "tos:ListBucketVersions",
           "tos:GetObject",
           "tos:GetObjectAcl",
           "tos:GetObjectVersion"
         ],
         "Resource": [
           "trn:tos:cn-beijing:210015****:accesspoint/ap2",
           "trn:tos:cn-beijing:210015****:accesspoint/ap2/object/processed/*"
         ]
       }
     ]
   }
   ```
   
   
   
   </Tab>
   <Tab zoneid="jRUknitNAC" title="Access Point Policy for Departments 7–10">
   <TabTitle>Access Point Policy for Departments 7–10</TabTitle>
   
   ```JSON
   {
     "Statement": [
       {
         "Sid": "Folder read and write-yu3i",
         "Effect": "Allow",
         "Principal": [
           "210015****/model-dev"
         ],
         "Action": [
           "tos:ListBucket",
           "tos:HeadBucket",
           "tos:ListBucketVersions",
           "tos:ListBucketMultipartUploads",
           "tos:AbortMultipartUpload",
           "tos:GetObject",
           "tos:PutObject",
           "tos:GetObjectAcl",
           "tos:PutObjectAcl",
           "tos:GetObjectVersion",
           "tos:ListMultipartUploadParts"
         ],
         "Resource": [
           "trn:tos:cn-beijing:210015****:accesspoint/ap3",
           "trn:tos:cn-beijing:210015****:accesspoint/ap3/object/features/*"
         ]
       }
     ]
   }
   ```
   
   
   
   </Tab>
   </Tabs>
   

7. After configuring the parameters, click **Submit**.


<span id="3f2b27a7"></span>
## Step 3: Delegate Permissions to the Access Point

When accessing bucket resources via an access point, the system checks both the access point policy and the bucket policy. Access is only granted if both the access point policy and the bucket policy permit the request. If either policy denies or does not authorize the request, the request will fail. After successfully creating a single\-region access point policy, you need to configure a delegation authorization policy in the bucket policy of the storage bucket associated with the single\-region access point. This delegates the access control capability of the bucket policy to each access point, allowing users to access bucket resources through the access point.

TOS provides a visual permission delegation feature. After selecting the delegation type on the access point permission delegation page, the system automatically generates the corresponding delegation authorization policy. Once confirmed, the system will automatically create the relevant delegation authorization policy in the bucket policy of the storage bucket associated with the single\-region access point, thereby simplifying complex bucket policy configurations and achieving permission isolation based on the access point dimension.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, select **Access Point \> Single\-Region Access Point**.

3. On the **Single\-Region Access Point** page, click the name of the target single\-region access point.

4. On the single\-region access point details page, click the **Permission** tab.

5. Under the Visual View tab, click **Access point permission delegation**.

6. In the **Select delegate type** configuration wizard, select the **Delegation type** and click **Generation Policy**.

   
   |**Delegation Type** |**Description** |**Example Value** |
   |---|---|---|
   |DataAccessPointTrn |Delegate permissions for the current access point. After delegation, only the current access point is effective. |Select AccessPointNetworkOrigin, then select Internet. |
   |DataAccessPointAccount |Delegate permissions for all access points under the current account. Once delegation is complete, all access points under this account will take effect. ||
   |AccessPointNetworkOrigin |Delegate permissions for all access points from the specified network origin. Once delegation is complete, all access points from this network origin will take effect.<br><br>After selecting AccessPointNetworkOrigin, you also need to select the network origin. The instructions are as follows:<br><br><br>* **VPC**: Delegate permissions for all access points with network origin **VPC**.<br><br>* **Internet**: Delegate permissions for all access points with network origin **Internet**. ||
   

7. In the **Generation Policy** configuration wizard, after confirming the policy information is correct, click **Submit**.


<span id="730cad7a"></span>
## Follow\-up Actions

After successfully delegating permissions to the access point, you can share the access point alias with the relevant department, enabling them to access the corresponding resources via the access point. For specific operations, please refer to [Using Single-Region Access Point](https://docs.byteplus.com/docs/tos/Use-a-single-region-access-point).

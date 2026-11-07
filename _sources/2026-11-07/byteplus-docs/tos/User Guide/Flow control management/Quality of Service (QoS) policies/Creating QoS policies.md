---
title: "Creating QoS policies"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-a-qos-policy"
---

TOS allows you to customize a QoS policy in the visual or JSON view. This topic explains how to do so.

<span id="e2aa4888"></span>
## Notes


* The total JSON description size of QoS policies per account cannot exceed 20 KB.

* A single `Statement` can have at most ten resources or principals.

* If a request matches multiple QoS policies, all of the policies take effect. In this case, if the policies have the same type of QoS restriction, the restriction with the lowest quota applies.

* A QoS policy defines the bandwidth limit for specific resources under specific conditions within a region. Burst bandwidth, on the other hand, is an account's flexible upper limit at the regional level. These two concepts operate at different levels and take effect concurrently.

   For example, if an account’s intranet download bandwidth in China (Guangzhou) is 10 Gbps and its burst bandwidth is 5 Gbps, then the total intranet download bandwidth is 15 Gbps. At this time:

   * If you set a QoS policy for the "my\-data" bucket under this account that limits the maximum intranet read bandwidth to 2 Gbps, the system allows the "my\-data" bucket a maximum intranet read bandwidth of 2 Gbps.

   * If you set a QoS policy for the "my\-data" bucket that limits its maximum intranet read bandwidth to 20 Gbps but the account’s total intranet download bandwidth quota is 15 Gbps, the system will allow the "my\-data" bucket a maximum intranet read bandwidth of 15 Gbps.

* By default, the owner of an account has full permissions. IAM users have no permissions by default. If an IAM user needs to perform any of the following operations, the account owner must grant the user the appropriate permissions using an [IAM](https://docs.byteplus.com/en/docs/tos/docs-overview_6) or [bucket policy](https://docs.byteplus.com/en/docs/tos/docs-overview_5).

   * Set QoS policies: `tos:PutQosPolicy`

   * View QoS policy configurations: `tos:GetQosPolicy`

   * Delete QoS policies: `tos:DeleteQosPolicy`


<span id="a5380bf5"></span>
## Creating a QoS policy in visual view


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Flow control management** \> **QoS policy management**.

3. At the top left of the **QoS policy management** page, select the target region.

4. On the **Visual view** tab, click **Create policy**.

5. On the **Create QoS policy** page, set the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Policy configuration method |Select **Visual view**. |
   |Policy name |Enter a name for the policy. The policy name must:<br><br><br>* Be unique.<br><br>* Contain only uppercase and lowercase letters, numbers, hyphens (\-), underscores (_), periods (.), colons (:) and percent signs (%).<br><br>* Be between 1 and 255 characters long.<br><br><br>If this parameter is not specified, TOS will automatically generate a name. |
   |Policy Type |Select a throttling scheme for the QoS policy:<br><br><br>* **Threshold traffic control**: Uses flexible combinations of identity dimensions and resource scopes to throttle traffic to TOS resource groups. This enables isolation between multiple workloads.<br><br>* **Priority traffic control**: Adds multiple priority levels and guaranteed quotas to threshold\-based throttling, ensuring the stable operation of core services while maximizing resource utilization. |
   |QoS value |Set the throttling limits for the QoS policy. Options:<br><br><br>* **WritesQPS**: The QPS limit for write requests. Enter a positive integer.<br><br>* **ReadsQPS**: The QPS limit for read requests. Enter a positive integer.<br><br>* **ListQPS**: The QPS limit for list requests. Enter a positive integer.<br><br>* **WritesRate**: The upload bandwidth limit in Mbps. Enter a positive integer.<br><br>* **ReadsRate**: The download bandwidth limit in Mbps. Enter a positive integer.<br><br>* **FetchQps**: The QPS limit for synchronous fetches. Enter a positive integer.<br><br>* **FetchRate**: The bandwidth limit for synchronous fetches in Mbps. Enter a positive integer.<br><br>* **AsyncFetchQPS**: The QPS limit for asynchronous fetches. Enter a positive integer.<br><br>* **AsyncFetchRate**: The bandwidth limit for asynchronous fetches in Mbps. Enter a positive integer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For limits on read/write requests and bandwidth for each region per account, see <a href="https://docs.byteplus.com/docs/tos/docs-restrictions">Constraints and limitations</a>.</div><br> |
   |Priority |The QoS policy's priority level follows these rules:<br><br><br>* It takes natural numbers starting from 1, and they must be consecutive and unique. For example, 1/2 and 1/2/3 are supported, but 1/3 is not.<br><br>* At least 2 and at most 3 priority levels must be configured. A higher number indicates a higher priority.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter only applies when the <strong>Policy Type</strong> is set to <strong>Priority traffic control</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After you add priority configurations, the system automatically assigns the priority values. You do not need to enter them manually. You can click <strong>Move up</strong> or <strong>Move down</strong> in the <strong>Actions</strong> column to adjust priorities.</div><br> |
   |Guaranteed flow control value |Reserve a minimum amount of resources for a priority level. Even when the system is fully loaded, this level is guaranteed to receive this amount or more. This value follows the same rules as the **QoS value** parameter.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter only applies when the <strong>Policy Type</strong> is set to <strong>Priority traffic control</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Each priority level must be assigned a guaranteed quota greater than 0. In other words, a guaranteed quota must be assigned to each additional priority level.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The sum of the guaranteed quotas for all priority levels must be less than or equal to the total quota.</div><br> |
   |Authorized user |* **Specified account**: The policy only applies to the specified account(s). Options:<br><br>   * **Current main account**: The policy applies to one or more IAM users (subusers) or roles within the current account. The account ID is displayed by default. Click **Add row** to select IAM users or roles from the dropdown menu.<br><br>   * **Other main account**: The policy applies to another account and its IAM users (subusers) or roles. Enter the account ID and IAM username(s) or rolename(s).<br><br>* **All users**: The policy applies to all users, including anonymous users. |
   |User Policy |Select whether to include or exclude the specified user(s). The options are explained below.<br><br><br>* **Include the above users**: The policy applies to **authorized users**.<br><br>* **Exclude the above users**: The policy applies to all users except **authorized users**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>User Policy</strong> cannot be set to <strong>Exclude the above users</strong> when <strong>Authorized user</strong> is set to <strong>All users</strong>.</div><br> |
   |Resource |* **All buckets**: The policy takes effect on all buckets.<br><br>* **Objects in bucket**: The policy takes effect on a specific bucket. Select a bucket and specify the resource scope further:<br><br>   * **All objects**: All objects within the bucket.<br><br>   * **Specified object(s)** : Specific object(s) within the bucket. If you select **Specified object(s)** , click **Add resource path** to enter the prefix for the specified object(s).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The resource scope covers all buckets if both <strong>All buckets</strong> and <strong>Objects in bucket</strong> are selected under <strong>Resource</strong>.</div><br> |
   |Resource strategy |Select whether to include or exclude the specified resource(s). The options are explained below.<br><br><br>* **Include the above resources**: The policy applies to the specified **resources**.<br><br>* **Exclude the above resources**: The policy applies to all **resources** except those specified.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>Resource strategy</strong> cannot be set to <strong>Exclude the above resources</strong> when <strong>Resource scope</strong> is set to <strong>All buckets</strong>.</div><br> |
   |Condition |Click the **Add row** icon and set the condition and value. For more information, see [Conditions](https://docs.byteplus.com/en/docs/tos/Qos-policy-overview#aNd3FkmH). |
   

6. After completing the settings, click **Next step**.

7. After verifying the details, click **Confirm**.


<span id="94ae834d"></span>
## Creating a QoS policy in JSON view


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Flow control management** \> **QoS policy management**.

3. At the top left of the **QoS policy management** page, select the target region.

4. Click the **JSON view** tab.

5. Click **Edit** and enter the policy content. For more information on QoS policy parameters, see [Parameters](https://docs.byteplus.com/en/docs/tos/Qos-policy-overview#dBMgvLV2).

   Threshold‑based throttling example:

   The following statement establishes a 5,000 Mbps upload bandwidth limit for user "aaa" on the "bucketname" bucket.

   ```Plain
   {
     "Statement": [
       {
         "Sid": "test",
         "Quota": {
           "WritesQps": "",
           "ReadsQps": "",
           "ListQps": "",
           "WritesRate": "5000",
           "ReadsRate": "",
           "FetchQps": "",
           "FetchRate": "",
           "AsyncFetchQps": "",
           "AsyncFetchRate": ""
         },
         "Principal": [
           "trn:iam::214748****:user/aaa"
         ],
         "Resource": "trn:tos:::bucketname/*"
       }
     ]
   }
   ```
   

   Priority‑based throttling example:

   The following statement sets the upload bandwidth limit for user "aaa" to 5,000 Mbps for buckets "bucket1", "bucket2", and "bucket3". "bucket1" has priority 1 and a guaranteed upload bandwidth of 1,000 Mbps. "bucket2" has priority 2 and a guaranteed upload bandwidth of 1,000 Mbps. "bucket3" has priority 3 and a guaranteed upload bandwidth of 3,000 Mbps.

   ```Plain Text
   {
     "Statement": [
       {
         "Sid": "test-qos-policy",
         "Quota": {
           "WritesRate": "5000"
         },
         "Priority": [
           {
             "PriorityLevel": 3,
             "GuaranteedQuota": {
               "WritesRate": "3000"
             },
             "Principal": [
               "trn:iam::200000:user/aaa"
             ],
             "Resource": "trn:tos:::bucket3/*"
           },
           {
             "PriorityLevel": 2,
             "GuaranteedQuota": {
               "WritesRate": "1000"
             },
             "Principal": [
               "trn:iam::200000:user/aaa"
             ],
             "Resource": "trn:tos:::bucket2/*"
           },
           {
             "PriorityLevel": 1,
             "GuaranteedQuota": {
               "WritesRate": "1000"
             },
             "Principal": [
               "trn:iam::200000:user/aaa"
             ],
             "Resource": "trn:tos:::bucket1/*"
           }
         ]
       }
     ]
   }
   ```
   

6. Save your settings by clicking **Save**.


<span id="a660af3e"></span>
## Related operations


* Edit a QoS policy

   On the **QoS policy management** page, click the **Visual view** tab and then click **Edit** in the **Actions** column of the relevant policy. This will take you to the editing page where you can modify the policy.

* Copy a QoS policy

   On the **QoS policy management** page, find the **Visual view** tab and click  **...**  \> **Copy** in the **Actions** column of the relevant policy. On the **Create QoS policy** page, verify that the policy details are correct, and then click **Next step** and **Confirm**.

* Delete a QoS policy

   On the **QoS policy management** page, click the **Visual view** tab. In the **Actions** column of the relevant policy, click **Delete**. Then, confirm the deletion by clicking **Delete** in the box that appears.

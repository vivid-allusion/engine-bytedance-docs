---
title: "Creating ObjectSet tag policies"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Creating-ObjectSet-tag-policies"
---

You can add tags to your ObjectSets. Then, you can set quality of service (QoS) throttling and capacity limits for ObjectSets that share the same tag. You can also configure lifecycle rules to migrate or archive objects in bulk within all ObjectSets that have a specific tag. This topic explains how to create a tag policy.

<span id="0hUpk7u7"></span>
## Notes

Each key\-value pair corresponds to exactly one tag policy.

<span id="3ahipAJV"></span>
## Steps


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. In the left navigation pane, select **ObjectSet \> ObjectSet policy**.

6. Click **Create tag policy** and set the following parameters.

   
   |Category |Parameter |Description |
   |---|---|---|
   |Tag information |Tag Key |Key for the ObjectSet tag.<br><br>Requirements:<br><br><br>* The key length cannot exceed 128 characters.<br><br>* Tag keys cannot contain Chinese characters.<br><br>* Each key\-value pair corresponds to exactly one tag policy. |
   ||Tag Value |Value for the ObjectSet tag.<br><br>Requirements:<br><br><br>* The value length cannot exceed 256 characters.<br><br>* Tag values cannot contain Chinese characters.<br><br>* Each key\-value pair corresponds to exactly one tag policy. |
   |QoS traffic control |ReadsQps |QPS limit for read requests to ObjectSets that share the tag.<br><br>Enter a positive integer between 0 and 100,000,000. A value of 0 means there is no limit. |
   ||WritesQps |QPS limit for write requests to ObjectSets that share the tag.<br><br>Enter a positive integer between 0 and 100,000,000. A value of 0 means there is no limit. |
   ||ListQps |QPS limit for list requests to ObjectSets that share the tag.<br><br>Enter a positive integer between 0 and 100,000,000. A value of 0 means there is no limit. |
   ||ReadsRate |Read bandwidth limit, in Mbps, for ObjectSets that share the tag.<br><br>Enter a positive integer between 0 and 100,000,000. A value of 0 means there is no limit. |
   ||WritesRate |Write bandwidth limit, in Mbps, for ObjectSets that share the tag.<br><br>Enter a positive integer between 0 and 100,000,000. A value of 0 means there is no limit. |
   |Capacity ceiling |Capacity ceiling |Capacity limit for ObjectSets that share the tag.<br><br>The valid range is from 0 to 100 PiB. A value of 0 means there is no limit. |
   |Lifecycle |Go to configuration lifecycle rules |Lifecycle rules for ObjectSets that share the tag.<br><br>Go to the **Lifecycle** page to configure and associate rules uniformly. |
   

7. Click **OK** to finish creating the policy.


<span id="iZ2vUYb8"></span>
## Other operations

From the **Tag policy** page, you can perform the following operations on your tag policies.


* **Edit a tag policy**: Click **Edit** in the **Actions** column of the policy. This allows you to modify its QoS throttling limits and lifecycle rules.

* **Delete a tag policy**: Click **Delete** in the **Actions** column of the policy. In the box that appears, click **OK** to delete the policy.


&nbsp;

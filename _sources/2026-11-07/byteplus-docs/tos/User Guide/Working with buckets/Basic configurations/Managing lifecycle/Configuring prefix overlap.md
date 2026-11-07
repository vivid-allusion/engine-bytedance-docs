---
title: "Configuring prefix overlap"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Set-prefix-overlap"
---

The prefix overlap feature allows you to create lifecycle rules with overlapping prefixes. This topic covers how to configure the feature and its enforcement logic.

<span id="2ec01366"></span>
## Background information

With prefix overlap disabled, you cannot create two or more lifecycle rules that transition objects with overlapping prefixes to the same storage type, or delete objects with overlapping prefixes. With prefix overlap enabled, you can create lifecycle rules with overlapping prefixes under any conditions.

<span id="d55f249d"></span>
## Rule priority

After enabling prefix overlap, if an object matches multiple lifecycle rules, the rule with a short expiration date will be executed first. If the lifecycle rules have the same expiration date, the lifecycle rules will be executed according to the principle of lower cost. The specific priorities are as follows:

Delete Object \> Transition to Deep Cold Archive \> Transition to Cold Archive \> Transition to Archive \> Transition to Flashback Archive \> Transition to Infrequent Access Storage \> Add Deletion Mark to Object

For example, if one rule is configured to transition all objects in the bucket to Infrequent Access Storage 180 days after upload, and another rule is configured to transition objects with the prefix `test/` to Infrequent Access Storage 90 days after upload, then objects with the prefix `test/` will transition to Infrequent Access Storage after 90 days. All other objects in the bucket will transition to Infrequent Access Storage after 180 days.

<span id="bcbe323a"></span>
## Turn on prefix overlap

Before enabling prefix overlap, make sure you have a lifecycle rule in place, otherwise prefix overlap cannot be enabled.


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, select **Basic Settings \> Lifecycle.** 

4. In the upper\-left corner of the **lifecycle** page, turn on the **Prefix overlap** switch.


<span id="29bb5376"></span>
## Turn off prefix overlap

Before turning off prefix overlap, delete all prefix overlap lifecycle rules, otherwise prefix overlap cannot be turned off.


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, select **Basic Settings \> Lifecycle.** 

4. In the upper\-left corner of the **Lifecycle** page, turn off the **Prefix overlap** switch.

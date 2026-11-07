---
title: "Configuring lifecycle rules based on last access time"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Lifecycle-rules-based-on-last-accesstime"
---

With TOS, you can configure lifecycle rules based on when an object was last accessed (last access time). You can instruct TOS to automatically move an object to the most cost\-effective storage type when it remains unaccessed for a preset number of days. This approach allows for intelligent data tiering, helping you identify cold data and reduce storage costs. This topic introduces the use cases, notes, and steps for configuring lifecycle rules based on last access time.

<span id="9ed99dfb"></span>
## Use cases

Both Intelligent Tiering and lifecycle rules allow you to transition objects based on their access frequency to reduce storage costs. However, these features are mutually exclusive and cannot be configured simultaneously. They also differ in implementation and use cases. See below for a detailed explanation of their respective characteristics and use cases.


|Feature |**Use cases** |
|---|---|
|Intelligent Tiering |* **Characteristics**: Intelligent Tiering automatically moves objects between the frequent, infrequent, and flashback archive access tiers based on how often they are accessed. These transition rules are fixed and cannot be modified at this time. For more information, see [Intelligent Tiering overview](https://docs.byteplus.com/docs/tos/docs-overview_1).<br><br>* **Use cases**: Suitable for scenarios where data access patterns are changing or unpredictable. |
|Configuring lifecycle rules based on last access time |* **Characteristics**: Lifecycle rules can be used to transition objects to the desired storage type if they remain unaccessed for a preset number of days. The applicable storage types are Infrequent Access Storage, Flashback Archive, Archive, Cold Archive, and Deep Cold Archive. Lifecycle rules provide greater flexibility in configuration, allowing you to specify the number of days or time until expiration.<br><br>* **Use cases**: Suitable for scenarios where data access patterns are well understood, and more flexible data tiering policies are desired. |


<span id="59f18d90"></span>
## Notes


|**Category** |Considerations |
|---|---|
|Supported features |You can create a lifecycle rule that transitions objects based on their last access time. However, you cannot use a lifecycle rule to delete objects based on their last access time. |
|Storage type |You can use a lifecycle rule to transition objects to the following storage types: Infrequent Access Storage, Flashback Archive, Archive, Cold Archive, and Deep Cold Archive. However, you cannot use a lifecycle rule to transition objects to Intelligent Tiering. |
|Usage limits |* Transitioning unmerged parts and appendable objects based on the last access time is not supported.<br><br>* A lifecycle rule can include policies based on either the last modified or access time, but not both. |
|Operations that update an object's last access time |TOS calculates the last access time of objects from the day access monitor is enabled. Operations such as overwriting or downloading an object update its last access time.<br><br>However, if multiple GetObject requests are made for the same object within 24 hours, only the time of the first request is recorded as the object's last access time. For instance, if an object is downloaded at 8:00 a.m. on January 1, its access time will be recorded as 8:00 a.m. on January 1. Any subsequent download requests before 8:00 a.m. on January 2 will not update the access time. The access time will only update if the object is downloaded after 8:00 a.m. on January 2. Other operations update the object's last access time based on the time of the operation. For more information, see [Which operations update an object's last access time?](https://docs.byteplus.com/docs/tos/Which-operations-update-the-lastaccesstime). |
|Permissions |Before you begin, ensure that your account has the necessary permissions to enable access monitor and configure lifecycle rules. Specifically:<br><br><br>* Enable access monitor: tos:PutBucketAccessMonitor and tos:GetBucketAccessMonitor<br><br>* Configure lifecycle rules: tos:PutLifecycleConfiguration and tos:GetLifecycleConfiguration<br><br><br>For more information, see [Bucket policy](https://docs.byteplus.com/en/docs/tos/docs-overview_5). |


<span id="cebe8b4c"></span>
## Step 1: Enable access monitor

Before creating a lifecycle rule based on last access time, you must enable the **Access monitor** feature. Starting from the day this feature is enabled, TOS will automatically begin tracking the last access time of all objects in the bucket.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. In the **Buckets** list, click the bucket you want to manage.

3. In the left navigation pane, select **Basic configurations \> Lifecycle**.

4. On the **Lifecycle** page, switch on **Access monitor**.

5. In the box that appears, click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Though TOS currently does not charge for this service, enabling the access monitor feature will generate monitoring\-related costs.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Before disabling access monitor, you must first delete all lifecycle rules based on last access time. Otherwise, this feature cannot be disabled.   </div>
   


<span id="efbd5e78"></span>
## Step 2: Create a lifecycle rule


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. In the **Buckets** list, click the bucket you want to manage.

3. In the left navigation pane, select **Basic configurations \> Lifecycle**.

4. On the **Lifecycle** page, click **Create rule**.

5. On the Create Lifecycle page, configure the following parameters:

   
   |**Parameter** |**Description** |
   |---|---|
   |Rule name |Used to identify the lifecycle rule. Lifecycle names must:<br><br><br>* Be between 1 and 255 characters long.<br><br>* Be unique within the bucket. |
   |Status |Determines when the rule takes effect. The options are:<br><br><br>* **Enable**: The rule takes effect immediately after creation.<br><br>* **Disable**: The rule is created but remains inactive. |
   |Impact Scope |Defines the scope of objects affected by the lifecycle rule. The options are:<br><br><br>* **Entire bucket**: The rule applies to the entire bucket.<br><br>* **Specify prefix**: The rule applies to objects with the specified prefix. The prefix cannot include the bucket name. For example, if you want to apply the rule only to objects starting with the prefix `prefix`, select **Specify prefix** and set Prefix to `prefix`. Follow these guidelines when specifying a prefix:<br><br>   * Prefixes can contain Chinese characters, letters, numbers, and common symbols.<br><br>   * Length must be between 1 and 1,024 characters.<br><br>   * Prefixes cannot start with a forward slash (/) or backslash (\). Consecutive forward slashes (/) are not allowed.<br><br>   * ".." cannot be used as a directory name.<br><br>   * Regular expressions are not supported for prefix matching. |
   |Tag |TOS allows you to configure lifecycle rules for objects with specific tags, supporting up to ten tags. For more information, see [Managing object tags](https://docs.byteplus.com/docs/tos/docs-managing-file-labels).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">For a lifecycle rule to take effect, an object must match both the tag key and value specified in the rule.</div><br> |
   |File size |Specifies the size range of objects to which the lifecycle rule applies. Valid range: [1 B, 5 TiB]. The parameters are described below:<br><br><br>* **Specify the minimum file**: The smallest size of an object to which the rule applies.<br><br>* **Specify the maximum file**: The largest size of an object to which the rule applies.<br><br><br>If both **Specify the minimum file** and **Specify the maximum file** are selected, the lifecycle rule only applies to objects whose sizes fall within this range.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If both are configured, the maximum size must exceed the minimum size.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The rule will apply to all objects regardless of size if the <strong>file size</strong> is not specified, as long as other policy conditions are met.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">A minimum charge applies to objects in Infrequent Access Storage, Flashback Archive, Archive, Cold Archive, and Deep Cold Archive based on file size. Objects smaller than 64 KiB are charged as if they were 64 KiB. To optimize storage costs, we recommend transitioning only objects larger than 64 KiB.</div><br> |
   |Effective policy |Select **Last access time**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Before setting <strong>Effective policy</strong> to <strong>Last access time</strong>, you must switch on <strong>Access monitor</strong>. If <strong>Access monitor</strong> is not enabled on the <strong>Lifecycle</strong> page, you can enable it quickly below <strong>Last access time</strong>.</div><br> |
   |Latest file version expiration policy |Transitions latest object versions. This policy only supports **Specify days**. Once the desired number of days has been set, TOS will automatically transition any latest version that remains unaccessed for the preset duration to the target storage type.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If <strong>versioning</strong> is enabled for your objects, this rule applies to the latest versions. To clear historical versions, enable <strong>File history version expiration policy</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you select multiple expiration policies, make sure the time interval between any two policies is greater than or equal to the minimum storage duration for each respective storage type. Otherwise, early deletion charges may apply. The minimum storage durations are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Infrequent Access Storage: 30 days</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Flashback Archive: 90 days</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Archive: 90 days</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Cold Archive: 180 days</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Deep Cold Archive: 180 days</div><br><br><br>      <div data-tips="true" data-tips-type="warning">For example, if the number of days after which in\-scope objects will automatically transition to Flashback Archive is set to 90, the transition to Archive must occur after at least 180 days to avoid early deletion charges.      </div><br>       |
   |File history version expiration policy |Transitions historical object versions. This policy only supports **Specify days**. Once the desired number of days has been set, TOS will automatically transition any historical version that remains unaccessed for the preset duration to the target storage type.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you select multiple expiration policies, make sure the time interval between any two policies is greater than or equal to the minimum storage duration for each respective storage type. Otherwise, early deletion charges may apply. The minimum storage durations are as follows:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Infrequent Access Storage: 30 days</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Flashback Archive: 90 days</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Archive: 90 days</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Cold Archive: 180 days</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Deep Cold Archive: 180 days</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For example, if the number of days after which in\-scope objects will automatically transition to Flashback Archive is set to 90, the transition to Archive must occur after at least 180 days to avoid early deletion charges.</div><br> |
   

6. Click **Create**.

7. In the box that appears, click **OK**.

   After creating a lifecycle rule, you can view it in the rules list.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After creating a lifecycle rule, you can copy or search for the rule:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Copy a lifecycle rule: On the <strong>Lifecycle</strong> page, click <strong>...</strong> \> <strong>Replication rule</strong> in the <strong>Actions</strong> column of the rule you want to copy. The system will automatically populate the content of the original rule. Based on this, you can adjust the rule parameters to meet your current requirements.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Search for a lifecycle rule: On the <strong>Lifecycle</strong> page, click the search icon next to the <strong>Rule name</strong> or <strong>Scope of application</strong> column. You can search for specific lifecycle rules by name or scope.   </div>
   


<span id="c82fe8dd"></span>
## Related operations

You can retrieve and analyze access logs generated during your interactions with TOS through Torch Log Service. When the log field `RequestSourceType` is `lifecycle`, it indicates that the request is a lifecycle rule request. You can use this field to query the request time, Object Key, and other lifecycle rule request information. For instructions, see [Log analysis](https://docs.byteplus.com/docs/tos/Log-analysis).

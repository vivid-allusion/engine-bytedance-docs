---
title: "Configuring lifecycle rules based on last modified time"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-setting-lifecycle-rules"
---

With TOS, you can configure lifecycle rules based on when an object was last modified (last modified time). If an object remains unmodified for a preset number of days, you can instruct TOS to move it to a more cost\-effective storage type. TOS can also help you delete long\-unmodified data in batches. This topic introduces the use cases, notes, and steps for configuring lifecycle rules based on last modified time.

<span id="92050f1f"></span>
## Use cases

This approach is suitable for scenarios in which data access patterns are fixed or large batches of data need to be deleted. Examples include:


* Log files are uploaded periodically but only need to be retained for one week or one month, after which they need to be deleted.

* Some files are frequently accessed within a given time period. After this period, the files may no longer be accessed and should be transitioned to Infrequent Access Storage or Archive, or deleted.

* A large number of files need to be batch deleted from a bucket. Manually deleting them is both time\-consuming and subject to a quantity limit. If lifecycle rules are configured for the bucket, all files can be deleted as scheduled.


<span id="da1b29c6"></span>
## Notes


|**Category** |Considerations |
|---|---|
|Usage limits |* Transitioning appendable objects based on the last modified time is not supported.<br><br>* A lifecycle rule can include policies based on either the last modified or access time, but not both. |
|Intelligent Tiering |* Objects stored in Intelligent Tiering can only be transitioned to Flashback Archive via lifecycle rules.<br><br>* When an object is transitioned from Standard Storage to Intelligent Tiering via lifecycle rules, it is placed in the frequent access tier. To transition an object from Infrequent Access Storage to Intelligent Tiering, it must have been uploaded more than 30 days ago. It will then be placed in the infrequent access tier of Intelligent Tiering. |
|Operations that update an object's last modified time |Operations such as renaming or overwriting an object update its last modified time. For more information, see [Which operations update an object's last modified time?](https://docs.byteplus.com/docs/tos/Which-operations-update-the-lastmodifytime). |
|Permissions |Before you begin, ensure that your account has the `tos:PutLifecycleConfiguration` and `tos:GetLifecycleConfiguration` permissions. For more information, see [Bucket policy](https://docs.byteplus.com/en/docs/tos/docs-overview_5). |


<span id="e2bc5a08"></span>
## Steps


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. In the **Buckets** list, click the bucket you want to manage.

3. In the left navigation pane, select **Basic configurations \> Lifecycle**. On the **Lifecycle** page, click **Create rule**.

4. On the **Create Lifecycle** page, configure the following parameters:

   
   |**Parameter** |**Description** |
   |---|---|
   |Rule name |Used to identify the lifecycle rule. Lifecycle names must:<br><br><br>* Be between 1 and 255 characters long.<br><br>* Be unique within the bucket. |
   |Status |Determines when the rule takes effect. The options are:<br><br><br>* **Enable**: The rule takes effect immediately after creation.<br><br>* **Disable**: The rule is created but remains inactive. |
   |Impact Scope |Defines the scope of objects affected by the lifecycle rule. The options are:<br><br><br>* **Entire bucket**: The rule applies to the entire bucket.<br><br>* **Specify prefix**: The rule applies to objects with the specified prefix. The prefix cannot include the bucket name. For example, if you want to apply the rule only to objects starting with the prefix `prefix`, select **Specify prefix** and set **Prefix** to `prefix`. Follow these guidelines when specifying a prefix:<br><br>   * Prefixes can contain Chinese characters, letters, numbers, and common symbols.<br><br>   * Length must be between 1 and 1,024 characters.<br><br>   * Prefixes cannot start with a forward slash (/) or backslash (\). Consecutive forward slashes (/) are not allowed.<br><br>   * ".." cannot be used as a directory name.<br><br>   * Regular expressions are not supported for prefix matching. |
   |Tag |TOS allows you to configure lifecycle rules for objects with specific tags, supporting up to ten tags. For more information, see [Managing object tags](https://docs.byteplus.com/docs/tos/docs-managing-file-labels).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">For a lifecycle rule to take effect, an object must match both the tag key and value specified in the rule.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Tag matching rules do not apply to object parts.</div><br> |
   |Not |Enabling this option will prevent the lifecycle rule from applying to objects with the specified prefix and tag.<br><br>Follow these guidelines when specifying a prefix or tag:<br><br><br>* The total length of a prefix cannot exceed 1,023 characters.<br><br>* The valid characters for a tag include uppercase and lowercase letters, numbers, spaces, and symbols (`: + - = ._ : /`).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">After enabling Not, you will no longer be able to delete incomplete multipart uploads using this lifecycle rule.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can only add one Not configuration to a lifecycle rule.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The Not prefix must start with the prefix provided in the Impact Scope section. For example, if the prefix provided in the Impact Scope section is <code>a/</code>, then the Not prefix must be <code>a/xxx</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The Not tag key must differ from those defined in the Tag section. For example, if the tag <code>"key1":"value1"</code> is provided in the Tag section, then you cannot specify the tag as <code>"key1":"value1"</code> or <code>"key1":"value2"</code> in the Not section.</div><br> |
   |File size |Specifies the size range of objects to which the lifecycle rule applies. Valid range: [1 B, 5 TiB]. The parameters are described below:<br><br><br>* **Specify the minimum file**: The smallest size of an object to which the rule applies.<br><br>* **Specify the maximum file**: The largest size of an object to which the rule applies.<br><br><br>If both **Specify the minimum file** and **Specify the maximum file** are selected, the lifecycle rule only applies to objects whose sizes fall within this range.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If both are configured, the maximum size must exceed the minimum size.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The rule will apply to all objects regardless of size if the <strong>file size</strong> is not specified, as long as other policy conditions are met.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">File size constraints do not apply to part expiration policies.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">A minimum charge applies to objects in Infrequent Access Storage, Flashback Archive, Archive, Cold Archive, and Deep Cold Archive based on file size. Objects smaller than 64 KiB are charged as if they were 64 KiB. To optimize storage costs, we recommend transitioning only objects larger than 64 KiB.</div><br> |
   |Effective policy |Select **Last modified time**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">TOS only retains the time when an object was last modified (last modified time). If you do not update the object's metadata or overwrite the object, the last modified time will remain the same as the creation time. For more information, see <a href="https://docs.byteplus.com/docs/tos/Which-operations-update-the-lastmodifytime">Which operations update an object's last modified time?</a>.</div><br> |
   |Latest file version expiration policy |This policy is turned off by default. The parameters are explained as follows:<br><br><br>* **Specify days** (relative time): Any in\-scope objects that have not been modified within the preset number of days will either be transitioned to a specified storage type or deleted.<br><br>* **Specify date** (absolute time): After the specified date is reached, TOS automatically deletes or transitions objects whose last modified time is earlier than the specified date. Objects whose last modified time is equal to or later than the specified date will remain unaffected.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If <strong>versioning</strong> is enabled for your objects, this rule applies to the latest versions. To clear historical versions, enable <strong>File history version expiration policy</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you select multiple expiration policies, make sure the time interval between any two policies is greater than or equal to the minimum storage duration for each respective storage type. Otherwise, early deletion charges may apply. The minimum storage durations are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Infrequent Access Storage: 30 days</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Flashback Archive: 90 days</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Archive: 90 days</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Cold Archive: 180 days</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Deep Cold Archive: 180 days</div><br><br><br>      <div data-tips="true" data-tips-type="warning">For example, if the number of days after which in\-scope objects will automatically transition to Flashback Archive is set to 90, the transition to Archive must occur after at least 180 days to avoid early deletion charges.      </div><br>       |
   |File history version expiration policy |If versioning is enabled for your bucket, you can activate the historical version expiration policy. This policy is turned off by default. The parameters are explained as follows:<br><br><br>* **Specify days** (relative time): Any in\-scope objects that have not been modified within the preset number of days will either be transitioned to a specified storage type or deleted.<br><br>* **Specify date** (absolute time): After the specified date is reached, TOS automatically deletes or transitions objects whose last modified time is earlier than the specified date. Objects whose last modified time is equal to or later than the specified date will remain unaffected.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you select multiple expiration policies, make sure the time interval between any two policies is greater than or equal to the minimum storage duration for each respective storage type. Otherwise, early deletion charges may apply. The minimum storage durations are as follows:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Infrequent Access Storage: 30 days</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Flashback Archive: 90 days</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Archive: 90 days</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Cold Archive: 180 days</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Deep Cold Archive: 180 days</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For example, if the number of days after which in\-scope objects will automatically transition to Flashback Archive is set to 90, the transition to Archive must occur after at least 180 days to avoid early deletion charges.</div><br> |
   |Part expiration policy |This policy is turned off by default. Once enabled, you can set an expiration period in days. Any uploaded but unmerged parts will be automatically deleted after the expiration period elapses. |
   

5. Click **Create**.

6. In the box that appears, click **OK**.

   After creating a lifecycle rule, you can view it in the rules list.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After creating a lifecycle rule, you can copy or search for the rule:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Copy a lifecycle rule: On the <strong>Lifecycle</strong> page, click <strong>...</strong> \> <strong>Replication rule</strong> in the <strong>Actions</strong> column of the rule you want to copy. The system will automatically populate the content of the original rule. Based on this, you can adjust the rule parameters to meet your current requirements.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Search for a lifecycle rule: On the <strong>Lifecycle</strong> page, click the search icon next to the <strong>Rule name</strong> or <strong>Scope of application</strong> column. You can search for specific lifecycle rules by name or scope.   </div>
   


<span id="51604d23"></span>
## Related operations

You can retrieve and analyze access logs generated during your interactions with TOS through Torch Log Service. When the log field `RequestSourceType` is `lifecycle`, it indicates that the request is a lifecycle rule request. You can use this field to query the request time, Object Key, and other lifecycle rule request information. For instructions, see [Log analysis](https://docs.byteplus.com/docs/tos/Log-analysis).

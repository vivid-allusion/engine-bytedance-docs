---
title: "Creating data subscription rules"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Creating_data_subscription_rules"
---

You can set up data subscription rules to automatically copy data from the source service to a TOS bucket, making data acquisition easier and more efficient. This topic describes how to do so.

## Notes

When using the data subscription feature, pay attention to the following:

* **Supported regions**: Currently, only Asia Pacific (Johor) is supported. If you need to use data subscription in another region, please contact your account manager for assistance.

* **Supported bucket types**: Currently, only FNS buckets can be selected as the destination bucket. HNS buckets are not supported.

* **Out\-of\-order replication**: Objects may not be replicated to your destination bucket in the same order they were written to the source.

* **Guaranteed success rate**: This feature uses asynchronous replication. While it does not ensure 100% replication success, it offers a reliability of at least 99.9% and an automatic retry mechanism.

* **Supported inference endpoint types**: This feature only supports content generated via VeArk inference endpoints, including both preset and customized ones.

* **Historical data**: A data subscription rule only applies to data generated after its creation. It does not apply to data that existed before the rule was created.

* **Scope of application:**  This feature only applies to scenarios that meet all of the following conditions:

   * **Data source**: Data for subscription must come from the **ModelArk** platform.

   * **Supported models:**

      |**Model category** |**Model name** |
      |---|---|
      |Image generation |seedream\-5.0 |
      ||seedream\-4.5 |
      ||seedream\-4.0 |
      ||dola\-seedream\-5.0\-pro |
      ||dola\-seedream\-5.0\-flash |
      |Video generation |dreamina\-seedance\-2.0 |
      ||dreamina\-seedance\-2.0\-fast |
      ||dreamina\-seedance\-2.0\-mini |
      ||dreamina\-seedance\-2.5 |

## Prerequisites

Before creating a data subscription rule, make sure that:

1. You have created a TOS bucket to store the subscribed data. For instructions, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

2. You have permission to write data to your bucket via data subscription. When creating a data subscription rule for the first time, click **One\-click authorization** in the console to create a service\-linked role (`TosSubscribeToArkRole`) and grant it the following key permissions:

   `tos:PutObject`: Used to write ModelArk outputs to the specified bucket.

## Steps

1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Data subscription**.

3. In the upper\-left corner of the **data subscription** page, click **Create data subscription**.

4. On the **Create data subscription rules** page, configure the following parameters.

   |**Parameter** |**Description** |
   |---|---|
   |Rule name |Enter a name for your data subscription rule. Naming rules:<br><br><br>* Rule names can contain Chinese characters and English letters. They cannot exceed 255 characters in length.<br><br>* Each rule name must be unique within the same account. |
   |Enabled status |The status of the data subscription rule.<br><br><br>* Enabled: The rule takes effect immediately after creation and begins replicating eligible data.<br><br>* Disabled: The rule is created, but remains inactive. It can be manually enabled later. |
   |Data source |Currently, only **ARK** is supported. |
   |Inference access point |The inference endpoints supported by VeArk. You can select multiple endpoints.<br><br>> **tip**<br><br><br>> Inference endpoints must be unique across different rules.<br> |
   |Destination bucket region |The region of the bucket where the replicated objects are stored. The available destination buckets depend on the region you select.<br><br>> **tip**<br><br><br>> Currently, only Asia Pacific (Johor) is supported. If you need to use data subscription in another region, please contact your account manager for assistance.<br> |
   |Destination bucket |The name of the destination bucket.<br><br>Select an existing bucket in the current region to store ModelArk outputs. The source data and the destination bucket must be located in the same country. Cross\-border replication is not supported. |
   |Destination storage type |The storage type used when the replicated objects are stored in the destination bucket.<br><br>The following storage types are currently available for data subscription: **Standard Storage**, **Infrequent Access Storage**, **Flashback Archive**, **Archive**, **Cold Archive**, and **Deep Cold Archive**. We recommend choosing a storage type based on access frequency and cost. The default is **Standard Storage**. |
   |Destination object renaming rules |To organize the object structure within the destination bucket, you can use a fixed string as the prefix for the replicated object name. For example, use `my-aigc-images/` to store all outputs under that directory.<br><br>Example:<br><br>Suppose the name of the source object is `task123.jpg` and the prefix is set to `generated/`. The resulting object name would be `generated/task123.jpg`.<br><br>> **tip**<br><br><br><br>* > Follow these guidelines when specifying a prefix:<br><br><br>   * > Prefixes can contain Chinese characters, letters, numbers, and common symbols. The prefix length must not exceed 500 characters.<br><br><br>   * > Prefixes cannot start with a forward slash (`/`) or backslash (`\`). Consecutive forward slashes (`/`) are not allowed.<br><br><br>   * > `..` cannot be used as a directory name.<br><br><br>* > If the name of a replicated object is empty, the replication task will fail.<br><br><br>* > If you do not define a prefix rule, the source object name is copied as is.<br> |
   |Overwrite namesake object policy |Specify how to handle an existing object with the same name in the destination bucket.<br><br><br>* **Overwrite**: Replace the destination object with the source object.<br><br>* **Skip**: Keep the destination object and discard the source object for this replication. |

5. Click **Select** to finish creating the rule.

## Related operations

On the **data subscription** page, you can perform the following actions:

* Enable/disable: Activate or pause a data subscription rule with one click.

* **Edit**: Modify configurations of a rule, such as inference endpoint and fixed prefix.

* **Delete**: Permanently delete subscription rules that you no longer need.

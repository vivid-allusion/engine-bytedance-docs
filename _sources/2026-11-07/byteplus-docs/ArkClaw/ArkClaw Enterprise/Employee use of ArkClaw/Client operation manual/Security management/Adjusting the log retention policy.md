---
title: "Adjusting the log retention policy"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/adjusting-the-log-retention-policy"
---

Logs are stored only on the current device and contain only the beginning and end segments of content, such as command output and file differences. You can modify the log retention policy to extend the log retention period, manage local disk usage, or adjust the evidence content retained in logs.

* **Default policy**: Logs are retained for 90 days by default, and the default maximum size limit is 500 MB.

* **Automatic cleanup**: Records that exceed the retention period are deleted automatically. When the maximum size limit is reached, records are deleted starting with the earliest records.

> **warning**

> If you shorten the retention period, lower the maximum size limit, or perform monthly cleanup, earlier logs may be deleted sooner. If you still need these records for audit or troubleshooting, we recommend exporting them before you make the adjustment.

## Procedure

1. Log in to the ArkClaw client locally.

2. Switch to the target ArkClaw.

3. Click "![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_733c3e75c42df2726b84b0bb6a1cd7bc.png)\> Security management".

4. On the "Security logs" tab, click "Retention settings" to expand the log retention policy pane.

5. Adjust the log retention policy as needed.

   > **tip**

   * > To retain audit records for a longer period, choose a longer retention period. Also monitor the maximum size limit to prevent old records from being deleted early due to insufficient space.

   * > To reduce local space usage, lower the maximum size limit, select a more lightweight evidence retention option, and use monthly cleanup. However, we recommend exporting important logs that you still need.

   * > To quickly review key processes only, choose **Summary** to balance issue tracing and local storage costs.

   * > To obtain more complete troubleshooting information, consider choosing **Original text**. We also recommend evaluating the maximum size limit to prevent logs from growing too fast.

   |**Policy item** |**Effect and impact** |Procedure |
   |---|---|---|
   |Retention period |Determines the maximum log retention period. Records that exceed the retention period are deleted automatically. |From the **Retention period** drop\-down list, select 30 days, 60 days, 90 days, 180 days, or 365 days. |
   |Size limit |Determines the maximum local space that logs can occupy. After the limit is reached, records are deleted starting with the earliest records. |From the **Size limit** drop\-down list, select 100 MB, 200 MB, 500 MB, 1 GB, 2 GB, or 5 GB. |
   |Evidence retention |Determines which auxiliary information is retained in logs. |From the **Evidence retention** drop\-down list, select **Metadata only**, **Summary**, or **Original text**.<br><br><br>* **Metadata only**: For command output, file differences, and tools' return values, only the size and hash are recorded. The content is not saved.<br><br>* **Summary**: The beginning and end segments and the line count are also saved, which helps you review what happened.<br><br>* **Original text**: After this option is enabled, the full text of command output, file differences, and tools' return values is encrypted and stored on this device (recognized credentials are still masked). Original text is retained for 30 days and can occupy up to 1 GB. After this limit is exceeded, the earliest records are deleted first. This quota is calculated separately from the maximum log size limit. Actions to view the original text are recorded. |
   |Monthly cleanup |Manually clears log records for a specified month. This option is suitable for releasing local space in batches by time. |To delete logs for a specific month only, confirm the month and the occupied space in the **Monthly cleanup** section, and then click "Clear" to release local space in batches. |

---
title: "Setting a disk cleanup threshold"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/setting-diskclean-threshold"
---

When the disk utilization of a Kafka instance exceeds the preset disk cleanup threshold, the back\-end service automatically deletes historical messages until the disk utilization becomes normal. This topic describes how to modify a disk cleanup threshold.

<span id="e31f4eb3"></span>
## Background information

Each broker in a Kafka instance shares the same disk cleanup threshold. If the overall disk utilization of a Kafka instance reaches the disk cleanup threshold, or if the disk utilization of a broker reaches the disk cleanup threshold due to data imbalance, the back\-end service deletes some historical messages from the respective broker based on the order they were stored, regardless of whether they exceed the message retention period, until the disk utilization becomes normal. This measure prevents Kafka instance anomalies due to high disk utilization and avoids replica desynchronization resulting from brokers failing to synchronize data.

The default disk cleanup threshold of a Kafka instance is 90%, but you can customize this threshold on the instance management page, within the range of 70%–90%.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If the current disk utilization of the instance exceeds the new threshold, lowering the disk cleanup threshold initiates automatic data cleanup for data beyond the new threshold. Proceed with caution when modifying the threshold.</div>


* <div data-tips="true" data-tips-type="tip">We recommend that you set threshold monitoring alarms for broker disk capacity so that you can address the issue promptly before the disk utilization approaches the cleanup threshold, preventing messages from being deleted before natural aging. For more information on the recommended alarm strategies, refer to <a href="https://docs.byteplus.com/en/docs/kafka/recommended-alarm-rules">Instance disk utilization exceeds 30% and disk skew rate exceeds 30%Instance disk utilization exceeds 30% and disk skew rate exceeds 30%</a>.</div>



<span id="2f561105"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. In the **Instance Configuration** pane on the **Instance Details** tab, locate **Disk cleanup level**.

4. Click the Edit icon next to it and reset the disk cleanup threshold.

5. Click **OK**.

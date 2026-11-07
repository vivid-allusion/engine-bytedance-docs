---
title: "Creating alert rules"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules"
---

You can manually configure alert rules by using PromQL statements, use the alert center to monitor specific metrics in specific workspaces, and configure alerts based on the thresholds of metrics. You can also configure the corresponding alert rules by referring to [Common alerts and rule recommendations](https://docs.byteplus.com/en/docs/vmp/Common_alerts_and_rule_recommendations?lang=en). This topic describes how to configure alert rules.

## Prerequisites

You have [created an alert notification policy](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules) and an [alert aggregation policy](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules).

## Limits

* A root user and its IAM users can create up to 500 alert rules in total.

* Up to 100 labels and 100 annotations can be configured for an alert rule.

## Procedureprocedure

1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. In the top navigation bar, select the target region.

3. In the left navigation pane, click **Alert Center \> Alert Rule**. Click **Create** \> **Create manually**.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8c7a885bc9e8c79e44265c312916c013.png)

4. Specify the basic information.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7d6a9a8d66516b146dda620e299edc19.png)

   |**Parameter** |**Description** |
   |---|---|
   |Name |Specify the name of the alert rule. |
   |Project |The project to which the alert rule belongs. |
   |Tags |The tag of the alert rule. A tag consists of a tag key and a tag value. |

5. Configure the alert trigger condition.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c8a1a01e266277ec03052b00ed7cd8aa.png)

|**Parameter** |**Description** |
|---|---|
|workspace |Select the workspace that you want to monitor and trigger alerts from the Workspace list. |
|Query statement |Use standard PromQL statements to configure monitoring objects or metrics. For details, see [Basic usage of PromQL](https://docs.byteplus.com/en/docs/vmp/Basic-PromQL-methods?lang=en). |
|Detect Type |Specifies the type of alert trigger mechanism. The following types are supported: static threshold and dynamic threshold.<br><br><br>* **Static threshold**: The alert trigger condition is set to a fixed threshold. The system sends an alert message when the metric value meets the trigger condition. This type suits stable workloads with clear metric baselines.<br><br>* **Dynamic threshold**: The system automatically pulls historical metric data to learn trends. It dynamically calculates thresholds and identifies abnormal fluctuations. An AI model then determines whether to trigger an alert. No manual maintenance of threshold rules is required. |
|Trigger policy |The specific policy for triggering alerts requires the following parameters to be configured:<br><br><br>* **Static threshold**: Defines the alert trigger rule. This policy takes effect when **Detect type** is set to **Static threshold**.<br><br>   * **Alert level**: Select P0, P1, or P2 to set different alert levels. If you do not select an option, alerts at this level are not configured.<br><br>   * **Comparison condition**: Specify the comparison condition between the PromQL statement and the threshold. You can configure multiple comparison conditions. Valid values: **Greater than**, **Greater than or equal to**, **Less than**, **Less than or equal to**, **Equal to**, and **Not equal to**.<br><br>   * **Threshold**: Set the threshold of the metric.<br><br>   * **Condition duration**: Configures the duration for which the metric meets the condition. Valid values:<br><br>      * **Trigger immediately**: An alert is triggered immediately when the alert condition is met.<br><br>      * **Custom duration**: Select the required duration for triggering the alert. The alert is triggered only when the calculation result of the PromQL statement meets the comparison condition and persists for the specified duration. For example, 1 minute means that the alert will be triggered after the condition has been met for 1 minute.<br><br>* **Dynamic threshold**: Defines the alert trigger rule. This policy takes effect when **Detect type** is set to **Dynamic threshold**.<br><br>   > **tip**<br>   <br><br>   > After you configure parameters, click "**Detection preview**" to view how the dynamic threshold bounds map to the real\-time metric value. The gray shading indicates the pre\-detection interval. The yellow shading indicates suppressed spike data. The red circles indicate the actual anomaly points that triggered alerts.<br>   <br><br>   * **Alert level**: Select P0, P1, or P2 to set different alert levels. If you do not select an option, alerts at this level are not configured.<br><br>   * **Duration**: The duration for which an abnormal condition must persist to trigger an alert. When you select **Trigger immediately**, an alert is triggered immediately after a single detection meets the abnormal condition. When you select a specific duration, an alert is triggered only after the abnormal condition is continuously met for the duration.<br><br>   * **Model sensitivity**: The core configuration that controls the sensitivity of anomaly detection. It determines how strongly the model responds to metric fluctuations. Higher sensitivity makes detection more sensitive and more likely to classify fluctuations as anomalies.<br><br>   * **Anomaly trend**: Defines the scope of anomaly trends. For example, "Increase or decrease" means upward or downward trends that reach the anomaly range calculated by the AI model are detected.<br><br>   * **Spike suppression**: Controls whether jitter anomalies are included in anomaly detection. Use it to handle spike data. This option is enabled by default. When this option is enabled, spike data is automatically suppressed and flagged, reducing false positives and improving alert accuracy.<br><br>   * **Zero or missing data detection**: Detects scenarios where metrics stay at 0 or are missing. This option is disabled by default. When this option is enabled, the system detects an anomaly when data drops to zero or goes missing and the anomaly step threshold is reached.<br><br>      > **tip**<br>      <br><br>      > The anomaly step is the step count threshold for anomaly detection. One step equals one data point. For metrics with 1\-minute granularity, a maximum of 30 steps can be configured. For metrics with other granularities, a maximum of 24 steps can be configured.<br>      <br><br>   * **Baseline threshold**: The detection range for metric values. This option is disabled by default. When this option is enabled, an alert is generated only when the metric value meets the baseline threshold and the detection result meets the alert trigger condition. This prevents false positives caused by metric fluctuations within the normal range. |

6. Configure an alert notification. You can select a suitable notification policy and aggregation policy from the Unified Alert Center or the Original VMP alert policy tab.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_341f4b0116a722eeb10c7abe4813fdab.png)

   |**Parameter** |**Description** |
   |---|---|
   |Notify policy |Select an alert notification policy. The system will send alerts to the specified contacts based on the alert levels and contact groups configured in the notification policy. For more details, see [Creating alert notification policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules). |
   |Aggregation policies |Select an alert aggregation policy. This defines the alert aggregation interval and notification interval. For more details, see [Creating alert aggregation policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules). |

7. Advanced configuration

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1165f8f04e48666854af5d2ef667c98b.png)

   |**Parameter** |**Description** |
   |---|---|
   |Label |Specify a set of additional tags to be added to the alert rule.<br><br>> **tip**<br><br><br>> When you configure multiple labels in different scenarios (such as [creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces?lang=en) and [creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules?lang=en)), the priorities of the labels are sorted in the following descending order: rule label \> global label \> PromQL label.<br> |
   |Annotation |Specify a set of information tags to be added to the alert rule. |

8. Click **Add** to complete the configuration.

---
title: "Alarm management"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Alert_management"
---

EMR Serverless instances provide alarm functionality. When a resource instance triggers an alarm, an alarm history entry is automatically generated to record the name of the faulty resource, the time the alarm occurred, the duration of the alarm, the alarm level, the alarm policy name, and other information. This allows you to review alarm records in a unified and convenient manner.

## prerequisites

* An EMR Serverless instance has been successfully created.

## Limits

* The maximum alarm history retention time is 14 days.

* If the number of historical alarms in the past six months exceeds 5,000, only the most recent 5,000 alarms are displayed.

* From the first time a resource instance triggers an alarm until it returns to normal, this is recorded as a single alarm history entry. If the resource recovers and then triggers another alarm, a new alarm history entry is generated.

## Alarm policy configuration

When configuring relevant alarm policies, users must have cloud monitoring configuration permissions. For detailed instructions, see [Create alarm policy](https://www.volcengine.com/docs/6408/69472).

Go to **Cloud Monitoring**  **\> Alarm Center \> Alarm Policy \> Create Alarm Policy**, and select **E\-MapReduce\-Serverless\-Olap** as the resource type.

> **说明**

> This section mainly lists core metrics. Users can add metrics as needed based on their focus.

|Alarm items |Condition |Rule |Value |Symbol |
|---|---|---|---|---|
|BE maximum storage utilization |Maximum value | |80 |% |
|Cluster maximum CN disk utilization |Maximum value | |80 |% |
|BE maximum CPU utilization |Maximum value | |90 |% |
|BE maximum memory utilization |Maximum value | |80 |% |
|FE node maximum CPU utilization |Maximum value | |90 |% |
|Cluster CN node maximum CPU utilization |Maximum value | |90 |% |
|FE JVM maximum heap memory utilization |Maximum value | |80 |% |
|Error query QPS |Maximum value | |0.5 |Count/s |
|Query response time P95 |Maximum value | |3 |s |
|FE maximum number of connections |Maximum value | |600 |Count |

## View alarm history

1. Log in to [EMR Console ](https://console.volcengine.com/emr/)[EMR Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. In the left navigation bar, click Resources\> Serverless \> Instance/Name \> Monitoring and alerts\> Alert history to enter the alarm history page.

3. At the top of the alarm history list, you can select the target time period and set filter conditions to find the desired alarm history records.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f587191e4cbe40aebe7f113937c54ef8~tplv-goo7wpa0wc-image.image)

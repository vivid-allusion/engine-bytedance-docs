---
title: "ModifyInstanceParameters"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ModifyInstanceParameters-v2"
---

Call ModifyInstanceParameters interface to modify the parameter configuration of the corresponding instance.

<span id="ae5fafe8"></span>
## **Instructions for use**

This interface is used to modify the configuration parameters of the instance, such as message retention duration and maximum message size.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Modifying some configurations will cause the instance to restart, please proceed with caution.</div>


<span id="215b9975"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngqkfgdudt\*\*\*\* |Instance ID. |
|Parameters |String |Yes | |New parameter configuration for Kafka instances.<br><br>Please refer to the table below for the list of currently supported parameters and their default values. You can also go through the documentation [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter) View the details of each parameter.<br><br>When calling the API through Mail carrier, etc., you should pay attention to escaping, such as`{\"LogRetentionHours\":\"72\",\"MessageMaxByte\":\"10\",\"MessageTimestampType\":\"CreateTime\",\"OffsetRetentionMinutes\":\"4320\"}`. |


Parameters parameter description


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|MessageMaxByte |String |No |12 |Maximum message size.<br><br>The unit is MB, and the value range is 1 to 12. Default is 10. |
|LogRetentionHours |String |No |2160 |Message retention duration.<br><br>The unit is hours, and the value range is 0~ 2160, that is, the message is retained for a maximum of 90 days. The default is 72. |
|OffsetRetentionMinutes |String |No |10080 |Spend check point retention time.<br><br>The unit is minutes, and the value range is 1~ 10080, that is, the consumption check point is retained for a maximum of 7 days. The default is 4320. |
|MessageTimestampType |String |No |LogAppendTime |Message time type, supported setting is:<br><br><br>* LogAppendTime: The time the message was written to the server.<br><br>* CreateTime: (Default) The time the Producer created the message. |
|AutoDeleteGroup |String |No |False |Whether to automatically delete Groups. Defaults to false.<br><br><br>* True: If all consumers in a consumer group are Empty, the backend service will automatically delete the consumer group after the consumption check point retention period is exceeded.<br><br>* False: The automatic deletion of the consumption progress does not affect the status of the consumption group, and the group in the Empty state will not be automatically deleted. |


<span id="1c192e0a"></span>
## **response parameter**

None

<span id="4bee3e4b"></span>
## **example**

<span id="930d28ab"></span>
### **Request example**

```JSON
POST /?Action=ModifyInstanceParameters&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnng5ysg5vv9****",
  "Parameters": "{\"LogRetentionHours\":\"72\",\"MessageMaxByte\":\"10\",\"MessageTimestampType\":\"CreateTime\",\"OffsetRetentionMinutes\":\"4320\"}"
}
```


<span id="e44e40a6"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023022719011888DDE2072F6B0A7393B3",
        "Action": "ModifyInstanceParameters",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

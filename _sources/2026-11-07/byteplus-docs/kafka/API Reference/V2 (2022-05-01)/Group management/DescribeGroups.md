---
title: "DescribeGroups"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeGroups-v2"
---

Call the DescribeGroups interface to get the list of consumer groups.

<span id="0f2b95f0"></span>
## **Instructions for use**

This interface is used to obtain the list of consumer groups for the specified instance, and supports filtering by consumer group ID and status.

<span id="0f52cf00"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\*x |Instance ID. |
|PageNumber |Integer |Yes |1 |The page number of the list, with a minimum value of 1. |
|PageSize |Integer |Yes |10 |The number of entries per page in the list, ranging from 1 to 100. |
|GroupId |String |No |Connect\-cluster |Filter by consumer group ID. |


**response parameter**


|Parameter |Parameter type |Example value |Description |
|---|---|---|---|
|Total |Integer |2 |Total number of consumer groups. |
|GroupsInfo |Array of BasicGroupInfo |/ |List of consumption groups. For detailed instructions, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) In the BasicGroupInfo section. |


<span id="551fe0ea"></span>
## **example**

<span id="d9421101"></span>
### **Request example**

```JSON
POST /?Action=DescribeGroups&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnng3s31v076****",
  "PageNumber": 1,
  "PageSize": 2
}
```


<span id="c6d204bb"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023022720461429AE2FDCE34FC0788D62",
        "Action": "DescribeGroups",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "GroupsInfo": [
            {
                "GroupId": "kafka-cnng3s31v076****-connect-cluster",
                "State": "Stable",
                "Description": "test",
                "ProtocolType": "consumer",
                "BalanceAlgorithm": "range"
            }
        ],
        "Total": 1
    }
}
```

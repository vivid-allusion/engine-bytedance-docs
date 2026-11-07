---
title: "DescribeRegions"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeRegions-v2"
---

Call the DescribeRegions interface to view the Region list.

<span id="98de592b"></span>
## **request parameters**

None.

<span id="230e1571"></span>
## **response parameter**


|Name |Type |Example value |Description |
|---|---|---|---|
|Regions |Array of RegionObject |/ |List of regions. For more information on Regions, see [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2). |


<span id="e2841ec9"></span>
## Example

<span id="f97f2fbd"></span>
### **Request example**

```JSON
POST /?Action=DescribeRegions&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka
```


<span id="d3c38c5d"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023032021075995F8AAD5096623174D7C",
        "Action": "DescribeRegions",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Regions": [
            {
                "Description": "ap-southeast-1",
                "RegionId": "ap-southeast-1",
                "RegionName": "ap-southeast-1",
                "Status": "Available"
            }
        ]
    }
}
```

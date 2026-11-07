---
title: "DescribeAvailabilityZones"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeAvailabilityZones-v2"
---

Call DescribeAvailabilityZones interface to view the list of available zones.

<span id="d7cb62bd"></span>
## **request parameters**


|Name |Type |Is it required |Example value |Description |
|---|---|---|---|---|
|RegionId |String |Yes |ap\-southeast\-1 |Region ID, callable [DescribeRegions](https://docs.byteplus.com/en/docs/kafka/DescribeRegions-v2) Query. |


<span id="ffcb641c"></span>
## **response parameter**


|Name |Type |Example value |Description |
|---|---|---|---|
|RegionId |String |ap\-southeast\-1 |Region ID. |
|Zones |Array of ZoneObject |/ |List of availability zones. For more information on Zones, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) The ZoneObject section of the document. |


<span id="605859f7"></span>
## Example

<span id="95b9bc99"></span>
### Request example

```JSON
POST /?Action=DescribeAvailabilityZones&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
    "RegionId": "ap-southeast-1"
}
```


<span id="5ca9b50c"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230227162855CD78212B545D4168BA43",
        "Action": "DescribeAvailabilityZones",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "RegionId": "ap-southeast-1",
        "Zones": [
            {
                "Description": "Zone A",
                "Status": "Normal",
                "ZoneId": "ap-southeast-1a",
                "ZoneName": "ap-southeast-1"
            }
        ]
    }
}
```

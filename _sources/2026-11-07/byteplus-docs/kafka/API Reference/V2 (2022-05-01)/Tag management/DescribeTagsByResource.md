---
title: "DescribeTagsByResource"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeTagsByResource-v2"
---

Call DescribeTagsByResource interface to query the tag\-bound resource.

<span id="13f24608"></span>
## Interface description


* A single call to this interface supports querying up to 10 labels.

* The same label key supports querying up to 3 label values simultaneously.


<span id="58fa106f"></span>
## **request parameters**


|Name |Type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |["kafka\-cnng5b3sy14s\*\*\*\*", "kafka\-cnng5b3sy14s\*\*\*"] |The instance ID of the bound tag.<br><br>Support multiple instance IDs at a time, up to 50 instance IDs at the same time. |
|TagFilters |Array of TagFilterObject |No |[{"Key": "test\-key:", "Value": "test\-val"}] |Filter according to the specified label key value, support filtering according to the label key, or filtering according to the label key + label value.<br><br>For detailed examples and instructions, please refer to [Filtering instances by tag](https://docs.byteplus.com/en/docs/kafka/filtering-instances-by-tag). |
|PageSize |Integer |Yes |10 |When the query results are displayed in pages, this parameter is used to represent the amount of data per page. Values range from 1 to 100. |
|PageNumber |Int32 |Yes |1 |When the query results are displayed in pages, this parameter is used to represent the page number. The minimum supported value is 1. |


<span id="95712218"></span>
## **response parameter**


|**name** |**type** |**sample value** |**describe** |
|---|---|---|---|
|Total |Integer |10 |Specifies the total number of instances corresponding to the label. |
|TagResources |Array of TagResourceObject |/ |The label information of the instance. For detailed instructions, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2). |


<span id="f75a3103"></span>
## Example

<span id="c8696068"></span>
### **Request example**

```JSON
POST /?Action=DescribeTagsByResource&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
   "InstanceIds":["kafka-cnng5b3sy14s****"],
   "PageNumber":1,
   "PageSize":10
}
```


<span id="b58e430e"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230217175421E698024A11179196218F",
        "Action": "DescribeTagsByResource",
        "Version": "2022-01-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "TagResources": [
            {
                "InstanceId": "kafka-cnng5b3sy14s****",
                "Key": "module",
                "Value": "tcp"
            }
        ],
        "Total": 1
    }
}
```

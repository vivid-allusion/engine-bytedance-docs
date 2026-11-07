---
title: "DescribeAcls"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeAcls-v2"
---

Call the DescribeAcls interface to query the created ACL rule policy.

<span id="d2fb0210"></span>
## **Instructions for use**

This interface is used to query the ACL rule policy that has been created, and supports fuzzy search according to the content of some fields.

<span id="c926604e"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnoe8qu6hgw1\*\*\*\* |The instance ID of the ACL to be queried. |
|PageNumber |Integer |Yes |1 |The page number to be queried. |
|PageSize |Integer |Yes |10 |Maximum number of rules for a single page query. |
|UserName |String |No |Test |SASL username, used to filter ACL rules containing the specified user. Supports filtering using string fuzzy match. |
|Ip |String |No |192.168 |IP address, used to filter ACL rules containing the specified IP address. Supports filtering using string fuzzy match. |
|ResourceType |String |No |Topic |Resource type, supported to be configured as Topic or Group. Indicates that the ACL rules containing the specified resource type are filtered. Fuzzy match is not supported. |
|PatternType |String |No |Literal |Match type, supported to be configured as Literal or Prefixed. Indicates that the filter contains ACL rules for the specified match type. Fuzzy match is not supported. |
|Resources |String |No |Test |Resource name or name prefix for filtering. Supports fuzzy matching. |
|AccessPolicy |String |No |Read |Access policy for filtering. Fuzzy matching is not supported. |


<span id="ab6c4d30"></span>
## **response parameter**


|Parameter |Parameter type |Example value |Description |
|---|---|---|---|
|Total |Integer |1 |The total number of rules that meet the query criteria. |
|Acls |Array of AclObject |/ |List of query results for the current page. For detailed instructions, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) AclObjectpart in. |


<span id="3cffd1da"></span>
## **example**

<span id="cda598e3"></span>
### **Request example**

```JSON
POST /?Action=DescribeAcls&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
    "InstanceId": "kafka-cnoe8qu6hgw1****",
    "PageNumer": 1,
    "PageSize": 20,
    "UserName": "test",
    "Ip": "192.168",
    "ResourceType": "Topic",
    "PatternType": "Literal",
    "Resource": "test",
    "AccessPolicy": "Read"
}
```


<span id="eb8e268e"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20231009164722454D149CF757A9BFA1DC",
        "Action": "DescribeAcls",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Total": 1,
        "Acls": [
            {
                "UserName": "test",
                "Ip": "192.168.0.1/18",
                "ResourceType": "Topic",
                "PatternType": "Literal",
                "Resource": "test",
                "AccessPolicy": "Read"
            }
        ]
    }
}
```
